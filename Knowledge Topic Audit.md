---
tags:
  - audit
  - topic-map
  - maintenance
type: guide
status: evergreen
source: "vault-local topic audit"
parent_note: "[[Knowledge Topic Registry]]"
---

# Knowledge Topic Audit

หน้านี้ใช้เป็น audit matrix ระดับ topic เพื่อช่วยจัดหมวด vault ใหม่โดยไม่แตะเนื้อหาเดิม

หลักการ:
- ไม่ย้ายหรือ rewrite เนื้อหาในรอบนี้
- เลือก canonical owner ให้แต่ละ topic มีเจ้าของหลักเพียงตัวเดียว
- ถ้า topic ซ้อนกัน ให้หน้าอื่นเป็น bridge / entry / implementation note แทน

---

## Core Ownership Map

| Topic | Canonical Home | Canonical Owner | Bridge / Entry Notes | หมายเหตุ |
|---|---|---|---|---|
| LLM primitives | `01 Foundations/LLM Foundations` | `LLM Foundations - MOC` | `AI Agent Fundamentals/12 - LLM พื้นฐาน` | theory base |
| Prompt design | `01 Foundations/Prompt Engineering` | `Prompt Engineering - MOC` | `AI Agent Fundamentals/13 - Messages, System Prompt และ Chat Templates` | prompt theory |
| Context engineering | `01 Foundations/Context Windows` | `Context Windows - MOC` | `AI Agent Fundamentals/13 - Messages, System Prompt และ Chat Templates` | context budget / caching |
| Tokenization | `01 Foundations/Tokenizer in AI` | `Tokenizer in AI - MOC` | `LLM Foundations` links | stable primitive |
| Agent runtime | `02 AI Systems/AI Agent Fundamentals` | `AI Agent Fundamentals - MOC` | `05 Use Cases/Use Cases - Build an AI Agent` | runtime owner |
| Framework selection | `02 AI Systems/Agent Frameworks` | `Agent Frameworks - MOC` | `06 Engineering/Frameworks/*`, `05 Use Cases/Use Cases - Choose an Agent Framework` | selection owner |
| MCP / protocol layer | `02 AI Systems/MCP` | `MCP - MOC` | `AI Agent Fundamentals/14 - Tools: การออกแบบและทำงาน` | protocol owner |
| Memory architecture | `02 AI Systems/Memory Systems` | `Memory Systems - MOC` | `04 Synthesis/Synthesis - Memory in Agents`, `05 Use Cases/Use Cases - Design Memory for an AI Agent` | memory owner |
| Retrieval / RAG | `02 AI Systems/RAG` | `RAG - MOC` | `04 Synthesis/Synthesis - Memory vs RAG vs Context`, `05 Use Cases/Use Cases - Design a RAG System` | retrieval owner |
| Guardrails / control | `02 AI Systems/Guardrails` | `Guardrails - MOC` | `05 Use Cases/Use Cases - Design Guardrails for Tool Use` | control owner |
| Evaluation | `02 AI Systems/Evals` | `Evals - MOC` | `05 Use Cases/Use Cases - Evaluate an AI Agent` | measurement owner |
| Bridge / synthesis | `04 Synthesis` | `Synthesis - MOC` | comparison / decision bridge notes | cross-topic layer |
| Use case decisions | `05 Use Cases` | `Use Cases - MOC` | application examples and decision paths | decision layer |
| Implementation | `06 Engineering` | `Engineering - MOC` | framework, recipe, decision, project notes | code / runtime implementation |
| Claude Code / tooling | `03 Tools/Claude Code` | `Claude Code - Multi-Agent MOC` | volatile tool-specific notes | volatile layer |

---

## Boundary Map

### 1. Foundations

- `01 Foundations` เป็นเจ้าของของ LLM, prompt, context, tokenizer, และ evaluation primitives
- ถ้าเนื้อหาเป็น theory ที่นิ่งและใช้ซ้ำได้ ให้เก็บที่นี่

### 2. Agent Runtime

- `02 AI Systems/AI Agent Fundamentals` เป็นเจ้าของของ agent loop, runtime architecture, และ decision ว่าเมื่อไรควรใช้ agent
- `12`, `13`, `14` ในหมวดนี้เป็น bridge notes ไปยัง Foundations และ Engineering

### 3. Framework vs Implementation

- `02 AI Systems/Agent Frameworks` เป็นเจ้าของของ framework selection และ runtime tradeoffs
- `06 Engineering` เป็นเจ้าของของ code, recipe, framework-specific implementation, และ project-specific detail

### 4. Memory vs Retrieval

- `Memory Systems` เป็นเจ้าของของ memory architecture, taxonomy, read/write policy
- `RAG` เป็นเจ้าของของ retrieval pipeline, chunking, reranking, grounding, และ evaluation

### 5. Control vs Measurement

- `Guardrails` เป็นเจ้าของของ policy, validation, fallback, permission, monitoring
- `Evals` เป็นเจ้าของของ benchmark, judge, regression, human review, observability

### 6. Bridge vs Decision vs Implementation

- `04 Synthesis` = bridge / compare / decision synthesis
- `05 Use Cases` = decision path / application example
- `06 Engineering` = implementation / recipe / project note

### 7. Tooling

- `03 Tools/Claude Code` = volatile tool reference
- ถ้าเป็น concept หลัก ให้กลับไป canonical owner ก่อนเสมอ

---

## Overlap Rules

- ถ้า topic เดียวมีหลายหน้า ให้เลือก canonical home หนึ่งหน้า แล้วหน้าอื่นเป็น bridge
- ถ้าเป็น comparison ข้ามหลาย topic ให้ไป `04 Synthesis`
- ถ้าเป็นวิธีใช้จริง ให้ไป `05 Use Cases`
- ถ้าเป็น implementation detail ให้ไป `06 Engineering`
- ถ้าเป็นเรื่องอธิบายพื้นฐาน ให้ไป `01 Foundations` หรือ `02 AI Systems` ตาม owner ของ topic นั้น

---

## Suggested Audit Priority

1. `01 Foundations`
2. `02 AI Systems/AI Agent Fundamentals`
3. `02 AI Systems/Agent Frameworks`
4. `02 AI Systems/Memory Systems`
5. `02 AI Systems/RAG`
6. `02 AI Systems/Guardrails`
7. `02 AI Systems/Evals`
8. `02 AI Systems/MCP`
9. `04 Synthesis`
10. `05 Use Cases`
11. `06 Engineering`
12. `03 Tools/Claude Code`

---

## Use With Registry

- อ่านหน้านี้คู่กับ `Knowledge Topic Registry`
- ใช้ Registry เป็นแผนที่ owner
- ใช้ Audit นี้เป็น checklist ว่า topic ไหนควร stay, bridge, หรือ move

