---
tags:
  - usecase
  - agents
  - frameworks
type: usecase
status: evergreen
source: ""
parent_note: "[[Home]]"
---

# Use Cases - Choose an Agent Framework

## Summary

การเลือก agent framework ที่ดีไม่ใช่การถามว่า framework ไหนดัง แต่คือการ map use case ของเราเข้ากับ runtime needs จริง เช่น orchestration, state, memory, observability, และ human approval

รายละเอียด framework landscape, framework-vs-custom, state, tool orchestration, observability, และ checkpointing อยู่ใน canonical notes ของ `Agent Frameworks` และ `06 Engineering` แล้ว

---

## ใช้เมื่อไร

ใช้ note นี้เมื่อ:
- กำลังตัดสินใจว่าจะใช้ framework หรือ custom build
- ต้องเลือกแนว graph, actor, kernel, หรือ process-oriented
- อยากคุยกับ agent ให้ชัดว่า requirement ของระบบคืออะไร

---

## Step 1: นิยาม use case ก่อน

ตอบคำถาม 5 ข้อนี้ก่อน:
- งานเป็น single-agent หรือ multi-agent
- workflow deterministic หรือ open-ended
- ต้องมี state / checkpoints / resume หรือไม่
- ต้องมี human approval หรือไม่
- ต้องมี tools และ external systems มากแค่ไหน

ถ้ายังตอบไม่ได้ อย่าเพิ่งเลือก framework

---

## Step 2: เลือกจาก runtime needs

### ถ้าต้องการ explicit orchestration สูง

ให้เอนทาง graph-oriented frameworks

### ถ้าต้องการ distributed multi-agent communication

ให้เอนทาง actor/message-oriented frameworks

### ถ้าต้องการ plugin-centric enterprise integration

ให้เอนทาง kernel-centric frameworks

### ถ้าต้องการ task/team processes ชัด

ให้เอนทาง process-oriented frameworks

---

## Step 3: ถามเรื่อง state and memory

framework จะเหมาะหรือไม่ขึ้นกับคำถามพวกนี้:
- state ถูกเก็บที่ไหน
- resume execution ได้หรือไม่
- checkpoint มีไหม
- external memory ต่อได้ไหม
- observability พอไหม

ถ้าตอบไม่ได้ แปลว่ายังเลือกเร็วเกินไป

---

## Step 4: ถามเรื่อง control vs speed

### เลือก framework เมื่อ

- ต้องการประกอบระบบเร็ว
- orchestration complexity สูง
- ต้องการ runtime primitives สำเร็จรูป

### เลือก custom build เมื่อ

- problem เล็กและชัด
- abstraction ของ framework หนักเกินไป
- ต้องการ control สูงมาก

---

## Heuristic แบบเร็ว

| สถานการณ์ | แนวทางที่มักเหมาะ |
|---|---|
| prototype เร็ว, task ตรงไปตรงมา | custom หรือ framework เบา |
| long-running workflow with checkpoints | graph-oriented framework |
| multi-agent messaging / delegation | actor/message-oriented framework |
| enterprise plugins / service integration | kernel-centric framework |
| role-based task orchestration | process/team-oriented framework |

---

## Anti-Patterns

- เลือกจากกระแสอย่างเดียว
- เลือกจาก demo โดยไม่ดู state model
- ใช้ framework หนักเกิน use case
- เขียนเองหมดทั้งที่ต้องการ features ระดับ runtime เยอะ

---

## สิ่งที่ควรถาม agent เวลาให้ช่วยเลือก

- ระบบนี้มี state แบบไหน
- ต้อง resume ได้ไหม
- ต้องใช้ tools กี่ class
- มี high-risk actions ไหม
- ต้อง trace / debug ระดับไหน
- team รับ abstraction overhead ของ framework นี้ได้ไหม

---

## Recommended Reading

1. [[02 AI Systems/Agent Frameworks/Core/01 - Landscape]]
2. [[02 AI Systems/Agent Frameworks/Core/02 - Framework vs Custom Build]]
3. [[02 AI Systems/Agent Frameworks/Core/03 - State and Memory]]
4. [[02 AI Systems/Agent Frameworks/Core/04 - Tool Orchestration]]
5. [[02 AI Systems/Guardrails/Core/03 - Tool Safety]]

---

## Cross Links

- [[02 AI Systems/Agent Frameworks/Agent Frameworks - MOC]]
- [[02 AI Systems/Agent Frameworks/Core/01 - Landscape]]
- [[02 AI Systems/Agent Frameworks/Core/02 - Framework vs Custom Build]]
- [[02 AI Systems/Agent Frameworks/Core/03 - State and Memory]]
- [[02 AI Systems/Agent Frameworks/Core/04 - Tool Orchestration]]
- [[Home]]
