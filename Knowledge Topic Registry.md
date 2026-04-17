---
tags:
  - registry
  - topic-map
  - maintenance
type: guide
status: evergreen
source: "vault-local topic registry"
parent_note: "[[Home]]"
---

# Knowledge Topic Registry

ใช้หน้านี้เป็นแผนที่กลางของ vault เวลาจะจัดหมวดใหม่หรือเช็กว่า topic หลักควรอยู่ตรงไหน

## วิธีใช้

- อ่านตารางนี้ก่อนถ้าจะเพิ่ม topic ใหม่
- ถ้า topic เดียวมีหลาย note ให้เลือก canonical note จากตารางนี้ก่อน
- ใช้ bridge notes เฉพาะตอนต้องเชื่อมข้ามหมวด

## Core Topics

| Topic | Canonical Folder | Canonical Note | Bridge / Entry Notes |
|---|---|---|---|
| LLM foundations | `01 Foundations/LLM Foundations` | `LLM Foundations - MOC` | `01 Foundations/LLM Foundations/12 - LLM พื้นฐาน` |
| Prompt design | `01 Foundations/Prompt Engineering` | `Prompt Engineering - MOC` | `01 Foundations/Prompt Engineering/13 - Messages, System Prompt และ Chat Templates` |
| Context engineering | `01 Foundations/Context Windows` | `Context Windows - MOC` | `01 Foundations/Prompt Engineering/13 - Messages, System Prompt และ Chat Templates` |
| Tokenization | `01 Foundations/Tokenizer in AI` | `Tokenizer in AI - MOC` | `LLM Foundations` links |
| Weights / context / retrieval / tools | `04 Synthesis` | `Synthesis - Weights, Context, Retrieval และ Tools` | `01 Foundations/LLM Foundations/04 - Inference, Context และ RAG`, `01 Foundations/Prompt Engineering/07 - Structured Generation และ Output Formats`, `02 AI Systems/RAG/RAG - MOC`, `02 AI Systems/MCP/MCP - MOC` |
| Agent runtime | `02 AI Systems/AI Agent Fundamentals` | `AI Agent Fundamentals - MOC` | `05 Use Cases/Use Cases - Build an AI Agent` |
| Workflow vs AI Agent | `04 Synthesis` | `Synthesis - Workflow vs AI Agent` | `02 AI Systems/AI Agent Fundamentals` bridge |
| When to use an agent | `05 Use Cases` | `Use Cases - When to Use an Agent` | `04 Synthesis/Synthesis - Workflow vs AI Agent` |
| Framework selection | `02 AI Systems/Agent Frameworks` | `Agent Frameworks - MOC` | `06 Engineering/Frameworks/*`, `05 Use Cases/Use Cases - Choose an Agent Framework` |
| MCP / protocol layer | `02 AI Systems/MCP` | `MCP - MOC` | `02 AI Systems/MCP/14 - Tools: การออกแบบและทำงาน` |
| Memory architecture | `02 AI Systems/Memory Systems` | `Memory Systems - MOC` | `04 Synthesis/Synthesis - Memory in Agents`, `05 Use Cases/Use Cases - Design Memory for an AI Agent` |
| Retrieval / RAG | `02 AI Systems/RAG` | `RAG - MOC` | `04 Synthesis/Synthesis - Memory vs RAG vs Context`, `05 Use Cases/Use Cases - Design a RAG System` |
| Guardrails / control | `02 AI Systems/Guardrails` | `Guardrails - MOC` | `05 Use Cases/Use Cases - Design Guardrails for Tool Use` |
| Evaluation | `02 AI Systems/Evals` | `Evals - MOC` | `05 Use Cases/Use Cases - Evaluate an AI Agent` |
| Bridge / synthesis | `04 Synthesis` | `Synthesis - MOC` | comparison / decision bridge notes |
| Use case decisions | `05 Use Cases` | `Use Cases - MOC` | application examples and decision paths |
| Implementation | `06 Engineering` | `Engineering - MOC` | framework, recipe, decision, project notes |
| Claude Code / tooling | `03 Tools/Claude Code` | `Claude Code - Multi-Agent MOC` | volatile tool-specific notes |

