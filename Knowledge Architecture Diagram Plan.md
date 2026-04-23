---
tags:
  - maintenance
  - diagrams
  - architecture
  - vault-health
type: plan
status: evergreen
source: "vault-local diagram audit"
parent_note: "[[Knowledge Refactor - Task Board]]"
created: "2026-04-19"
updated: ""
---

# Knowledge Architecture Diagram Plan

แผนนี้ใช้ติดตามงานเติม architecture / workflow / decision diagrams ให้ vault ทั้งชุด

เป้าหมาย:
- ทำให้ผู้อ่านเห็นภาพรวมของ vault และแต่ละ domain ได้เร็วขึ้น
- เติม Mermaid เฉพาะจุดที่ช่วยอธิบาย architecture, workflow, loop, lifecycle, decision, หรือ implementation flow
- ไม่เติม diagram ใน raw source, template, หรือ note ที่เป็น checklist/reference สั้น ๆ ถ้าไม่ได้เพิ่มความเข้าใจจริง

---

## Audit Snapshot

ตรวจเมื่อ: `2026-04-19`

- Markdown ทั้งหมด: `235`
- ไฟล์ที่มี Mermaid แล้ว: `92`
- ไฟล์ที่เข้าข่าย architecture/workflow/decision/MOC/use case แต่ยังไม่มี Mermaid: ประมาณ `142`

ข้อสรุป:
- `02 AI Systems/RAG` มี coverage ดีมากแล้วในระดับ concept / architecture notes
- ช่องว่างหลักอยู่ที่หน้า hub, synthesis, use case, และ engineering decision/recipe
- ไม่จำเป็นต้องเติม diagram ทุกไฟล์ที่ match keyword เพราะ raw sources, templates, manifests, README, และ checklist บางไฟล์ไม่คุ้ม

---

## Diagram Standards

ใช้ diagram เมื่อช่วยตอบอย่างน้อยหนึ่งคำถาม:
- ระบบนี้ประกอบด้วย component อะไร
- ข้อมูลหรือ control flow วิ่งอย่างไร
- lifecycle เริ่มและจบตรงไหน
- decision path เลือกทางใดตามเงื่อนไขอะไร
- layer นี้เชื่อมกับ layer อื่นใน vault อย่างไร

รูปแบบที่ควรใช้:
- `flowchart TD` สำหรับ architecture / lifecycle
- `flowchart LR` สำหรับ pipeline หรือ runtime flow
- `sequenceDiagram` สำหรับ protocol / client-server interaction
- decision tree สำหรับ choice / when-to-use notes

ไม่ควรเติม diagram เมื่อ:
- note เป็น raw source / manifest / source record
- note เป็น template
- note เป็น checklist ที่ไม่มี flow
- diagram จะซ้ำกับ note ข้างเคียงโดยไม่เพิ่ม insight

---

## Phase 0 — Vault-Level Overview

สถานะ: `done`

เป้าหมาย: เติมภาพรวมระดับ vault ก่อน เพื่อให้ผู้อ่านรู้ว่าแต่ละ layer อยู่ตรงไหน

| Priority | File | Diagram ที่ควรเพิ่ม | สถานะ |
|---|---|---|---|
| P0 | [[Home]] | Vault Knowledge Architecture: `00 Raw Sources -> 01 Foundations -> 02 AI Systems -> 03 Tools -> 04 Synthesis -> 05 Use Cases -> 06 Engineering` | done |
| P0 | [[index]] | Domain Navigation Graph: foundations, systems, synthesis, use cases, engineering | done |
| P1 | [[Knowledge Topic Registry]] | Topic ownership map: canonical folder -> bridge/use case/engineering links | done |
| P1 | [[Knowledge Folder Structure Plan v2]] | Folder role architecture: Core / Bridge / Application / Reference / Implementation | done |

Acceptance:
- `Home` มีภาพรวม vault layer เดียวที่อ่านแล้วเข้าใจทั้งระบบ
- `index` มี navigation map ไม่ซ้ำกับ `Home` แต่ช่วยเลือก entry point

---

## Phase 1 — Core Domain MOCs

