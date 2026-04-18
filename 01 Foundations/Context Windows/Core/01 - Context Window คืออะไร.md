---
tags:
  - context
  - token
  - llm
  - contextwindow
type: note
status: evergreen
source: "Context Windows/knowledge-base-context-windows.md"
parent_note: "[[Context Windows - MOC]]"
---

# Context Window คืออะไร

## นิยาม (ระดับพื้นฐาน)

**context window** คือปริมาณข้อความที่โมเดล "มองเห็นได้ระหว่างตอบ" ในช่วงเวลาหนึ่ง

- **ความหมาย**: ความจำระยะสั้นของโมเดล (`working memory`)
- **ไม่ใช่**: ความรู้ที่โมเดลเรียนรู้ตั้งแต่แรก (อยู่ใน weights แล้ว)

```
ตัวอย่างสมดุล:
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

หลังจากการ train:
  Model weights = ความรู้ทั่วไป (เช่น "อักษร", "หลักไวยากรณ์")
  คงอยู่ตลอดเวลา ไม่เปลี่ยน

ตอนตอบคำถาม (`inference`):
  context window = ข้อมูล + คำถาม ที่ "เห็นอยู่ตอนนี้"
  เปลี่ยนทุก request

ตัวอย่าง:
  User: "ผมชื่อ Alice" ← อยู่ใน context
  User: "ผมชื่อเรื่อง?" 
  Model: "ชื่อ Alice" ← อ้างอิงจาก context ข้างบน
  
  ถัดไป User ใหม่: "ผมชื่อ Bob"
  Model: "ชื่อ Bob" ← context ใหม่ จำ Alice ไม่ได้
```

---

## หน่วยพื้นฐาน: Token

โมเดลไม่ได้อ่าน "ตัวอักษร" แต่อ่าน **"tokens"** — หน่วยที่เล็กกว่าคำ

```
Text:     "Hello world"
Tokens:   ["Hello", "Ġworld"]  (Ġ = space)
IDs:      [15496, 995]

Text:     "transformer"
Tokens:   ["transform", "##er"]  (##er = continuation)
IDs:      [8499, 2200]
```

**ค่าประมาณคร่าว ๆ สำหรับภาษาอังกฤษ (OpenAI):**
| | ค่าประมาณ |
|---|---|
| 1 token | ≈ 4 ตัวอักษร |
| 1 token | ≈ 0.75 คำ (3 tokens = 4 คำ) |
| 100 tokens | ≈ 75 คำ |
| หน้ากระดาษ (~500 คำ) | ≈ 665 tokens |

**💡 ความสำคัญ:**
- context window วัดเป็น **tokens ไม่ใช่คำ**
- ข้อมูล 100 หน้า (50,000 คำ) = ~66,500 tokens ← อาจไม่พอกับ model 128K
- Tokenizer ต่างกัน → token count ต่างกัน (เช่น GPT2 vs BERT)

---

## อะไรบ้างที่ใช้พื้นที่ใน Context Window

context window **ไม่ใช่แค่คำถามปัจจุบัน** แต่รวมทุกอย่างที่ถูกส่งเข้า runtime:

| ส่วนประกอบ | เนื้อหา | จำนวน tokens โดยประมาณ |
|---|---|---:|
| system prompt | "You are a code reviewer..." | 500 |
| tools / schemas | 5 function definitions | 2,000 |
| ประวัติการสนทนา | 10 turns ก่อนหน้า | 15,000 |
| คำถามปัจจุบัน | "Review this PR: [code]" | 50,000 |
| Images / PDFs | ไฟล์ที่อัปโหลด | 10,000 |
| **รวมฝั่ง input** | ↑ ทั้งหมดนี้ | **77,500** |
| **พื้นที่สำรองฝั่ง output** | พื้นที่สำหรับคำตอบ | 4,000 |
| **ใช้ไปทั้งหมด** | | **81,500** |
| **เพดาน context** | Claude: 200K | 200,000 |
| **พื้นที่สำรอง** | พื้นที่เหลือ | 118,500 |

