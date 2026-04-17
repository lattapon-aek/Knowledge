---
tags:
  - refactor
  - task-board
  - maintenance
type: guide
status: evergreen
source: "vault-local task board"
parent_note: "[[Home]]"
---

# Knowledge Refactor - Task Board

ใช้หน้านี้เป็นแผนงานสำหรับ refactor vault โดยยึดหลัก:

- ไม่เปลี่ยนความหมาย
- ไม่แตะ mermaid/diagram
- ตัดเฉพาะเนื้อหาที่ซ้ำจริง
- ให้แต่ละ topic มี canonical note เดียว

---

## ทำแล้ว

### Vault governance

- ตั้ง `feature/knowledge-dedupe` เป็น branch งาน refactor
- สร้าง task board กลางสำหรับแผน refactor
- แยกบทบาท `Home`, `index`, `AGENTS.md`, และ `06 Engineering` ให้ชัด

### Canonical boundaries

- ทำให้ `AI Agent Fundamentals` เป็น learning path หลักของ agent basics
- ทำให้ `04 Synthesis` เป็น bridge / comparison / decision layer
- ทำให้ `06 Engineering` เป็น implementation layer
- ทำให้ `03 Tools/Claude Code` เป็น volatile layer

### Deduplication ที่ทำแล้ว

- ย่อ notes bridge ด้าน memory / RAG / context
- ย่อ notes bridge ด้าน prompting / fine-tuning / RAG
- ย่อ notes bridge ด้าน agent vs workflow / RAG
- ย่อ notes bridge ด้าน runtime layers และ LLM-to-agent stack
- ย่อ `AI Agent Fundamentals` หลายหน้าให้เหลือ concept สำคัญ
- ย่อ `Agent Frameworks - Landscape` และ `Framework vs Custom Build`
- ปิดฝั่ง `06 Engineering` ทั้งชุดแล้ว รวม `Frameworks`, `Architecture to Code`, `Recipes`, `Decisions`, `Evals`, `Guardrails`, `Memory`, `MCP`, `Patterns`, และ `Project Notes`

### Style cleanup

- ปรับหลายหน้าให้ไทย-first
- ลด presentation English ที่เกินจำเป็น
- คง technical terms และ mermaid diagram ไว้

---

## คงเหลือ

### 1. `02 AI Systems/Agent Frameworks`

โฟกัส:
- `Core/03 - State and Memory`
- `Core/04 - Tool Orchestration`
- `Core/06 - Evaluation and Observability`
- `Core/07 - Checkpointing and Resumability`

งานที่ต้องดู:
- ลด prose ที่ซ้ำกับ `06 Engineering/Frameworks`
- คงตาราง, diagram, และ framework-specific comparisons ไว้
- แยกให้ชัดว่าอะไรเป็น concept level และอะไรเป็น implementation level

### 2. `02 AI Systems/Memory Systems` และ `02 AI Systems/RAG`

โฟกัส:
- policy / taxonomy / retrieval / context assembly / agentic RAG

งานที่ต้องดู:
- ตรวจซ้ำระหว่าง memory, RAG, และ remaining synthesis notes
- ยังคง canonical notes ที่เป็นฐานความรู้ไว้ครบ

### 3. `02 AI Systems/Guardrails` และ `02 AI Systems/Evals`

โฟกัส:
- input/output controls
- safety / validation / permission / fallback
- success criteria / benchmark / judge / regression

งานที่ต้องดู:
- ลดการอธิบายที่ซ้ำกับ synthesis notes
- คง control/eval primitives ไว้ครบ

### 4. `05 Use Cases`

โฟกัส:
- decision paths
- practical application

งานที่ต้องดู:
- ตัดซ้ำกับ synthesis เมื่อเป็นแค่ decision bridge
- คง use case examples ที่ช่วยนำไปใช้จริง

### 5. `03 Tools/Claude Code`

สถานะ:
- ตั้งใจให้เป็น volatile/reference layer
- ยังไม่ใช่เป้าหมายหลักของ refactor ชุดนี้

---

## Working Rules

- ถ้า topic เดียวมีหลายหน้า ให้เลือกหน้า canonical ก่อน
- หน้าที่เหลือเป็น bridge, link, หรือ support note
- ถ้าจะตัด ต้องตัดเฉพาะส่วนที่ซ้ำจริง
- ถ้ามี mermaid หรือ diagram ให้เก็บไว้
- ถ้าเป็น fact ที่อ้าง source ควรรักษา provenance

---

## Suggested Next Steps

1. ตรวจ `Memory Systems` / `RAG` / `Guardrails` / `Evals` รอบสุดท้าย
2. ค่อย sweep `05 Use Cases` ถ้ายังมี bridge ที่ซ้ำ
3. เก็บ `03 Tools/Claude Code` ถ้าต้องการลด volatile overlap ในรอบถัดไป
