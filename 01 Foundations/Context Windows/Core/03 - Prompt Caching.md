---
tags:
  - context
  - caching
  - promptcaching
  - latency
  - cost
type: note
status: evergreen
source: "Context Windows/knowledge-base-context-windows.md"
parent_note: "[[Context Windows - MOC]]"
---

# Prompt Caching

## Prompt Caching คืออะไร

**เทคนิคเพิ่มประสิทธิภาพที่ reuse ผลการคำนวณ** เมื่อ prefix เดิม ทำให้เร็วขึ้นและถูกลง

### เปรียบเทียบ 3 requests

| มิติเปรียบเทียบ | Request 1 | Request 2 | Request 3 |
|---|---|---|---|
| **Prefix** | "You are a lawyer. [100K doc]" | (same) | (same) |
| **Query** | "Question 1?" | "Question 2?" | "Question 3?" |
| **สถานะ cache** | ❌ Miss | ✓ Hit | ✓ Hit |
| **Computation** | Compute from scratch | Reuse cached KV | Reuse cached KV |
| **Cost** | $0.30 | $0.03 | $0.03 |
| **Speed** | ~3s | ~200ms | ~200ms |

**เปรียบเทียบต้นทุน**

| วิธี | ต้นทุนรวม | ประหยัดได้ |
|---|---|---|
| ไม่ใช้ caching | $0.30 × 3 = $0.90 | — |
| ใช้ caching | $0.30 + $0.03 + $0.03 = $0.36 | **ประหยัด 60%** |

### อะไรควร cache และอะไรไม่ควร

| Cache ไหม | ประเภทเนื้อหา | เหตุผล |
|---|---|---|
| ✓ ใช่ | System instructions | Stable across requests |
| ✓ ใช่ | Tool definitions | ใช้ซ้ำทุก request |
| ✓ ใช่ | Large documents | Expensive to recompute |
| ✓ ใช่ | Few-shot examples | Static reference data |
| ❌ ไม่ใช่ | Per-request queries | Always new, unique |
| ❌ ไม่ใช่ | User-specific data | Changes per user/session |
| ❌ ไม่ใช่ | Dynamic content | Real-time updates needed |

---

## Prompt Caching ตามผู้ให้บริการ

### Anthropic Claude (ข้อมูลที่ยืนยันได้)

```
Cache Pricing:
  Base input:      $3/MTok (Claude 3.5 Sonnet)
  Cache write:     $3.75/MTok (5-min duration)
  Cache 1-hour:    $6/MTok
  Cache read:      $0.30/MTok ← 10% ของ base!

Requirements:
  Min cacheable: 1,024 tokens
  Default TTL: 5 minutes
  Longer TTL: 1 hour (at 2x cost)
  
Usage:
  cache_control={"type": "ephemeral"}
```

### ตัวอย่าง: economics ของ code review API

**โครงสร้างของ request**
- System prompt: 500 tokens
- Tools (5 functions): 2,000 tokens
- Codebase doc (reused): 50,000 tokens
- Query: 1,000 tokens
- **Total per request: 53.5K tokens**

**เปรียบเทียบต้นทุน**

| Metric | Without Cache | With Cache |
|---|---|---|
| Cost/request | 53.5K × $3 = $0.161 | $0.195 (first request) |
| Subsequent requests | $0.161 each | $0.155 each |
| **Break-even point** | — | **~2 requests** |

**ผลเมื่อปริมาณการใช้งานเพิ่มขึ้น**

| Requests | No Caching | With Caching | Savings |
|---:|---|---|---|
| 1 | $0.16 | $0.20 | — |
| 10 | $1.61 | $0.20 + (9 × $0.155) = $1.60 | ~1% |
| 100 | $16.10 | $0.20 + (99 × $0.155) = $15.55 | ~3% |
| 1,000 | $161 | $0.20 + (999 × $0.155) = $155 | ~4% |

**ข้อสังเกต:** ROI จะค่อย ๆ ดีขึ้นเมื่อปริมาณ request สูงขึ้น

### OpenAI GPT-4o

| คุณสมบัติ | รายละเอียด |
|---|---|
| **Min cacheable** | 1,024 tokens |
| **Default TTL** | 5 minutes |
| **Extended TTL** | 24 hours |
| **Cache read cost** | ~50% of base (check official docs) |

### Google Gemini

| คุณสมบัติ | รายละเอียด |
|---|---|
| **Caching types** | Implicit (automatic) + Explicit |
| **TTL control** | Set expiration time manually |
| **Best for** | High-volume queries on same docs |
| **Pricing** | ⓘ See official pricing page |

