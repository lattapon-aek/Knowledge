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
- ทำให้ `01 Foundations` เป็น canonical home ของ LLM / prompt / context primitives
- ทำให้ `MCP` เป็น canonical home ของ protocol layer สำหรับ tools, resources, prompts, client features, และ security/consent
- ให้ `AI Agent Fundamentals/12, 13, 14` เป็น bridge notes สำหรับ agent-facing runtime เท่านั้น
- ทำให้ `Agent Frameworks` เป็น canonical home ของ framework selection และ framework-level tradeoffs
- ทำให้ `Memory Systems` เป็น canonical home ของ memory architecture และ memory policy
- ทำให้ `RAG` เป็น canonical home ของ retrieval pipeline, grounding, และ RAG evaluation
- ทำให้ `Guardrails` เป็น canonical home ของ control layer และ safety boundaries
- ทำให้ `Evals` เป็น canonical home ของ evaluation layer
- ทำให้ `Use Cases` เป็น canonical home ของ decision paths และ application examples

### Deduplication ที่ทำแล้ว

- ย่อ notes bridge ด้าน memory / RAG / context
- ย่อ notes bridge ด้าน prompting / fine-tuning / RAG
- ย่อ notes bridge ด้าน agent vs workflow / RAG
- ย่อ notes bridge ด้าน runtime layers และ LLM-to-agent stack
- ย่อ notes bridge ด้าน memory retrieval vs RAG และ memory / RAG / context
- ย่อ notes bridge ด้าน agent runtime layers และ LLM-to-agent stack ให้เป็น pointer เท่านั้น
- ย่อ `AI Agent Fundamentals` หลายหน้าให้เหลือ concept สำคัญ
- ย่อ `Agent Frameworks - Landscape` และ `Framework vs Custom Build`
- ปิดฝั่ง `06 Engineering` ทั้งชุดแล้ว รวม `Frameworks`, `Architecture to Code`, `Recipes`, `Decisions`, `Evals`, `Guardrails`, `Memory`, `MCP`, `Patterns`, และ `Project Notes`
- ปิดฝั่ง `MCP` core + client + security notes เป็น evergreen แล้ว

### Style cleanup

- ปรับหลายหน้าให้ไทย-first
- ลด presentation English ที่เกินจำเป็น
- คง technical terms และ mermaid diagram ไว้

---

## Archive / Watchlist

ไม่มีงาน refactor หลักค้างอยู่แล้วในรอบนี้

หัวข้อนี้เก็บไว้เป็นรายการตรวจสอบสำหรับรอบถัดไปเท่านั้น

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
- ปิดเป็น volatile/reference layer แล้ว
- note หลักถูกยกเป็น `evergreen` ครบแล้ว

### 6. `02 AI Systems/MCP`

สถานะ:
- ปิด core, client, และ security notes เป็น evergreen แล้ว
- protocol layer พร้อมใช้อ่านต่อจาก `AI Agent Fundamentals` และ `06 Engineering`

---

## Working Rules

- ถ้า topic เดียวมีหลายหน้า ให้เลือกหน้า canonical ก่อน
- หน้าที่เหลือเป็น bridge, link, หรือ support note
- ถ้าจะตัด ต้องตัดเฉพาะส่วนที่ซ้ำจริง
- ถ้ามี mermaid หรือ diagram ให้เก็บไว้
- ถ้าเป็น fact ที่อ้าง source ควรรักษา provenance

---

## Suggested Next Steps

1. เก็บไว้ใช้เป็น checklist ตอนจะ re-categorize vault ใหม่
2. ถ้ากลับมาทำ refactor อีก ให้เริ่มจาก `Agent Frameworks` กับ `06 Engineering`
3. ใช้ `Future Re-categorization Plan` เป็นแผนกลางสำหรับการจัดหมวดใหม่ทั้ง vault

---

## Future Re-categorization Plan

