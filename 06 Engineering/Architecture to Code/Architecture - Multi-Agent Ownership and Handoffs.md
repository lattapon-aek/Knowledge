---
tags:
  - engineering
  - architecture
  - multi-agent
  - ownership
  - handoff
  - state
  - version-sensitive
  - derived
type: note
status: evergreen
source: "https://platform.openai.com/docs/guides/agent-builder-safety · https://platform.openai.com/docs/guides/trace-grading · https://docs.langchain.com/oss/javascript/langgraph/persistence · https://docs.langchain.com/oss/javascript/langchain/human-in-the-loop · https://microsoft.github.io/autogen/stable/user-guide/core-user-guide/design-patterns/group-chat.html · https://docs.crewai.com/en/concepts/flows"
parent_note: "[[06 Engineering/Architecture to Code/Architecture to Code - MOC]]"
---

# Architecture - Multi-Agent Ownership and Handoffs

## ภาพรวม

ระบบ multi-agent ต้องมีโมเดลความเป็นเจ้าของที่ชัดเจน ทุกครั้งที่มี handoff ควรตอบให้ได้ 3 เรื่อง:
- ตอนนี้ใครเป็นเจ้าของงาน
- state อะไรถูกส่งต่อไป
- จะสื่อว่างานเสร็จหรือให้ escalate อย่างไร

ถ้าไม่มีคำตอบพวกนี้ การ delegate จะกำกวม และ debug workflow ได้ยากขึ้นมาก

---

## โมเดลความเป็นเจ้าของ

### 1. Orchestrator เป็นเจ้าของ workflow

Orchestrator หรือ manager ต้องรับผิดชอบเรื่อง:
- การ route งาน
- เงื่อนไขการหยุด
- นโยบาย retry / escalate
- state ของ workflow โดยรวม
- traceability ของ run

OpenAI Agent Builder มอง agent เป็น workflow ที่ประกอบด้วย agent, tool และ control-flow logic ดังนั้นความเป็นเจ้าของของ workflow จึงแยกจากความเป็นเจ้าของของ specialist แต่ละตัว

### 2. Specialist ควรรับผิดชอบงานย่อยที่แคบ

แต่ละ specialist ควรมีขอบเขตงานที่ชัดและจำกัด เช่น:
- ดึง evidence
- ร่างเนื้อหา
- ตรวจ output
- ตรวจ policy
- สรุป state

ถ้า specialist รับผิดชอบกว้างเกินไป handoff จะรก และการ recover จะยากขึ้น

### 3. ต้องระบุ owner ของ state ให้ชัด

state ควรมีรูปแบบความเป็นเจ้าของอย่างใดอย่างหนึ่ง:
- shared state ที่ orchestrator เป็นเจ้าของ
- agent-local state ที่ส่งต่อผ่าน handoff payload อย่างชัดเจน
- persisted checkpoint state ที่ผูกกับ thread / run identity

LangGraph persistence ใช้ checkpoint ที่ผูกกับ threads และ workflow ที่มี human-in-the-loop ต้องทำให้ state inspect และ resume ได้

---

## ข้อตกลงของ Handoff

ทุก handoff ควรกำหนดให้ชัด:
- agent ต้นทาง
- agent ปลายทาง
- task id
- state payload
- รูปแบบผลลัพธ์ที่คาดหวัง
- เกณฑ์ความสำเร็จ
- เกณฑ์สำหรับ escalate

ถ้าเป็น handoff แบบ async ให้กำหนดเพิ่มด้วย:
- retry policy
- idempotency key
- timeout
- dead-letter behavior

---

## รูปแบบของ Handoff

### Controller ไป Specialist

Controller เป็นคนตัดสินใจว่าใครควรทำงานถัดไป

ใช้เมื่อ:
- flow ส่วนใหญ่เป็นแบบ sequential
- ต้องการคุมงานให้แน่น
- ต้องการ debug ให้ง่าย

AutoGen group chat ใช้ manager agent เพื่อเลือก speaker ถัดไป และ manager ยังเป็นผู้คุมลำดับเสมอ

### Handoff แบบอิง State

ส่งงานต่อเมื่อ state ผ่านเงื่อนไขที่กำหนดแล้ว