สถานะ: `done`

เป้าหมาย: ทุก MOC หลักควรมี diagram ที่อธิบาย domain architecture หรือ learning path

| Priority | File | Diagram ที่ควรเพิ่ม | สถานะ |
|---|---|---|---|
| P0 | [[02 AI Systems/RAG/RAG - MOC]] | Master RAG Architecture: sources -> ingestion -> indexes -> retrieval/routing -> rerank -> assembly -> generation -> citation -> eval | done |
| P0 | [[02 AI Systems/AI Agent Fundamentals/AI Agent Fundamentals - MOC]] | Agent Architecture Overview: model -> tools -> memory -> planning/orchestration -> actions -> eval/guardrails | done |
| P0 | [[02 AI Systems/MCP/MCP - MOC]] | MCP System Map: host -> client -> server -> tools/resources/prompts -> auth/consent | done |
| P0 | [[02 AI Systems/Guardrails/Guardrails - MOC]] | Guardrails Control Stack: input -> tool safety -> permissions -> output validation -> fallback -> monitoring | done |
| P0 | [[02 AI Systems/Evals/Evals - MOC]] | Evaluation Lifecycle: criteria -> dataset -> judge/human eval -> regression -> observability -> feedback loop | done |
| P0 | [[02 AI Systems/Memory Systems/Memory Systems - MOC]] | Memory System Architecture: working memory -> episodic/semantic/procedural -> read/write policy -> retrieval -> failure modes | done |
| P1 | [[02 AI Systems/Agent Frameworks/Agent Frameworks - MOC]] | Framework Selection Map: framework landscape -> state/memory -> tools -> observability -> checkpointing | done |
| P1 | [[03 Tools/Claude Code/Claude Code - Multi-Agent MOC]] | Claude Code Multi-Agent Workflow Map: session -> subagents -> tools/worktrees -> permissions -> error handling | done |
| P1 | [[04 Synthesis/Synthesis - MOC]] | Synthesis Layer Map: bridge notes vs decision notes and their upstream/downstream links | done |
| P1 | [[05 Use Cases/Use Cases - MOC]] | Use Case Navigation Map: application paths vs decision paths | done |
| P1 | [[06 Engineering/Engineering - MOC]] | Implementation Layer Map: architecture -> frameworks -> RAG -> guardrails -> evals -> MCP -> memory -> patterns -> recipes | done |

Acceptance:
- MOC diagram ต้องเป็นภาพรวมของ domain ไม่ใช่ซ้ำกับ leaf note
- ทุก diagram ต้องชี้ว่า domain เชื่อมกับ MOC อื่นตรงไหน

---

## Phase 2 — Engineering Implementation Diagrams

สถานะ: `done`

เป้าหมาย: เติม decision tree และ implementation pipeline ให้ notes ที่ใช้ลงมือทำจริง

| Priority | File | Diagram ที่ควรเพิ่ม | สถานะ |
|---|---|---|---|
| P0 | [[06 Engineering/RAG/Recipe - Build a RAG Pipeline]] | Implementation pipeline: connector -> parser -> chunker -> metadata validator -> embedder -> index writer -> retrieval API -> answer service | done |
| P0 | [[06 Engineering/RAG/Decision - Choose a Retrieval Strategy]] | Retrieval strategy decision tree: exact / semantic / multi-source / long docs / relationship-heavy / agentic | done |
| P0 | [[06 Engineering/Architecture to Code/Architecture to Code - MOC]] | Architecture-to-implementation flow: concept -> component -> contract -> runtime -> eval -> runbook | done |
| P0 | [[06 Engineering/Evals/Recipe - Build an Eval Harness]] | Eval harness architecture: dataset -> runner -> model/system -> scorer -> report -> regression gate | done |
| P0 | [[06 Engineering/Guardrails/Recipe - Add Output Validation]] | Validation boundary flow: schema -> semantic validation -> policy -> fallback -> logging | done |
| P0 | [[06 Engineering/MCP/Recipe - Add MCP Server Integration]] | MCP integration sequence: host/client -> server discovery -> tool call -> auth -> result handling | done |
| P0 | [[06 Engineering/Memory/Recipe - Add a Memory Layer]] | Memory read/write pipeline: observe -> salience -> write policy -> store -> retrieve -> assemble | done |
| P1 | [[06 Engineering/Decisions/Decision - Choose a Framework]] | Framework selection decision tree | done |
| P1 | [[06 Engineering/Evals/Decision - Choose an Evaluation Gate]] | Evaluation gate placement decision flow | done |
| P1 | [[06 Engineering/Guardrails/Decision - Choose a Validation Boundary]] | Validation boundary placement diagram | done |
| P1 | [[06 Engineering/MCP/Decision - Choose MCP Integration Boundary]] | MCP boundary decision tree | done |
| P1 | [[06 Engineering/Memory/Decision - Choose a Memory Policy]] | Memory policy decision tree | done |