**ความสำคัญ:**
- ❌ ถ้า input 190K + output reserve 4K → เกิน 194K
- ❌ ประวัติสนทนาสะสมไปเรื่อย ๆ → token เพิ่มทุก turn
- ✓ ควรเช็ก token count ก่อนส่ง request

---

## สมดุลระหว่าง Input กับ Output

**ภาพรวมการเติบโตของแต่ละส่วนตามจำนวนรอบสนทนา**

| ส่วนประกอบ | Tokens | สถานะ | หมายเหตุ |
|---|---:|---|---|
| System + Tools + Docs | 70K | คงที่ | ใช้ซ้ำทุก request |
| Historical Messages (Turn 1) | 5K | เพิ่มขึ้น | สะสมตามจำนวนรอบ |
| Historical Messages (Turn 50) | 95K | เพิ่มขึ้น | อาจใหญ่ขึ้นได้หลายเท่า |
| Current Query | 10K | ใหม่ | เปลี่ยนทุก request |
| **Total Input (Turn 50)** | **175K** | — | Approaching limit |
| **Output ที่เหลือได้** | **25K** | ⚠️ ตึง | เหลือ buffer เพียง 12.5% |

**ตัวอย่างสถานการณ์ (Claude 200K):**

| สถานการณ์ | จำนวน turns | Input | พื้นที่ output | สถานะ |
|---:|---:|---:|---:|---|
| บทสนทนาสั้น | 1 | 80K | 120K | ✓ ปลอดภัย (buffer 60%) |
| บทสนทนาปานกลาง | 20 | 140K | 60K | ⚠️ เริ่มตึง (buffer 30%) |
| บทสนทนายาว | 50 | 175K | 25K | ❌ ตึงมาก (buffer 12.5%) |
| บทสนทนายาวมาก | 60 | 185K | 15K | ❌ อันตราย (buffer < 8%) |

**เมื่อ buffer เริ่มตึง ควรทำอย่างไร**

| ระดับ buffer | การตีความ | คำแนะนำ |
|---|---|---|
| > 20% | ไปต่อได้ | ใช้งานตามปกติ |
| 10-20% | ต้องเฝ้าดู | ติดตามอย่างใกล้ชิด |
| < 10% | ต้องจัดการ | ตัดประวัติหรือสรุปย่อ |
| < 5% | วิกฤต | เปลี่ยนไปใช้ RAG หรือ chunking |

---

## Input กับ Output ใช้งบ Context Window ร่วมกัน

**ตัวอย่างการแบ่งงบ context (Claude 200K):**

| ส่วนประกอบ | Tokens | % ของงบ |
|---|---:|---:|
| system prompt | 3K | 1.5% |
| Tools | 5K | 2.5% |
| Documents | 50K | 25% |
| Chat History | 80K | 40% |
| **Total Input** | **138K** | **69%** |
| **Output Reserved** | **15K** | **7.5%** |
| **Remaining Buffer** | **47K** | **23.5%** |

**ตัวอย่างการตั้งงบ output**

| การตั้ง `max_tokens` | พื้นที่ output | พื้นที่ buffer ที่เหลือ | สถานะ |
|---:|---:|---:|---|
| 10,000 | 10K | 37K | ✓ ปลอดภัย (เหลือพอมาก) |
| 15,000 | 15K | 32K | ⚠️ เริ่มตึง (ใกล้เพดาน) |
| 40,000 | 40K | -3K | ❌ Error (เกินงบ) |

**พฤติกรรมสำคัญของ Anthropic Claude**

| เงื่อนไข | พฤติกรรม |
|---|---|
| input + output > 200K | 406 Validation Error |
| Request rejected | No silent truncation (explicit error) |
| Prevention | Count tokens **before** sending |

---

## ขนาด Context Window ของผู้ให้บริการหลัก