ใช้เมื่อ:
- งานควรเดินต่อได้ก็ต่อเมื่อเงื่อนไขชัดเจน
- workflow มีหลาย phase
- agent ถัดไปอ่านจาก persisted state แล้วทำงานต่อได้

### Shared Topic หรือ Shared Thread

ให้ agent หลายตัว subscribe topic หรือ thread เดียวกัน แล้วสลับกันทำงาน

ใช้เมื่อ:
- การร่วมมือสำคัญกว่าการตอบแบบ request/response แบบเข้ม
- ทีมต้องมี context ร่วมกัน
- ยอมรับการผลัด turn ตามบทบาทได้

CrewAI Flows และ Tasks/Processes มี primitives สำหรับ orchestration แบบ stateful ที่เข้ากับรูปแบบนี้

---

## กติกาของ State Schema

- ต้อง version state schema
- แยก transient state ออกจาก long-term memory
- ทำให้ handoff payload กระชับและมีโครงสร้าง
- ใส่ provenance ของ state ที่มาจาก tools หรือ retrieval
- ห้ามใส่ secrets ลงใน shared handoff payload

---

## กติกาความปลอดภัยและขอบเขต

- กำหนดให้ชัดว่า agent ตัวไหนเป็น read-only
- กำหนดให้ชัดว่า agent ตัวไหนเรียก tool ที่มี side effect ได้
- ใช้ approval gate เมื่อจำเป็น
- แยก tool ความเสี่ยงสูงออกจาก input ที่เชื่อถือได้น้อย
- ถือว่า prompt injection สามารถไหลผ่าน tool output ได้ถ้าไม่กรอง

แนวทางด้านความปลอดภัยของ OpenAI มอง untrusted text และ tool path เป็น boundary ด้าน security โดยตรง

---

## Checklist การลงมือทำ

ก่อนเขียน workflow:
1. กำหนดบทบาทของ orchestrator
2. กำหนดขอบเขตของ specialist แต่ละตัว
3. กำหนด schema ของ handoff payload
4. กำหนดว่าใครเป็นเจ้าของ state
5. กำหนดพฤติกรรม resume และ interrupt
6. กำหนดสิทธิ์ของ tools
7. กำหนดฟิลด์สำหรับ trace logging
8. กำหนดเกณฑ์ retry และ escalate

---

## หลักออกแบบ

- อย่า delegate โดยไม่มี handoff contract
- อย่า persist state โดยไม่มี owner
- อย่าให้ message payload กลายเป็นข้อมูลดิบที่ไร้โครงสร้าง
- อย่าใช้ shared state แทน routing ที่ไม่ชัด
- อย่าให้ handoff ลบ provenance ทิ้ง

---

## ลิงก์ที่เกี่ยวข้อง

- [[04 Synthesis/Bridge/Synthesis - Single to Multi-Agent Infrastructure]]
- [[04 Synthesis/Bridge/Synthesis - Multi-Agent Failure Modes]]
- [[06 Engineering/Architecture to Code/Architecture - Multi-Agent Infrastructure]]
- [[06 Engineering/Architecture to Code/Architecture - Multi-Agent Security and Permissions]]
- [[06 Engineering/Architecture to Code/Architecture - Multi-Agent Deployment and Topology]]
- [[06 Engineering/Patterns/Pattern - Sync vs Async Agent Communication]]
- [[02 AI Systems/Agent Frameworks/Core/07 - Checkpointing and Resumability]]
- [[02 AI Systems/MCP/MCP - MOC]]
- [[Home]]

---

## แหล่งอ้างอิง

- OpenAI Agents / Agent Builder: https://platform.openai.com/docs/guides/agent-builder
- OpenAI Safety in Building Agents: https://platform.openai.com/docs/guides/agent-builder-safety
- OpenAI Trace Grading: https://platform.openai.com/docs/guides/trace-grading
- LangGraph Persistence: https://docs.langchain.com/oss/javascript/langgraph/persistence
- LangGraph HITL: https://docs.langchain.com/oss/javascript/langchain/human-in-the-loop
- AutoGen Group Chat: https://microsoft.github.io/autogen/stable/user-guide/core-user-guide/design-patterns/group-chat.html
- CrewAI Flows: https://docs.crewai.com/en/concepts/flows
