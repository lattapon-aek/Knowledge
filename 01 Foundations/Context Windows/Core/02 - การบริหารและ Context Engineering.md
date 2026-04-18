---
tags:
  - context
  - contextengineering
  - promptlayout
  - tokencount
type: note
status: evergreen
source: "Context Windows/knowledge-base-context-windows.md"
parent_note: "[[Context Windows - MOC]]"
---

# การบริหารและ Context Engineering



---

## ✅ วิธีจัดวาง Prompt ให้มีประสิทธิภาพ

### ปัญหา: context rot (ลืมตรงกลาง)

ถ้าเนื้อหาสำคัญอยู่ตรงกลาง โมเดลจะให้ความสนใจน้อย

### วิธีแก้: การจัดวาง prompt ที่เหมาะ

**ลำดับจากต้นไปท้าย (ตามความสนใจของโมเดล):**

| # | ตำแหน่ง | ส่วนประกอบ | จุดประสงค์ | ระดับความสนใจ | การ cache |
|---|---|---|---|---|---|
| 1 | **ต้น** | System Instructions | บทบาทและพฤติกรรม | ⬆️ สูง (beginning bias) | ✓ cache |
| 2 | ต้น | tools / schemas | Function definitions, rules | ⬆️ สูง | ✓ cache |
| 3 | กลาง | Context / Documents | ข้อมูลพื้นหลังขนาดใหญ่ | ↗️ กลาง | ✓ cache |
| | | ├─ **Important info (sandwich)** | วาง key facts ก่อน/หลังข้อมูลก้อนใหญ่ | ⬆️ สูง | ✓ cache |
| 4 | กลาง-ท้าย | Examples | ตัวอย่าง few-shot | ↗️ กลาง | ✓ cache |
| 5 | **ท้าย** | Question / User Query | คำถามปัจจุบันของผู้ใช้ | ⬆️ สูง (recency bias) | ❌ ใหม่ |

**ตัวอย่างการจัดลำดับข้อความ**

| ลำดับ | เนื้อหา | ประเภท |
|---|---|---|
| 1. ต้น | `"You are a code reviewer..."` | System |
| 2. ถัดมา | `"Company standards:\n..."` | System |
| 3. กลางก้อนใหญ่ | `"[500-page codebase]"` | Context |
| 4. ก่อนท้าย | `"CRITICAL: Check for security holes"` | Important (resurfaced) |
| 5. ท้าย | `"Review this PR: [link]"` | Query |

**ประโยชน์:**
- ✓ Recall: โมเดลจำ info ถูกต้องขึ้น (high attention at start + end)
- ✓ Caching: Stable prefix (items 1-4) cached, only query (item 5) changes
- ✓ Token efficiency: Important info ที่ย้ำซ้ำมีโอกาสถูก cache ได้ง่ายขึ้น

---

## 🔢 Token Counting (สำคัญสำหรับงาน production)

ตัวแม่ของการจัดการ context — **ต้องนับก่อนส่ง request**

### ถ้าไม่นับ token จะเกิดอะไรขึ้น

| วิธี | Input | Output ที่ขอ | Output ที่ได้จริง | ผลลัพธ์ |
|---|---:|---:|---:|---|
| **ไม่ได้นับก่อน** | 150K | 50K | ~30K | ❌ ถูกตัดทอนโดยไม่เตือน |
| **นับก่อนส่ง** | 150K | 50K | 50K | ✓ ได้คำตอบครบ |

**ผลกระทบเมื่อเทียบกัน**

| สถานการณ์ | สิ่งที่เกิดขึ้น | ผลตามมา |
|---|---|---|
| **ไม่ได้นับก่อน** | คิดเองว่ามี output space 50K | Model truncates silently when input exhausts it |
| | 150K input consumes most context | You receive incomplete data unaware |
| | Can't plan alternatives | Unpredictable behavior |
| **นับก่อนส่ง** | รู้ชัดว่า 150K input + 50K output = 200K total | Get full expected response |
| | ตั้ง `max_tokens` ได้ชัดเจน | วางแผนทางเลือกได้ถ้าพื้นที่เริ่มตึง |
| | พฤติกรรมคาดเดาได้ | ได้ข้อมูลครบตามที่คาด |

### เครื่องมือสำหรับนับ