ใช้แผนนี้เมื่อจะจัดหมวดใหม่ทั้ง vault:

### 0. Topic Registry

- `Knowledge Topic Registry.md` ถูกสร้างแล้วเป็นแผนที่กลางของ vault
- ใช้เป็นรายการว่า topic หลักแต่ละเรื่องควรอยู่ folder ไหน / note ไหนเป็น canonical / note ไหนเป็น bridge
- topic registry จะเป็น source เดียวสำหรับตรวจ ownership ของเรื่องสำคัญก่อนย้ายหรือแตกหมวดใหม่

### 1. Re-categorization Order

ใช้ลำดับนี้เป็นงานหลักของ phase ใหม่:

0. `Foundations / base primitives`
1. `Agent runtime`
2. `Framework selection`
3. `Memory architecture`
4. `Retrieval / RAG`
5. `Guardrails / control`
6. `Evaluation`
7. `Use case decisions`
8. `Bridge / synthesis`
9. `Implementation`
10. `Claude Code / tooling`

## Core Folder Layout

```
Knowledge/
├── 00 Raw Sources/
├── 01 Foundations/
├── 02 AI Systems/
├── 03 Tools/
├── 04 Synthesis/
├── 05 Use Cases/
├── 06 Engineering/
├── _Templates/
├── Home.md
├── index.md
├── AGENTS.md
└── README.md
```

### หน้าที่ของแต่ละ Folder

- `00 Raw Sources` = แหล่งข้อมูลดิบ / digest / source records
- `01 Foundations` = concept base ที่นิ่งที่สุด
- `02 AI Systems` = agent runtime, protocol, memory, RAG, guardrails, evals
- `03 Tools` = volatile tooling knowledge
- `04 Synthesis` = bridge / comparison / decision synthesis
- `05 Use Cases` = decision paths และ application examples
- `06 Engineering` = implementation, recipes, decisions, project notes
- `_Templates` = template สำหรับโน้ตใหม่
- `Home.md` = landing page หลัก
- `index.md` = catalog กลาง
- `AGENTS.md` = instructions สำหรับ agent
- `README.md` = documentation สำหรับคนอ่าน GitHub

### 1. Foundations

- `01 Foundations` = LLM / prompt / context / token / evaluation primitives
- หน้าที่ของหมวดนี้คือเป็นฐาน concept ที่นิ่งที่สุด

### 2. Agent Runtime

- `02 AI Systems/AI Agent Fundamentals` = agent loop, runtime, orchestration
- `02 AI Systems/Agent Frameworks` = framework selection และ runtime tradeoffs

### 3. Protocol and Tooling

- `02 AI Systems/MCP` = protocol layer สำหรับ tools, resources, prompts
- `03 Tools/Claude Code` = volatile tool/reference layer

### 4. Retrieval, Memory, Safety, Evaluation

- `Memory Systems` = memory architecture and policy
- `RAG` = retrieval pipeline and grounding
- `Guardrails` = control layer
- `Evals` = evaluation layer

### 5. Application and Implementation

- `05 Use Cases` = decision paths / application examples
- `06 Engineering` = implementation, recipes, decisions, project notes

### 6. Bridge Layer

- `04 Synthesis` = comparison, bridge, and decision synthesis

### Re-categorization Rules

- ถ้าหัวข้ออยู่ได้มากกว่า 1 หมวด ให้เลือก canonical home ก่อน
- ถ้าเป็นความรู้พื้นฐานที่ใช้หลายที่ ให้คงไว้ใน `01 Foundations`
- ถ้าเป็น runtime behavior ของ agent ให้ไป `02 AI Systems`
- ถ้าเป็นวิธีทำงานจริงหรือ code-level detail ให้ไป `06 Engineering`
- ถ้าเป็นตัวอย่างใช้งานจริงหรือ decision path ให้ไป `05 Use Cases`
- ถ้าเป็น bridge ระหว่างหมวด ให้ไป `04 Synthesis`