| Model | ขนาด context | งานที่เหมาะ |
|---|---:|---|
| **Claude Opus/Sonnet 4.6** | 200K tokens | เอกสารใหญ่, บทสนทนายาว |
| **GPT-4o** | 128K tokens | เอกสารขนาดกลาง + งานโค้ด |
| **Gemini 2.0/Gemini Pro** | 1M tokens | ขนาดใหญ่สุด (เอกสารเต็มคลัง) |
| **Llama 3.1 70B** | 128K tokens | Open source alternative |

**🔴 ข้อควรระวัง:**
- ตัวเลขเปลี่ยนเรื่อย ๆ → ดู official page ล่าสุด
- context size ไม่ได้เป็นตัวแทนของ quality โดยตรง (ยาวไม่ได้แปลว่าดีเสมอ)
- ค่าใช้บริการอาจเพิ่มขึ้นตาม context (ส่วนใหญ่เรียกเก็บต่อ 1M tokens)

**ตัวอย่างการเลือก model**

งาน: review PR comment + เอกสาร 50 หน้า

**ขั้นที่ 1: ประมาณจำนวน tokens**

| Component | Tokens |
|---|---:|
| Code + docs | 40K |
| History + buffer | 8K |
| **Subtotal Input** | **48K** |
| Output reserve | 5K |
| **Total Needed** | **53K** |

**ขั้นที่ 2: เลือก model และดูต้นทุน**

| Model | Context | Buffer | Cost/Request | สถานะ |
|---|---:|---:|---|---|
| Claude 200K | 53K | 147K | $0.16 | ✓ ปลอดภัยและคุ้มสุด |
| GPT-4o 128K | 53K | 75K | $0.27 | ✓ ใช้ได้แต่แพงกว่า |
| Gemini 1M | 53K | 947K | varies | ⚠️ เกินความจำเป็น |

**ข้อแนะนำ:** Claude (คุ้มค่าและมี buffer เหลือมาก)

---

## บทสนทนาสะสมอย่างไร

ในแต่ละ turn โมเดลจะได้รับ **ประวัติทั้งหมด** ไม่ใช่แค่ข้อความล่าสุด

**ตัวอย่างการสะสมของ tokens ตามจำนวน turns (Claude 200K):**

| Turn | History | Query | Total | % Used | โซน | สถานะ |
|---:|---:|---:|---:|---:|---|---|
| 1 | — | 5K | 5K | 2.5% | ปลอดภัย | ✓ เริ่มบทสนทนาใหม่ |
| 5 | 10K | 5K | 15K | 7.5% | ปลอดภัย | ✓ ยังเหลือมาก |
| 10 | 35K | 5K | 40K | 20% | ปลอดภัย | ✓ ค่อย ๆ โต |
| 20 | 70K | 5K | 75K | 37.5% | เฝ้าดู | ⚠️ เริ่มจับตา buffer |
| 50 | 175K | 5K | 180K | 90% | อันตราย | ❌ เหลือเพียง 20K |
| 60 | 210K | 5K | 215K | 107% | เกินเพดาน | ❌ เกิน limit แล้ว |

**แนวทางตีความแต่ละโซน**

| โซน | Input | พื้นที่ output | สิ่งที่ควรทำ |
|---|---|---|---|
| **ปลอดภัย** (< 70%) | 0-140K | > 60K | ✓ ใช้งานตามปกติ |
| **เฝ้าดู** (70-85%) | 140-170K | 30-60K | ⚠️ ติดตามอย่างใกล้ชิด |
| **อันตราย** (85-95%) | 170-190K | 10-30K | ❌ เตรียมตัดทอนข้อมูล |
| **เกินเพดาน** (> 95%) | > 190K | < 10K | ❌ มีโอกาส error สูงมาก |