---

## ✅ แนวปฏิบัติที่ดีสำหรับการทำ Caching

### รูปแบบการจัดวาง

```python
response = client.messages.create(
    model="claude-opus-4-6",
    max_tokens=4000,
    system=[
        {
            "type": "text",
            "text": "You are a helpful assistant.",
            "cache_control": {"type": "ephemeral"}  # ← ต้อง cache
        },
        {
            "type": "text",
            "text": "Tools:\n[50KB of tool definitions]",
            "cache_control": {"type": "ephemeral"}  # ← ต้อง cache
        },
        {
            "type": "text",
            "text": "[100KB large document]",
            "cache_control": {"type": "ephemeral"}  # ← ต้อง cache
        }
    ],
    messages=[
        {
            "role": "user",
            "content": "Question for today?"  # ← NO cache control
        }
    ]
)

# ตัวอย่างการติดตามผล:
print(f"Cache creation: {response.usage.cache_creation_input_tokens}")
print(f"Cache read: {response.usage.cache_read_input_tokens}")
print(f"Total cost: ({response.usage.cache_read_input_tokens} × $0.30/MTok) + ({response.usage.input_tokens} × $3/MTok)")
```

### เวลาใช้งานมีผล (TTL 5 นาที)

| เวลา | Request | สถานะ cache | ต้นทุน | สถานะ |
|---|---|---|---|---|
| 0:00 | "Review PR1" | Miss | $0.20 | ✓ Cache created |
| 1:00 | "Review PR2" | Hit | $0.02 | ✓ Cheap (10% cost) |
| 2:00 | "Review PR3" | Hit | $0.02 | ✓ Cheap (10% cost) |
| 5:30 | "Review PR4" | Miss | $0.20 | ❌ Expired (lost savings) |

**หลักที่ควรใช้**

| เงื่อนไข | การตัดสินใจ | เหตุผล |
|---|---|---|
| Request frequency < TTL | Use caching | Reuse prefix efficiently |
| Stable content + frequent queries | Use 1-hour TTL | Extended reuse window |
| Requests spread out (> TTL apart) | Skip caching | No ROI, wasted writes |

---

## 📊 ROI ในการใช้งานจริง

### ตัวอย่าง use case: ระบบถามตอบเอกสาร

**สมมติฐาน:** 1,000 users × 5 questions each = 5,000 queries/day, ใช้เอกสาร 100 หน้า (105K tokens) ซ้ำ, TTL 5 นาที, cache hit 80%

**แจกแจงต้นทุน**

| Component | Tokens | Rate | Cost |
|---|---:|---|---|
| **Without Caching** | 5,000 × 105K | $3/MTok | **$1,575/day** |
| **With Caching** | — | — | |
| Cache writes (200 users) | 200 × 105K | $3.75/MTok | $79 |
| Cache reads (80%) | 4,800 × 105K | $0.30/MTok | $151 |
| Fresh queries (20%) | 200 × 105K | $3/MTok | $63 |
| **Total with caching** | — | — | **$293/day** |
| **Savings** | — | — | **81% ($1,282/day)** |

### ตัวอย่าง use case: agentic workflows

**agent แบบหลายขั้นตอน (RAG → reasoning → tool calls)**

**องค์ประกอบต่อ 1 ขั้นตอน**

| Component | Tokens | Reused? |
|---|---:|---|
| System prompt | 10K | ✓ Yes |
| Retrieved docs | 20K | ✓ Yes (same query) |
| Previous context | 5K | ✓ Yes |
| Current step | 2K | ❌ No (changes) |
| **Total per step** | **37K** | — |

**วิเคราะห์ต้นทุน (10 steps)**

| Scenario | Cost/Step | Total (10 steps) |
|---|---|---|
| ไม่ใช้ caching | $0.111 | $1.11 |
| ใช้ caching | $0.0165 | ~$0.20 |
| **Savings per query** | — | **~$0.91 (85%)** |

**ข้อสังเกต:** agents ได้ประโยชน์จาก caching มาก เพราะหลายส่วน เช่น system, docs, และ context มักคงที่ข้ามหลายรอบ reasoning

---

## ดูต่อ

- [[01 - Context Window คืออะไร]] — พื้นฐาน context window
- [[02 - การบริหารและ Context Engineering]] — หลักการจัด prompt layout
- [[Context Windows - MOC]]