Acceptance:
- Decision notes ต้องมี decision tree ที่ใช้เลือกทางได้จริง
- Recipe notes ต้องมี pipeline ที่เอาไป implement เป็น task list ได้

---

## Phase 3 — Synthesis and Use Case Diagrams

สถานะ: `done`

เป้าหมาย: เติม comparison map และ decision flow ให้ notes ที่ใช้คิดเชิงกลยุทธ์

| Priority | File | Diagram ที่ควรเพิ่ม | สถานะ |
|---|---|---|---|
| P0 | [[04 Synthesis/Bridge/Synthesis - Agent Runtime Layers]] | Runtime layer stack | done |
| P0 | [[04 Synthesis/Bridge/Synthesis - LLM to Agent Stack]] | Progression: LLM -> tool-use -> workflow -> agent -> multi-agent | done |
| P0 | [[04 Synthesis/Bridge/Synthesis - Memory vs RAG vs Context]] | Comparison map: context / RAG / memory responsibilities | done |
| P0 | [[04 Synthesis/Decision/Synthesis - Agent vs Workflow vs RAG]] | Decision tree: use RAG / workflow / agent / hybrid | done |
| P0 | [[04 Synthesis/Decision/Synthesis - Prompting vs Fine-tuning vs RAG]] | Intervention choice diagram | done |
| P1 | [[04 Synthesis/Bridge/Synthesis - Multi-Agent Failure Modes]] | Failure propagation map across agents | done |
| P1 | [[04 Synthesis/Bridge/Synthesis - Single to Multi-Agent Infrastructure]] | Migration path from single agent to multi-agent infra | done |
| P1 | [[05 Use Cases/Application/Use Cases - Build an AI Agent]] | End-to-end agent build flow | done |
| P1 | [[05 Use Cases/Application/Use Cases - Design a RAG System]] | Practical RAG design flow | done |
| P1 | [[05 Use Cases/Application/Use Cases - Design Guardrails for Tool Use]] | Tool safety control flow | done |
| P1 | [[05 Use Cases/Application/Use Cases - Design Memory for an AI Agent]] | Memory design flow | done |
| P1 | [[05 Use Cases/Application/Use Cases - Evaluate an AI Agent]] | Agent evaluation workflow | done |
| P1 | [[05 Use Cases/Decision/Use Cases - When to Use an Agent]] | Agent/no-agent decision tree | done |
| P1 | [[05 Use Cases/Decision/Use Cases - Move from Single to Multi-Agent]] | Migration flow | done |

Acceptance:
- Synthesis diagrams ต้องช่วยเปรียบเทียบ ไม่ใช่แค่ restate headings
- Use case diagrams ต้องเป็น practical flow ที่ผู้อ่านทำตามได้

---

## Phase 4 — Foundations MOC and Learning Path Diagrams

สถานะ: `done`

เป้าหมาย: เติมภาพรวมให้ foundations hubs ที่ยังไม่มี master diagram

