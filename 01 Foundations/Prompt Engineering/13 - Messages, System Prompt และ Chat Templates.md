---
tags:
  - llm
  - system-prompt
  - chat-template
  - messages
type: note
status: evergreen
source: "HuggingFace Agents Course — Unit 1 \"Messages and Special Tokens\" (huggingface.co/learn/agents-course/unit1)"
parent_note: "[[Prompt Engineering - MOC]]"
---

# Messages, System Prompt และ Chat Templates



---

## ภาพรวม

โน้ตนี้โฟกัสที่ runtime layer ของ agent: วิธีแพ็ก messages, system prompt, และ chat templates ให้ model เข้าใจ conversation ได้ถูกต้อง  
ถ้าต้องการหลักการเขียน prompt หรือ prompt anatomy แบบทั่วไป ให้ดู `Prompt Engineering`  
ถ้าต้องการเรื่อง context budget และ context engineering ให้ดู `Context Windows`

เมื่อผู้ใช้คุยกับ Agent ผ่าน chat interface สิ่งที่เกิดขึ้นเบื้องหลัง:

> Messages หลายรายการถูก **concatenate และ format** เป็น single prompt ก่อนส่งให้ LLM ทุกครั้ง — model ไม่ได้ "จำ" การสนทนา แต่อ่านทั้งหมดในครั้งเดียว

**Chat Templates** คือสะพานระหว่าง conversational messages (user/assistant turns) กับ formatting ที่ LLM แต่ละตัวต้องการ

---

## 3 ประเภทของ Messages

### 1. System Message (System Prompt)

กำหนด **พฤติกรรมของ model** — เป็น persistent instructions ที่ส่งผลต่อทุก interaction

```python
system_message = {
    "role": "system",
    "content": "You are a professional customer service agent. Always be polite, clear, and helpful."
}
```

**บทบาทของ System Message ใน Agent:**
- บอก behavior ของ agent
- ระบุ instructions สำคัญ เช่น tools ที่ใช้ได้ และรูปแบบ output
- กำหนด guardrails และ persona ของระบบ

> รายละเอียดเชิง runtime layer และ tool contract ดูที่ [[02 AI Systems/MCP/14 - Tools: การออกแบบและทำงาน|14 - Tools: การออกแบบและทำงาน]]

### 2. User Messages

ข้อความจากผู้ใช้

```python
{"role": "user", "content": "I need help with my order"}
```

### 3. Assistant Messages

ข้อความจาก LLM/Agent

```python
{"role": "assistant", "content": "I'd be happy to help. Could you provide your order number?"}
```

---

## Conversation Structure

```python
conversation = [
    {"role": "user", "content": "I need help with my order"},
    {"role": "assistant", "content": "I'd be happy to help. Could you provide your order number?"},
    {"role": "user", "content": "It's ORDER-123"},
]
```

ทุก message ถูก concatenate เป็น single prompt — chat template แปลงรูปแบบนี้ให้ LLM เข้าใจได้

---

## Chat Templates

### ทำไมต้องมี Chat Templates

แต่ละ LLM ใช้ special tokens และ formatting rules ต่างกัน — chat template รับประกันว่า prompt ถูก format ถูกต้องสำหรับ model นั้น ๆ

### ตัวอย่าง: SmolLM2 vs Llama 3.2

บทสนทนาเดียวกัน output ต่างกัน:

**SmolLM2:**
```
system
You are a helpful AI assistant named SmolLM, trained by Hugging Face
user
I need help with my order
assistant
I'd be happy to help. Could you provide your order number?
user
It's ORDER-123
assistant
```

**Llama 3.2:** ใช้ special delimiter tokens แตกต่างออกไป (`<|begin_of_text|>`, `<|eot_id|>`, ฯลฯ)

### ChatML Format

มาตรฐานที่ใช้กันกว้างขวาง — จัด conversation ด้วย role indicators ชัดเจน (system, user, assistant)

---

## การใช้ apply_chat_template()

วิธีที่ง่ายที่สุดในการ format prompt ให้ถูกต้อง:

```python
from transformers import AutoTokenizer

messages = [
    {"role": "system", "content": "You are an AI assistant with access to various tools."},
    {"role": "user", "content": "Hi!"},
    {"role": "assistant", "content": "Hi human, what can I help you with?"},
]

tokenizer = AutoTokenizer.from_pretrained("HuggingFaceTB/SmolLM2-1.7B-Instruct")
rendered_prompt = tokenizer.apply_chat_template(messages, tokenize=False, add_generation_prompt=True)
```

`rendered_prompt` พร้อมส่งเข้า model ได้ทันที

---

## บทบาทของ System Prompt ใน Agent Loop

เมื่อ agent ทำงาน system prompt มีความสำคัญมาก เพราะ:

1. **Tool descriptions ถูก inject เข้าไปที่นี่** — LLM รู้จัก tools ผ่าน text ใน system prompt
2. **TAO cycle instructions** ถูก embed ไว้ใน system prompt — กำหนดว่า agent ต้องคิด-ทำ-สังเกตอย่างไร
3. **Behavior guidelines** กำหนด personality และข้อจำกัดของ agent

ถ้าต้องการหลักการออกแบบ prompt โดยรวม ให้ดู [[01 Foundations/Prompt Engineering/Prompt Engineering - MOC|Prompt Engineering - MOC]]

> System prompt คือ "คู่มือการทำงาน" ของ agent ที่ถูกอ่านทุกครั้งที่ LLM ประมวลผล

---

## ดูต่อ

- [[01 Foundations/LLM Foundations/12 - LLM พื้นฐาน|12 - LLM พื้นฐาน]]
- [[02 AI Systems/MCP/14 - Tools: การออกแบบและทำงาน|14 - Tools: การออกแบบและทำงาน]]
- [[06 - วงจร Thought-Action-Observation (TAO)]]
- [[01 Foundations/Prompt Engineering/Prompt Engineering - MOC|Prompt Engineering - MOC]]
- [[01 Foundations/Context Windows/Context Windows - MOC|Context Windows - MOC]]

## ตัวอย่าง Implementation จริง

- [[03 Tools/Claude Code/12 - CLAUDE File|CLAUDE.md]] — CLAUDE.md คือ system-level memory ของ Claude Code ที่ inject บริบทโปรเจกต์, กฎ, และ context ให้ทุก agent อ่านอัตโนมัติ