## Core Subtopics

ใช้ตารางนี้เมื่อ topic ใหญ่แตกย่อยแล้ว แต่ยังอยากคุมเจ้าของหลักให้ชัด

| Subtopic | Canonical Home | Canonical Note / Entry |
|---|---|---|
| Agent loop / runtime basics | `02 AI Systems/AI Agent Fundamentals` | `AI Agent Fundamentals - MOC` |
| Workflow / decision bridge | `04 Synthesis` | `Synthesis - Workflow vs AI Agent` |
| Agent use decision | `05 Use Cases` | `Use Cases - When to Use an Agent` |
| Runtime messages / system prompt / templates | `02 AI Systems/AI Agent Fundamentals` | `13 - Messages, System Prompt และ Chat Templates` |
| Tool runtime contract | `02 AI Systems/AI Agent Fundamentals` + `06 Engineering` | `14 - Tools: การออกแบบและทำงาน` / `Architecture - Tool Schemas and Runtime Integration` |
| State / memory / checkpointing | `02 AI Systems/Agent Frameworks` | `03 - State and Memory`, `07 - Checkpointing and Resumability` |
| Tool orchestration | `02 AI Systems/Agent Frameworks` | `04 - Tool Orchestration` |
| Evaluation / observability / trace grading | `02 AI Systems/Agent Frameworks` + `02 AI Systems/Evals` | `06 - Evaluation and Observability` / `Evals - MOC` |
| Multi-agent infrastructure | `04 Synthesis` + `06 Engineering` | `Synthesis - Single to Multi-Agent Infrastructure` / `Architecture - Multi-Agent Infrastructure` |
| Multi-agent handoffs / ownership | `06 Engineering` | `Architecture - Multi-Agent Ownership and Handoffs` |
| Multi-agent security / permissions | `06 Engineering` | `Architecture - Multi-Agent Security and Permissions` |
| Multi-agent deployment / topology | `06 Engineering` | `Architecture - Multi-Agent Deployment and Topology` |
| Prompt anatomy / patterns | `01 Foundations/Prompt Engineering` | `Prompt Engineering - MOC` |
| Context budget / caching / long-context | `01 Foundations/Context Windows` | `Context Windows - MOC` |
| Tokenization / tokenizer behavior | `01 Foundations/Tokenizer in AI` | `Tokenizer in AI - MOC` |
| LLM theory / inference / evaluation primitives | `01 Foundations/LLM Foundations` | `LLM Foundations - MOC` |
| Retrieval / grounding / RAG eval | `02 AI Systems/RAG` | `RAG - MOC` |
| Memory policy / long-term recall | `02 AI Systems/Memory Systems` | `Memory Systems - MOC` |
| Guardrails / safety controls | `02 AI Systems/Guardrails` | `Guardrails - MOC` |
| Use-case decisions | `05 Use Cases` | `Use Cases - MOC` |
| Bridge / synthesis | `04 Synthesis` | `Synthesis - MOC` |
| Volatile tool reference | `03 Tools/Claude Code` | `Claude Code - Multi-Agent MOC` |

## Re-categorization Order

ใช้ลำดับนี้เวลาจะเริ่มจัดหมวดใหม่ทั้ง vault

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

## Folder Map

- `00 Raw Sources` = raw inputs / source records
- `01 Foundations` = stable primitives
- `02 AI Systems` = agent/runtime/system topics
- `03 Tools` = volatile tooling reference
- `04 Synthesis` = cross-topic bridge
- `05 Use Cases` = decision and application paths
- `06 Engineering` = implementation layer

## Notes

- ถ้า topic ไม่ชัดว่าอยู่หมวดไหน ให้เริ่มจาก canonical note ในตารางนี้
- ถ้าเป็นเรื่องใหม่ที่ยังไม่รู้ตำแหน่ง ให้เก็บใน `draft` ก่อน แล้วค่อยย้ายเมื่อเจ้าของ topic ชัด
- ถ้าเป็นเนื้อหาที่มีหลายมุม ให้เลือก home ที่นิ่งที่สุด แล้วใช้ bridge note เป็นทางเข้า