| Priority | File | Diagram ที่ควรเพิ่ม | สถานะ |
|---|---|---|---|
| P1 | [[01 Foundations/LLM Foundations/LLM Foundations - MOC]] | Model lifecycle map: data -> pretraining -> post-training -> inference -> serving -> eval | done |
| P1 | [[01 Foundations/Context Windows/Context Windows - MOC]] | Context architecture: prompt -> retrieved context -> memory/history -> tool results -> output | done |
| P1 | [[01 Foundations/Prompt Engineering/Prompt Engineering - MOC]] | Prompt lifecycle: intent -> instructions -> context -> constraints -> output format -> eval | done |
| P1 | [[01 Foundations/Tokenizer in AI/Tokenizer in AI - MOC]] | Tokenizer learning path: text -> normalization -> tokenization -> ids -> context/cost impact | done |

Acceptance:
- MOC diagram ต้องเป็น learning map ไม่ใช่รายละเอียดซ้ำกับ leaf note

---

## Phase 5 — Tooling and Claude Code Workflow Diagrams

สถานะ: `done`

เป้าหมาย: เติม workflow diagrams ให้ Claude Code notes ที่เป็น workflow หรือ multi-agent operations

| Priority | File | Diagram ที่ควรเพิ่ม | สถานะ |
|---|---|---|---|
| P1 | [[03 Tools/Claude Code/Workflow/04 - 1 Session vs Subagents vs Agent Teams]] | Workflow comparison: single session / subagents / agent team | done |
| P1 | [[03 Tools/Claude Code/Workflow/17 - Agent Tool]] | Agent tool lifecycle | done |
| P1 | [[03 Tools/Claude Code/Workflow/18 - Git Worktree]] | Worktree-based parallel workflow | done |
| P1 | [[03 Tools/Claude Code/Workflow/19 - วิธีเริ่ม Agent Team]] | Start-agent-team flow | done |
| P1 | [[03 Tools/Claude Code/Workflow/22 - Error Handling]] | Error handling / retry / fallback flow | done |
| P2 | [[03 Tools/Claude Code/Reference/09 - Permissions และ Settings]] | Permission boundary map | done |
| P2 | [[03 Tools/Claude Code/Reference/11 - โครงสร้างโฟลเดอร์ .claude]] | `.claude` folder structure diagram | done |
| P2 | [[03 Tools/Claude Code/Reference/14 - Built-in Subagents]] | Subagent selection map | done |

Acceptance:
- Tooling diagrams ต้อง mark ว่า content เป็น version-sensitive เมื่อผูกกับ behavior เฉพาะ release/config

---

## Skip List

ไม่ต้องเติม diagram ก่อน เว้นแต่มีเหตุเฉพาะ:
- `00 Raw Sources/**`
- `_Templates/**`
- `CLAUDE.md`
- `AGENTS.md`
- `README.md`
- `Knowledge Topic Audit.md`
- `Knowledge Refactor - Task Board.md`
- `Knowledge Folder Structure Plan v2.md` ยกเว้น phase 0 diagram
- `Knowledge Topic Registry.md` ยกเว้น phase 0 diagram
- source manifests / source records / digest notes
- notes ที่เป็น short checklist หรือ reference table ล้วน

---

## Work Order

1. ทำ Phase 0 ก่อน เพื่อให้ vault-level navigation เห็นภาพรวม — done
2. ทำ Phase 1 ต่อ เพื่อให้ทุก domain hub มี architecture map — done
3. ทำ Phase 2 ต่อ เพื่อให้ implementation layer ใช้ทำงานจริงได้ — done
4. ทำ Phase 3 ต่อ เพื่อให้ synthesis/use case ใช้ decision ได้ดีขึ้น — done
5. ทำ Phase 4 และ 5 ต่อเมื่อ diagram coverage ของ hubs/engineering ดีแล้ว — done

---

## Validation Checklist

หลังเติม diagram แต่ละรอบให้ตรวจ:
- Mermaid syntax อ่านง่ายและไม่ซับซ้อนเกิน
- diagram ไม่ซ้ำกับ diagram ใน note ใกล้เคียง
- diagram มี label ชัดและใช้ศัพท์ตรงกับ note
- ถ้าเป็น MOC ต้องช่วยนำทางไป notes ลูก
- ถ้าเป็น decision note ต้องช่วยเลือกทาง
- ถ้าเป็น recipe ต้องช่วยลงมือ implement
- `git diff --check` ผ่าน
