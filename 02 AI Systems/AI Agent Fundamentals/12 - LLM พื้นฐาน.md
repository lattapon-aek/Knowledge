---
tags:
  - llm
  - transformer
  - foundation
type: note
status: draft
source: "HuggingFace Agents Course — Unit 1 \"What are LLMs?\" (huggingface.co/learn/agents-course/unit1)"
parent_note: "[[AI Agent Fundamentals - MOC]]"
---

# LLM พื้นฐาน



---

## LLM คืออะไร

**Large Language Model (LLM)** คือ AI model ที่เชี่ยวชาญด้านการเข้าใจและสร้างภาษามนุษย์ ฝึกด้วยข้อมูล text จำนวนมหาศาล

หลักการพื้นฐาน:
> **Objective ของ LLM คือการทำนาย next token จาก sequence ของ tokens ก่อนหน้า**

LLM คือ **สมองของ Agent** — ทำหน้าที่ตีความคำสั่ง รักษา context วางแผน และตัดสินใจว่าจะใช้ tool ไหน

---

## Transformer Architecture

LLM ส่วนใหญ่ในปัจจุบันสร้างบน **Transformer architecture** ซึ่งใช้ Attention algorithm มีด้วยกัน 3 ประเภท:

| ประเภท | การทำงาน | ตัวอย่าง | Use Cases | ขนาด |
|---|---|---|---|---|
| **Encoder** | รับ text → สร้าง dense embedding | BERT (Google) | Text classification, Semantic search, NER | Millions params |
| **Decoder** | สร้าง tokens ทีละตัวเพื่อต่อ sequence | Llama (Meta) | Text generation, Chatbots, Code generation | Billions params |
| **Seq2Seq** | Encoder + Decoder ทำงานร่วมกัน | T5, BART | Translation, Summarization, Paraphrasing | Millions params |

**LLM ที่ใช้ใน Agent ส่วนใหญ่เป็น Decoder-based** ขนาด Billions parameters

### LLM ที่รู้จักกันดี

| Model | Provider |
|---|---|
| GPT-4 | OpenAI |
| Llama 3 | Meta |
| Deepseek-R1 | DeepSeek |
| Gemma | Google |
| Mistral | Mistral |
| SmolLM2 | Hugging Face |

---

## Tokens และ Tokenization

**Token** คือหน่วยข้อมูลที่ LLM ใช้ทำงาน — ไม่ใช่ word ทั้งคำ แต่เป็น sub-word units

ตัวอย่าง: `"interest"` + `"ing"` → `"interesting"` / `"interest"` + `"ed"` → `"interested"`

- ภาษาอังกฤษมีคำศัพท์ ~600,000 คำ
- แต่ Llama 2 ใช้ vocabulary เพียง ~32,000 tokens

---

## Special Tokens

แต่ละ LLM มี special tokens ที่ใช้แบ่ง structured components เช่น ต้น/ปลาย sequence, message, response

Token ที่สำคัญที่สุดคือ **End of Sequence (EOS)**

| Model | Provider | EOS Token | หน้าที่ |
|---|---|---|---|
| GPT-4 | OpenAI | `<\|endoftext\|>` | End of message text |
| Llama 3 | Meta | `<\|eot_id\|>` | End of sequence |
| Deepseek-R1 | DeepSeek | `<\|end_of_sentence\|>` | End of message text |
| SmolLM2 | Hugging Face | `<\|im_end\|>` | End of instruction/message |
| Gemma | Google | `<end_of_turn>` | End of conversation turn |

---

## การทำงานของ LLM: Autoregressive Decoding

LLM เป็น **autoregressive** — output จาก pass หนึ่งกลายเป็น input สำหรับ pass ถัดไป วนซ้ำจนกว่าจะ predict EOS token

กระบวนการในแต่ละ decoding loop:
1. Input text ถูก tokenize
2. Model คำนวณ representation ของ sequence (position + meaning)
3. Model output scores คะแนนความน่าจะเป็นของทุก token ใน vocabulary
4. เลือก next token ตาม strategy (greedy / beam search / sampling)

---

## Attention: "Attention is All You Need"

ไม่ใช่ทุก word ใน sentence จะสำคัญเท่ากันเมื่อทำนาย next token

ตัวอย่าง: `"The capital of France is ..."` → words ที่สำคัญคือ `"France"` และ `"capital"`

**Attention mechanism** ช่วยให้ model ระบุ words ที่สำคัญที่สุดสำหรับการทำนาย token ถัดไป

**Context length** = จำนวน tokens สูงสุดที่ LLM รับได้และ "attention span" ที่มี

---

## Prompting

Input sequence ที่ส่งให้ LLM เรียกว่า **Prompt** — การออกแบบ prompt ที่ดีช่วยนำ generation ไปในทิศทางที่ต้องการ

---

## การ Train LLM

1. **Pre-training**: ฝึกบน large text dataset ด้วย self-supervised learning — เรียนรู้โครงสร้างภาษาและ patterns
2. **Fine-tuning**: ฝึกต่อบน supervised objective สำหรับ task เฉพาะ เช่น conversational, tool usage, code generation

---

## การใช้ LLM

| วิธี | เหมาะเมื่อ |
|---|---|
| Run Locally | มี hardware เพียงพอ |
| Cloud/API | ใช้ Hugging Face Serverless Inference API หรือ providers อื่น ๆ |

---

## LLM ในบทบาท Agent Brain

LLM เป็น key component ของ Agent ทำหน้าที่:
- ตีความคำสั่งจาก user
- รักษา context ใน conversation
- กำหนดแผนและตัดสินใจว่าจะใช้ tool ไหน

> ดูวิธีที่ LLM รับ tool information ได้ที่ [[13 - Messages, System Prompt และ Chat Templates]]

---

## ดูต่อ

- [[13 - Messages, System Prompt และ Chat Templates]]
- [[14 - Tools: การออกแบบและทำงาน]]
- [[04 - สถาปัตยกรรม Agent: Model + Tools + Orchestration]]

## ตัวอย่าง Implementation จริง

- [[03 Tools/Claude Code/20 - Multi-Provider AI|Multi-Provider AI]] — Claude Code ใช้ Claude เป็น LLM หลัก และอธิบายว่า LLM ต่างเจ้า (GPT-4, Gemini, Claude) communicate กันได้อย่างไรในทางปฏิบัติ
