---
tags:
  - engineering
  - architecture
  - multi-agent
  - security
  - permissions
  - guardrails
  - version-sensitive
  - derived
type: note
status: evergreen
source: "https://developers.openai.com/api/docs/guides/agent-builder-safety · https://platform.openai.com/docs/guides/agent-builder · https://platform.openai.com/docs/guides/trace-grading"
parent_note: "[[06 Engineering/Architecture to Code/Architecture to Code - MOC]]"
---

# Architecture - Multi-Agent Security and Permissions

## ภาพรวม

ความปลอดภัยของ multi-agent คือปัญหาเรื่อง trust boundary เป็นหลัก ยิ่งมี agent, tool, หรือ handoff เพิ่มขึ้น ช่องทางที่ untrusted input จะกระทบพฤติกรรมของระบบก็ยิ่งมากขึ้น ค่าเริ่มต้นที่ปลอดภัยคือใช้ least privilege ต่อ agent, ทำ handoff แบบมีโครงสร้าง, มี approval สำหรับ side effect, และแยกเส้นทาง read / write / human review ให้ trace ได้ชัด

---

## โมเดลความเสี่ยง

ให้ถือว่าของต่อไปนี้เป็น untrusted จนกว่าจะ validate ได้ชัด:
- user input
- tool output
- retrieved documents
- downstream agent output
- ข้อมูลจาก MCP / connector

แนวทางด้าน safety ของ OpenAI ระบุชัดว่า prompt injection เกิดขึ้นเมื่อ untrusted text หรือ data เข้าสู่ AI system แล้วพยายาม override instruction ของระบบ แนวทางเดียวกันยังชี้ว่าการแชร์ context หรือ privilege มากเกินไปทำให้เกิดความเสี่ยงเรื่อง private data leakage ได้

---

## โมเดลสิทธิ์

### 1. Agent ที่อ่านอย่างเดียว (Read-only)

ใช้สำหรับ:
- retrieval
- summarization
- classification
- evidence collection

กติกา:
- ห้ามมี side effect
- ห้ามเขียนข้อมูลออกไปภายนอก
- ห้ามเข้าถึง secrets
- output ควรเป็น structured

### 2. Agent ที่เขียนได้ (Write-capable)

ใช้สำหรับ:
- state updates
- tool calls ที่มีผลภายนอก
- การสร้าง content ที่จะกลายเป็น input ของขั้นถัดไป

กติกา:
- ใช้ tool เท่าที่จำเป็น
- ใช้เฉพาะ input ที่ validate แล้ว
- ทุก write ต้อง trace ได้

### 3. Agent ที่ต้องผ่าน approval (Approval-gated)

ใช้สำหรับ:
- payments
- actions ที่ย้อนกลับไม่ได้
- changes ฝั่ง production
- privileged MCP operations

แนวทางของ OpenAI ระบุชัดว่าให้เปิด tool approvals ไว้ และใช้ human approval node ใน Agent Builder เพื่อให้ผู้ใช้ตรวจและยืนยันแต่ละ operation ได้ รวมถึงทั้ง read และ write

### 4. สิทธิ์เฉพาะ Orchestrator

สงวนไว้สำหรับ:
- routing decisions
- escalation policy
- state ownership
- approval routing
- final handoff validation

วิธีนี้ช่วยแยก control logic ออกจากงานของ specialist ให้ชัด

---

## กติกาขอบเขต

- ห้ามใส่ตัวแปรที่ยังไม่ผ่านการเชื่อถือ (untrusted) ลงใน developer messages โดยตรง
- ส่ง input ที่ยังไม่ผ่านการเชื่อถือผ่าน user message หรือ structured field ที่ validate แล้วเท่านั้น
- ใช้ enum หรือ fixed schema แทน freeform text ระหว่าง agent
- ห้ามปล่อยให้ raw retrieved text เป็นตัวสั่ง tool call โดยไม่กรอง
- ห้ามใส่ secrets ลงใน shared handoff payload
- ห้ามส่ง privilege เกินกว่าที่ step ต้นทางต้องใช้ไปยัง agent ปลายทาง

OpenAI แนะนำให้ใช้ structured outputs เพื่อควบคุม data flow และลดพื้นที่เสี่ยงของ injection

---

## ความปลอดภัยของ Handoff

ทุก handoff ควรมีแค่:
- task id
- allowed next action
- bounded evidence
- validated state snapshot
- explicit completion criteria

ห้าม handoff:
- raw secrets
- arbitrary freeform tool output
- unbounded conversation history
- implementation details the next agent does not need

ถ้า agent หนึ่งประมวลผล untrusted text แล้ว agent ถัดไปเอาผลลัพธ์นั้นไปใช้ ต้อง sanitize ก่อน handoff จุดนี้คือจุดที่ multi-agent systems มักเริ่มเปราะ แม้ตัวแรกจะดูปลอดภัย

---

## ชั้นของ Guardrail

ให้ใช้ชั้นเหล่านี้ร่วมกัน:

1. ตรวจสอบ input
2. ใช้ structured outputs
3. จำกัดสิทธิ์ตาม scope
4. ขอ human approval เมื่อมี side effect
5. เก็บ trace logging
6. ทำ eval กับ trace ที่มีความเสี่ยง

OpenAI แนะนำ guardrails สำหรับ user input, tool approvals สำหรับ MCP operations, และ trace graders / evals สำหรับจับความผิดพลาดของพฤติกรรม agent

---

## Checklist การลงมือทำ

ก่อนปล่อย multi-agent workflow:
1. ระบุให้ชัดว่า agent ตัวไหนเป็น agent ที่อ่านอย่างเดียว
2. ระบุว่า agent ตัวไหนเขียน state ได้
3. ระบุว่า agent ตัวไหนเรียก tool ที่มี side effect ได้
4. ระบุจุดที่ต้องมี human approval
5. กำหนด structured handoff payload ให้ชัด
6. กำหนดว่าอะไรห้ามออกจาก trust boundary
7. เก็บ trace ให้พอ reconstruct การตัดสินใจได้
8. ทดสอบเส้นทาง prompt injection และ handoff ที่ไม่ปลอดภัย

---

## หลักออกแบบ

- ต้องถือว่า prompt injection สามารถเดินทางผ่าน tool output ได้
- แยกเส้นทาง high-trust กับ low-trust ออกจากกัน
- จำกัด permission ตามบทบาท ไม่ใช่ตามความสะดวก
- บังคับ approval เมื่อ action นั้นย้อนกลับไม่ได้อย่างปลอดภัย
- ทำให้ privilege escalation ทุกครั้งเป็นเรื่องที่ชัดเจน

---

## ลิงก์ที่เกี่ยวข้อง

- [[04 Synthesis/Bridge/Synthesis - Multi-Agent Failure Modes]]
- [[06 Engineering/Architecture to Code/Architecture - Multi-Agent Ownership and Handoffs]]
- [[06 Engineering/Patterns/Pattern - Sync vs Async Agent Communication]]
- [[02 AI Systems/Guardrails/Guardrails - MOC]]
- [[02 AI Systems/Evals/Application/09 - Multi-Agent Evals]]
- [[02 AI Systems/MCP/MCP - MOC]]
- [[Home]]

---

## แหล่งอ้างอิง

- OpenAI Safety in Building Agents: https://developers.openai.com/api/docs/guides/agent-builder-safety
- OpenAI Agent Builder: https://platform.openai.com/docs/guides/agent-builder
- OpenAI Trace Grading: https://platform.openai.com/docs/guides/trace-grading