| ผู้ให้บริการ | วิธี |
|---|---|
| **Anthropic** | `POST /v1/messages/count_tokens` API |
| **OpenAI** | `tiktoken` library |
| **Google** | นับอยู่ในเครื่องมือคำนวณราคาและ SDK บางส่วน |

**ตัวอย่าง (Python):**

```python
import anthropic

client = anthropic.Anthropic()

# ประมาณก่อนส่ง request จริง
response = client.messages.count_tokens(
    model="claude-opus-4-6",
    system="You are a code reviewer",
    messages=[
        {"role": "user", "content": "Review this code..."}
    ]
)

print(f"Input tokens: {response.input_tokens}")
print(f"Total with output: {response.input_tokens + 4000}")

# ✓ ต่อเมื่อ input + output ≤ context window
if response.input_tokens + 4000 <= 200_000:
    actual_response = client.messages.create(...)
else:
    # Chunk/summarize/RAG
    pass
```

### การนับ token เอาไปใช้ทำอะไรได้บ้าง

1. **ตรวจสอบพอไหม** → ก่อนส่ง request
2. **คำนวณ cost** → ประมาณค่าใช้งาน (token × rate)
3. **Model routing** → เลือก model ที่เหมาะ (Claude vs GPT-4o)
4. **Truncation strategy** → ตัดข้อมูลตรงไหน ถ้าเกินขีด

---

## 🚨 เมื่อ Context Window เต็ม

### พฤติกรรมของผู้ให้บริการเมื่อเกิน context window

| ผู้ให้บริการ | เงื่อนไข | พฤติกรรม | ลักษณะการตอบสนอง | ข้อมูลหายไหม |
|---|---|---|---|---|
| **Anthropic Claude** | input + output > limit | 406 Validation Error | Explicit (fails early) | ✓ None (rejected) |
| | | "Message too long" | Must handle before sending | |
| **OpenAI GPT-4o** | input + output > limit | Silently truncate input | Implicit (no warning) | ❌ Yes (response incomplete) |
| | | Response may be incomplete | Unpredictable behavior | |
| **Google Gemini** | input > limit | Error with clear message | Explicit (specific error) | ✓ None (rejected) |
| | | Early rejection | Must handle before sending | |

### ทางเลือกเมื่อข้อมูลเกิน (decision matrix)

| วิธี | ความพยายาม | ประสิทธิผล | ต้นทุน | เหมาะกับ |
|---|---|---|---|---|
| **TRUNCATE** | ต่ำ | ❌ ข้อมูลหาย | ต่ำ | ❌ ควรหลีกเลี่ยงถ้าเป็นไปได้ |
| **SUMMARIZE** | สูง | ✓ แต่อาจเสียรายละเอียด | สูง | ✓ เอกสารสำคัญที่ยังต้องใช้ต่อ |
| **RAG** | สูง | ✓ ดึงเฉพาะส่วนที่เกี่ยวข้อง | กลาง | ✓ ฐานความรู้ขนาดใหญ่ |
| **CHUNKING** | สูงมาก | ✓ ประมวลผลเป็นหลายช่วง | สูง | ✓ agent workflows |

**ตัวอย่าง:** แอป review document

```python
def process_document(doc_path, question):
    client = anthropic.Anthropic()
    
    # Step 1: นับก่อน
    count = client.messages.count_tokens(
        model="claude-opus-4-6",
        messages=[{"role": "user", "content": f"Doc: {doc_text}\nQ: {question}"}]
    )
    
    if count.input_tokens < 200_000:
        # ✓ ใส่ทั้งหมด
        response = client.messages.create(
            model="claude-opus-4-6",
            max_tokens=4000,
            messages=[...]
        )
    else:
        # ❌ เกินหลาย tokens
        # Option A: RAG
        relevant_chunks = retrieve_relevant_sections(doc_text, question)
        
        # Option B: Summarize first
        summary = summarize_document(doc_text)  # ← API call
        
        # ✓ ใช้ summary หรือ chunks
        response = client.messages.create(...)
    
    return response
```

> 📌 **ข้อสำคัญ:** อย่าหวังให้ระบบจัดการเอง ต้อง **วางแผนล่วงหน้า** ไว้ก่อนว่าถ้าเกินแล้วจะทำอย่างไร

