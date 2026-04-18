---
tags:
  - llm
  - transformer
  - foundation
type: note
status: evergreen
source: "HuggingFace Agents Course — Unit 1 \"What are LLMs?\" (huggingface.co/learn/agents-course/unit1)"
parent_note: "[[LLM Foundations - MOC]]"
---

# LLM พื้นฐาน

---

## ขอบเขตของโน้ตนี้

โน้ตนี้เป็น bridge note สำหรับ `LLM Foundations` / agent-facing summary:
- ไม่ได้อธิบาย LLM theory แบบเต็ม
- ทำหน้าที่บอกว่า agent designer ต้องรู้ LLM แค่ส่วนไหน
- รายละเอียด model basics อยู่ที่ `01 Foundations/LLM Foundations`

## สิ่งที่ agent designer ต้องรู้เกี่ยวกับ LLM

| เรื่อง | อยู่ที่ไหน |
|---|---|
| LLM คืออะไร, tokenization, transformer, decoding, training, embeddings, evaluation | [[01 Foundations/LLM Foundations/LLM Foundations - MOC|LLM Foundations - MOC]] |
| Prompt anatomy, patterns, structured output | [[01 Foundations/Prompt Engineering/Prompt Engineering - MOC|Prompt Engineering - MOC]] |
| Context budget, context rot, caching, long-context trade-offs | [[01 Foundations/Context Windows/Context Windows - MOC|Context Windows - MOC]] |
| System prompt / messages / chat templates ใน runtime | [[01 Foundations/Prompt Engineering/Bridge/13 - Messages, System Prompt และ Chat Templates|13 - Messages, System Prompt และ Chat Templates]] |
| Tool schemas / tool calling / MCP runtime contract | [[02 AI Systems/MCP/Bridge/14 - Tools: การออกแบบและทำงาน|14 - Tools: การออกแบบและทำงาน]] |

## LLM ในบทบาท Agent Brain

LLM คือ core model ที่ agent ใช้เพื่อ:
- ตีความคำสั่ง
- รักษา context
- reason / plan
- ตัดสินใจว่าจะใช้ tool ไหน
- ประมวลผลผลลัพธ์จาก tool แล้วตอบกลับ

ถ้าต้องการรายละเอียด theory เต็ม ให้ไปอ่าน `LLM Foundations` ก่อน แล้วค่อยกลับมาดูโน้ตนี้ในมุม agent runtime

## ดูต่อ

- [[01 Foundations/LLM Foundations/LLM Foundations - MOC|LLM Foundations - MOC]]
- [[01 Foundations/Prompt Engineering/Bridge/13 - Messages, System Prompt และ Chat Templates|13 - Messages, System Prompt และ Chat Templates]]
- [[02 AI Systems/MCP/Bridge/14 - Tools: การออกแบบและทำงาน|14 - Tools: การออกแบบและทำงาน]]
- [[04 - สถาปัตยกรรม Agent: Model + Tools + Orchestration]]
