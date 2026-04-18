---
tags:
  - usecase
  - memory
  - agents
type: usecase
status: evergreen
source: ""
parent_note: "[[05 Use Cases/Use Cases - MOC]]"
---

# Use Cases - Design Memory for an AI Agent

## Summary

ใช้ note นี้เมื่อกำลังตัดสินใจว่า agent ควรมี memory แบบไหน, อ่านเมื่อไร, เขียนเมื่อไร, และอะไรควรเป็น memory แทนที่จะเป็น RAG หรือ context ธรรมดา

รายละเอียด memory architecture, taxonomy, policy, และ failure modes อยู่ใน `Memory Systems` แล้ว note นี้เป็นเพียง decision path สำหรับเลือก memory boundary

## Canonical Notes

- [[02 AI Systems/Memory Systems/Memory Systems - MOC]]
- [[04 Synthesis/Synthesis - Memory vs RAG vs Context]]
- [[04 Synthesis/Synthesis - Memory in Agents]]

---

## ใช้เมื่อไร

ใช้ note นี้เมื่อ:
- agent ต้องจำข้อมูลข้าม session
- ระบบต้อง personalize ตามประวัติผู้ใช้
- ต้องแยก session state ออกจาก durable memory
- ต้องตัดสินใจว่าเรื่องไหนควรเป็น memory, RAG, หรือ context

---

## Step 1: นิยาม memory need ก่อน

ตอบคำถามเหล่านี้:
- ต้องจำอะไรข้ามเวลา
- ข้อมูลนั้นเปลี่ยนบ่อยไหม
- มี owner หรือ scope ชัดไหม
- ถ้าจำผิดจะเสียหายแค่ไหน
- retrieval ต้องเร็วและ deterministic แค่ไหน

---

## Step 2: แยก memory types

โดยทั่วไปให้แยก:
- working memory สำหรับ current task
- episodic memory สำหรับ past interactions
- semantic memory สำหรับ stable facts/preferences
- procedural memory สำหรับ instructions or learned routines

---

## Step 3: ออกแบบ read/write policies

ต้องตอบให้ได้ว่า:
- เขียน memory เมื่อไร
- เขียนโดยใครหรือ component ไหน
- ต้องผ่าน validation หรือ approval ไหม
- อ่าน memory เมื่อไร
- จะป้องกัน stale, duplicated, หรือ over-personalized memory อย่างไร

---

## Step 4: แยก memory ออกจาก RAG

ใช้ memory เมื่อ:
- เป็นข้อมูลเฉพาะ user, session, หรือ history

ใช้ RAG เมื่อ:
- เป็น knowledge base ที่กว้างกว่า user
- ต้องการ grounded retrieval จาก documents

ใช้ context เมื่อ:
- เป็นข้อมูลเฉพาะงานปัจจุบันที่ยังไม่ควรถูกเก็บถาวร

---

## Heuristic แบบเร็ว

| สถานการณ์ | แนวทางที่มักเหมาะ |
|---|---|
| ข้อมูลชั่วคราวของงานปัจจุบัน | working memory / context |
| ความชอบของผู้ใช้ที่เสถียร | semantic memory |
| ประวัติการกระทำหรือบทสนทนา | episodic memory |
| ขั้นตอนการทำงานที่ควร reuse | procedural memory |
| ความรู้จาก documents จำนวนมาก | RAG |

---

## Anti-Patterns

- เขียนทุกอย่างลง memory
- ใช้ memory แทน RAG ทั้งหมด
- ไม่มี retention policy
- ไม่มี scope isolation ระหว่าง users
- ไม่มี evaluation สำหรับ memory failures

---

## Recommended Reading

1. [[02 AI Systems/Memory Systems/Core/01 - Working Memory vs Long-Term Memory]]
2. [[02 AI Systems/Memory Systems/Core/02 - Episodic vs Semantic vs Procedural Memory]]
3. [[02 AI Systems/Memory Systems/Core/03 - Memory Read and Write Policies]]
4. [[02 AI Systems/Memory Systems/Application/04 - Agent Memory Patterns]]
5. [[02 AI Systems/Memory Systems/Application/05 - Memory Failure Modes]]
6. [[04 Synthesis/Synthesis - Memory vs RAG vs Context]]
7. [[04 Synthesis/Synthesis - Memory in Agents]]
8. [[02 AI Systems/Agent Frameworks/Core/03 - State and Memory]]

---

## Cross Links

- [[02 AI Systems/Memory Systems/Memory Systems - MOC]]
- [[02 AI Systems/RAG/RAG - MOC]]
- [[05 Use Cases/Use Cases - Build an AI Agent]]
- [[Home]]