**ผลกระทบในการใช้งาน:**
- ❌ สนทนานาน → token count ยิ่งเพิ่มขึ้น
- ❌ ต้อง manual trimming/summarization ถ้า context ใกล้เต็ม
- ✓ Prompt caching ช่วยได้ถ้า prefix (system + docs) ซ้ำ

---

## ⚠️ Context Window ใหญ่ขึ้น ไม่ได้แปลว่าดีกว่าเสมอ

### context rot (ปัญหาจริง)

เมื่อ context ยาวมากเกินไป โมเดลอาจลืมสิ่งสำคัญตรงกลาง

**ตัวอย่าง:**
```
Needle-in-Haystack Test:

Context = 100K tokens (เอกสาร)
Question = "Key fact คืออะไร?" (ซ่อนอยู่เรื่อย ๆ)

ผลลัพธ์:
- Fact อยู่ ตำแหน่ง 10% (ต้น): ✓ accuracy ~95%
- Fact อยู่ ตำแหน่ง 50% (กลาง): ✓ accuracy ~70-80%
- Fact อยู่ ตำแหน่ง 90% (ท้าย): ✓ accuracy ~90%
```

**เหตุผล:**
- Transformer attention คำนวณหนักเพื่อ "prominent" tokens (beginning/end)
- Tokens ตรงกลาง → ถูกลืม (Attention จ่ายความสนใจน้อย)

**ผลในทางปฏิบัติ**
```
❌ ใส่เอกสาร 200 หน้า + คำถามปลายน้อย
→ อาจหา answer ไม่ได้ ถึงแม้ข้อมูลมีอยู่

✓ วาง context ที่สำคัญไว้ต้น/ท้าย (prompt layout)
→ ปรับปรุง accuracy ได้
```

---

## ทำไม Context Window มีขนาดจำกัด

**ไม่ใช่ "policy" แต่เป็นข้อจำกัดทางฟิสิกส์:**

```
Raw Input
    ↓
Tokenization (เรียงให้เป็น tokens)
    ↓
Self-Attention Computation
    ↓
    ❌ PROBLEM: Attention = O(n²)
       - n = 128K tokens
       - Computation: 128K × 128K = 16 billion operations per layer
       - ความต้องการ memory: เยอะมาก
       - Latency: ช้า
    ↓
Output Generation
```

**ผลกระทบจริง:**

| Context Size | Computation Cost | Memory | Latency (approx) |
|---|---|---|---|
| 4K tokens | 1x | 1x | ~100ms (prefill) |
| 32K tokens | 64x | ~10x | ~500ms |
| 128K tokens | 1,024x | ~30x | ~2-5 seconds |
| 1M tokens | 65,536x | ~100x | 10+ seconds |

```
📌 "ยิ่ง context ยาว ยิ่งช้า + แพง"

ทำไม 1M context ยัง offer ได้?
→ Optimization techniques (KV cache, quantization, flash attention)
→ ยังคงช้า/แพงกว่า ตามเปอร์เซนต์
```

---

## ดูต่อ

- [[02 - การบริหารและ Context Engineering]] — วิธีจัดการ context อย่างมีประสิทธิภาพ
- [[03 - Prompt Caching]] — การลด cost ด้วย prefix caching
- [[01 Foundations/LLM Foundations/Core/08 - Data, Pretraining และ Model Modes|Data, Pretraining และ Model Modes]] — แยก `weights`, `context`, และ `external memory`
- [[01 Foundations/LLM Foundations/Core/04 - Inference, Context และ RAG|Inference และ RAG]] — บริบท context ในระบบ serving
- [[01 Foundations/LLM Foundations/Core/09 - Serving Metrics และระบบ Production LLM|Serving Metrics และระบบ Production LLM]] — prefill, decode, TTFT, และ cache trade-offs
- [[02 AI Systems/RAG/RAG - MOC|RAG - MOC]] — ดูว่าข้อจำกัด context window มีผลต่อ retrieval, chunking, และ context assembly อย่างไร
- [[Context Windows - MOC]]
