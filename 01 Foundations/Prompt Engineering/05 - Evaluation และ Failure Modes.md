---
tags:
  - prompting
  - evaluation
  - failuremodes
  - testing
type: note
status: draft
source: "Prompt Engineering/prompt-engineering-knowledge-base.md"
parent_note: "[[Prompt Engineering - MOC]]"
---

# Evaluation และ Failure Modes



---

## ทำไม Evaluation จึงสำคัญ

Anthropic และ Google ต่างย้ำว่าการปรับ prompt โดยไม่มีเกณฑ์วัดผลจะทำให้ optimization ไม่มีทิศทาง

---

## 1. เริ่มจาก Success Criteria

Anthropic: success criteria ที่ดีควร **Specific** และ **Measurable**

แทนที่จะบอกว่า "ตอบดี" ให้ระบุว่า:
- "จัดหมวด sentiment ได้ถูกต้อง"
- "สรุปไม่เกิน 3 ประโยค"
- "ตอบอ้างอิงเฉพาะข้อมูลในเอกสาร"

---

## 2. ออกแบบ Eval ให้สะท้อนงานจริง

Anthropic แนะนำว่า eval ควร:
- Task-specific
- มี edge cases
- Automate ได้เมื่อเป็นไปได้
- มีตัวอย่างจำนวนพอ (ไม่ใช่ดูแค่ 1-2 เคส)

---

## 3. อย่าประเมินจากตัวอย่างเดียว

Google Cloud: prompt engineering เป็น iterative process ส่วน Anthropic บอกให้ทดสอบเชิงประจักษ์กับชุดเคสจริง

---

## 4. จับ Failure Mode ให้เป็นหมวด

เมื่อผลไม่ดี แยกให้ออกว่าปัญหาอยู่ที่:

| หมวด | ตัวอย่างปัญหา |
|---|---|
| Instruction ไม่ชัด | ambiguity, missing info, undefined jargon |
| Context ไม่พอ | ขาด grounding data |
| Examples ไม่ครอบคลุม | irrelevant examples, missing edge cases |
| Output format ไม่ชัด | ไม่ระบุ format, conflicting instructions |
| Task ใหญ่เกินไป | too many tasks in one prompt |
| Model ไม่เหมาะ | capability ไม่พอ |
| Parameter ไม่เหมาะ | temperature, top_p |

---

## Failure Modes พื้นฐาน (Google Cloud)

| หมวด | ตัวอย่าง |
|---|---|
| Writing issues | typo, grammar, ambiguity, missing information |
| Instruction/example issues | conflicting instructions, irrelevant examples, missing output spec |
| System design issues | underspecified task, too many tasks in one pass, prompt injection risk |

**ข้อสำคัญจาก Google Cloud:**
- ภาษากดดันหรือข่มขู่โมเดลไม่ใช่ best practice
- ถ้า task ซับซ้อนเกินไปใน prompt เดียว ควรแยก
- ถ้าต้อง parse ต่อด้วยระบบ ควรใช้ JSON, XML, Markdown, YAML

---

## Context และ Grounding

Microsoft: วิธีที่มีประสิทธิภาพที่สุดในการเพิ่มความน่าเชื่อถือคือให้โมเดลมี grounding data แทนการเดาเอง

- ถ้างานพึ่ง facts เฉพาะเอกสาร → แนบเอกสาร/ข้อความ/ตารางมาใน prompt
- ถ้างานพึ่งข้อมูลล่าสุด/ข้อมูลองค์กร → ใช้ retrieval หรือ tool access
- ถ้าไม่มีข้อมูลรองรับ → กำหนด fallback เช่น `not found` หรือ `ข้อมูลไม่ปรากฏในเอกสาร`

---

## ความสัมพันธ์ระหว่าง Prompt Engineering กับ Model / RAG / Tools

| ปัญหา | วิธีที่เหมาะ |
|---|---|
| ความจริงของข้อมูล | เพิ่ม grounding หรือ retrieval |
| Cost/latency | เปลี่ยน model |
| Output format ไม่เสถียร | เพิ่ม schema หรือ structured output |
| หลายขั้นตอนซับซ้อน | แตก workflow หรือใช้ tools |

---

## ดูต่อ

- [[04 - หลักการจากหลายบริษัท]] — best practices
- [[01 Foundations/LLM Foundations/05 - ข้อจำกัดและการประเมินผล LLM|ข้อจำกัดและการประเมินผล LLM]] — model eval vs system eval, hallucination, benchmark limits
- [[01 Foundations/LLM Foundations/04 - Inference, Context และ RAG|Inference, Context และ RAG]] — retrieval failures และ context-related failure modes
- [[02 AI Systems/Evals/Evals - MOC|Evals - MOC]] — ขยายไปสู่ prompt evals, RAG evals, และ agent evals
- [[02 AI Systems/Guardrails/Guardrails - MOC|Guardrails - MOC]] — เชื่อม failure modes กับ output validation, fallback, และ safety controls
- [[Prompt Engineering - MOC]]