---

## Extended Thinking / Reasoning Tokens (Optional)

### Extended Thinking ทำงานอย่างไร

**Request 1 (with extended thinking):**
- System + User query + Extended thinking enabled
- Output: Thinking + Answer
- Context consumed: All (thinking NOT stored in history)
- History for next turn: ✓ Answer only (thinking stripped)

**Request 2 (continued conversation):**
- System + History + Query
- History contains only the answer, no thinking
- Result: Saves context space for future turns

### ต้นทุนโดยประมาณ

| Scenario | Input | Thinking | Output | Total | Cost |
|---|---:|---:|---:|---:|---|
| **Normal** | 100 | — | 100 | 200 | $0.006 |
| **With Thinking** | 100 | 2,000 | 100 | 2,200 | $0.066 |
| **Multiplier** | — | — | — | — | **11x more expensive** |

### เมื่อไรควรใช้ Extended Thinking

| ลักษณะงาน | คำแนะนำ | หมายเหตุ |
|---|---|---|
| Complex math/logic | ✓ Yes | Benefits outweigh cost |
| Coding problems | ✓ Yes | Reduces errors |
| Multi-step reasoning | ✓ Yes | Improves accuracy |
| Simple Q&A | ❌ No | Wasted computation |
| FAQ responses | ❌ No | Too expensive for simple answers |
| Real-time queries | ❌ No | Latency penalty too high |

---

## Context Window vs RAG: ควรเลือกอย่างไร

**ไม่ใช่ "หรือ-หรือ" แต่เป็น "เมื่อไร"**

### แนวคิดในการตัดสินใจ

```
Question: "ข้อมูลมี 100 หน้า ต้องตอบคำถาม"

1. Token นับได้พอไหม?
   ├─ ใช่ (100 หน้า = 50K tokens, context = 200K)
   │  └─ ✓ ใส่ทั้งหมด
   │     Pros: Simple, accurate, complete
   │     ข้อเสีย: ช้า, แพง, และเสี่ยง context rot
   │
   └─ ไม่ใช่ (100 หน้า = 200K tokens, context = 200K → no buffer)
      └─ ต้องเลือก:

2. ต้องความถูกต้อง 100% หรือ?
   ├─ ใช่ (Legal/Medical/Critical)
   │  └─ ✓ RAG + verification
   │     - Retrieve relevant sections only
   │     - LLM verify answer
   │     - Cite sources
   │
   └─ ไม่ใช่ (General Q&A, creative)
      ├─ ข้อมูลเปลี่ยนบ่อยไหม?
      │  ├─ ใช่ (News, Current prices)
      │  │  └─ ✓ RAG + realtime fetch
      │  │
      │  └─ ไม่ใช่ (Static docs)
      │     ├─ ต้องประมวลผลเร็วไหม?
      │     │  ├─ ใช่ (< 100ms)
      │     │  │  └─ ✓ RAG (skip slow embedding)
      │     │  │
      │     │  └─ ไม่ใช่
      │     │     └─ ✓ Either (context หรือ RAG ได้)
```

### Comparison Table

| | long context | RAG |
|---|---|---|
| **Speed** | Slow (few seconds) | Fast (< 1s) |
| **Cost** | High (all tokens) | Medium (only relevant) |
| **Accuracy** | High (full context) | High (if retrieve correct) |
| **Hallucination** | Medium (context rot) | Low (grounded in retrieved docs) |
| **Setup** | Simple | Complex (vector DB, embeddings) |
| **ลักษณะงาน** | เอกสารเดี่ยวหรือคลังข้อมูลไม่ใหญ่ | คลังข้อมูลใหญ่หรือข้อมูล real-time |

---

## ดูต่อ

- [[03 - Prompt Caching]] — ลด cost และ latency ด้วย prefix caching
- [[02 AI Systems/RAG/RAG - MOC|RAG - MOC]] — ใช้เมื่อ context เยอะเกิน, ต้องการ precision สูง, หรือไม่อยากยัดข้อมูลทั้งหมดเข้า prompt
- [[02 AI Systems/Guardrails/Guardrails - MOC|Guardrails - MOC]] — guardrail เมื่อ context ใกล้เต็ม, truncation strategy, และ failure handling
- [[Context Windows - MOC]]
