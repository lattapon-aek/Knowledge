---
tags:
  - ingest
  - plan
  - sources
type: guide
status: evergreen
source: ""
parent_note: "[[00 Raw Sources/Raw Sources - MOC]]"
created: "2026-04-20"
updated: "2026-04-20"
---

# 2026-04 New Sources - Ingest Plan

แผน ingest สำหรับ 4 แหล่งข้อมูลใหม่ที่ประเมินแล้ว

---

## หลักการ Ingest รอบนี้

> **เสริมลึก ไม่ทับเดิม**

- ทุก task ต้องอ่าน note ปลายทางก่อนเขียน เพื่อเข้าใจน้ำเสียง โครงสร้าง และ claims ที่มีอยู่
- ถ้าเนื้อหาใหม่ซ้ำกับของเดิม → ไม่เพิ่ม
- ถ้าเนื้อหาใหม่ขยายความลึกของของเดิม → merge เป็น section ใหม่ใน note เดิม
- ถ้าเนื้อหาใหม่เป็นมุมที่ต่างออกไปจริง ๆ → สร้าง note ใหม่ แต่ต้องลิงก์กลับ note เดิมให้ชัด
- ห้ามเปลี่ยนข้อสรุปเดิมโดยไม่ระบุเหตุผลและ source
- ห้ามเพิ่ม claim ที่ไม่มี source รองรับ
- ถ้าเป็น architectural inference ต้องระบุให้ชัดว่าเป็น inference

---

## แหล่งข้อมูลที่ประเมิน

| # | Source | ประเภท | URL |
|---|---|---|---|
| S1 | RAG-Anything (HKUDS) | Framework + Paper | https://github.com/HKUDS/RAG-Anything |
| S2 | Dive into Claude Code (arxiv 2604.14228) | Academic paper | https://arxiv.org/abs/2604.14228 |
| S3 | ai-engineering-from-scratch (rohitg00) | Curriculum/Course | https://github.com/rohitg00/ai-engineering-from-scratch |
| S4 | llm-engineer-toolkit (KalyanKS-NLP) | Curated library list | https://github.com/KalyanKS-NLP/llm-engineer-toolkit |

---

## ลำดับความสำคัญ

| ลำดับ | Source | ความสำคัญ | เหตุผล |
|---|---|---|---|
| 🥇 | S2 — Dive into Claude Code | สูงมาก | architectural depth ที่ vault ยังขาด: design principles, permission model, context compaction, future directions |
| 🥈 | S1 — RAG-Anything | สูง | เติม Multimodal RAG ที่เป็น gap ชัดเจน + cross-modal knowledge graph |
| 🥉 | S4 — llm-engineer-toolkit | กลาง-ต่ำ | ใช้ update landscape/catalog ได้ ไม่มี depth |
| 4 | S3 — ai-engineering-from-scratch | ต่ำ | นอก scope หลักของ vault, เนื้อหาที่ overlap vault มีลึกกว่าแล้ว |

---

## Phase 1: S2 — Dive into Claude Code (arxiv 2604.14228)

### Gap Analysis — เทียบกับ notes ที่มี

**`01 - Claude Code คืออะไร`** — อธิบาย CLI tool, agentic loop, tools พื้นฐาน, เปรียบเทียบ Chat vs CLI
→ paper เสริมได้: while-loop core เป็นเรื่องเดียวกับ agentic loop แต่ paper ให้ detail ว่า "most code lives in systems around this loop" ซึ่ง note เดิมยังไม่มี

**`03 - Orchestrator Pattern`** — อธิบาย Subagents vs Agent Teams, mailbox, parallel
→ paper เสริมได้: subagent delegation mechanism + worktree isolation + append-oriented session storage เป็น implementation detail ที่ลึกกว่า

**`09 - Permissions และ Settings`** — อธิบาย settings scope hierarchy, allow/deny rules, pattern syntax
→ paper เสริมได้: permission system มี 7 modes + ML-based classifier ซึ่ง note เดิมยังไม่มี detail ระดับนี้

**ยังไม่มีใน vault เลย:**
- 5 human values / 13 design principles ที่ขับเคลื่อน architecture
- context compaction pipeline 5 layers
- extensibility mechanisms เป็นภาพรวม (MCP, plugins, skills, hooks)
- comparative architecture กับ agent system อื่น (OpenClaw)
- 6 open design directions

### Ingest Tasks

| # | งาน | ปลายทาง | วิธี | รายละเอียด |
|---|---|---|---|---|
| 1.1 | Source Record | `00 Raw Sources/Source Records/` | สร้างใหม่ | ลงทะเบียน paper |
| 1.2 | เสริม `01 - Claude Code คืออะไร` | `03 Tools/Claude Code/Core/01` | **merge section** | เพิ่ม section "Architecture Overview" ใต้เนื้อหาเดิม — อธิบายว่า core คือ while-loop แต่ complexity อยู่ที่ systems รอบ loop (permission, compaction, extensibility, session storage) พร้อม source citation ไม่แก้เนื้อหาเดิม |
| 1.3 | เสริม `09 - Permissions และ Settings` | `03 Tools/Claude Code/Reference/09` | **merge section** | เพิ่ม section "Permission Model Deep Dive" ต่อจาก settings scope ที่มี — อธิบาย 7 permission modes และ ML-based classifier ไม่แก้ตาราง settings scope เดิม |
| 1.4 | สร้าง note: Context Compaction Pipeline | `03 Tools/Claude Code/Core/` | **note ใหม่** | 5-layer compaction pipeline — เนื้อหานี้ไม่มีที่ลงใน note เดิมเลย ต้องสร้างใหม่ ลิงก์กลับ `Context Windows MOC` และ `01 - Claude Code คืออะไร` |
| 1.5 | สร้าง note: Extensibility Mechanisms | `03 Tools/Claude Code/Core/` | **note ใหม่** | ภาพรวม 4 mechanisms (MCP, plugins, skills, hooks) — note เดิมแต่ละตัวอธิบายแยก ๆ แต่ยังไม่มี note ที่วาง landscape ของ extensibility ทั้งหมด |
| 1.6 | เสริม `03 - Orchestrator Pattern` | `03 Tools/Claude Code/Core/03` | **merge section** | เพิ่ม section "Implementation Detail" — subagent delegation mechanism, worktree isolation, append-oriented session storage ต่อจาก comparison table ที่มี |
| 1.7 | สร้าง note: Claude Code vs OpenClaw | `03 Tools/Claude Code/Core/` | **note ใหม่** | comparative architecture — deployment context ต่างกันทำให้ design choices ต่างกัน (per-action vs perimeter safety, CLI loop vs gateway runtime, context-window vs gateway-wide capability) |
| 1.8 | เสริมหรือสร้าง: Open Design Directions | `04 Synthesis/Bridge/` | **note ใหม่** | 6 open directions — เป็น cross-domain (ไม่ใช่แค่ Claude Code) จึงเหมาะอยู่ Synthesis ลิงก์กลับ Agent Fundamentals, Guardrails, Evals |
| 1.9 | อัปเดต Claude Code MOC | `03 Tools/Claude Code/Claude Code - Multi-Agent MOC` | **update links** | เพิ่ม links ไป notes ใหม่ (1.4, 1.5, 1.7) และระบุว่า notes ไหนถูกเสริม |
| 1.10 | อัปเดต cross-links | หลายไฟล์ | **update links** | เชื่อม Context Windows MOC ↔ compaction note, Guardrails ↔ permission deep dive |

### Quality Gates

- [ ] อ่าน note ปลายทางก่อนเขียนทุกครั้ง
- [ ] merge sections ต้องไม่เปลี่ยน heading structure เดิม
- [ ] ทุก claim ใหม่ต้องมี `source: arxiv 2604.14228` หรือระบุว่าเป็น architectural inference
- [ ] note ใหม่ต้องมี metadata ครบตาม Vault Standards
- [ ] ตรวจว่า cross-links ไม่ broken หลัง update

---

## Phase 2: S1 — RAG-Anything

### Gap Analysis — เทียบกับ notes ที่มี

**`RAG - Knowledge Graph RAG`** — อธิบาย GraphRAG vs Vector RAG, retrieval patterns (text-based, entity-based, cluster-based, NL2Cypher), failure modes, design rules
→ paper เสริมได้: cross-modal entity extraction และ cross-modal relationship mapping ซึ่ง note เดิมพูดถึงแค่ text-based entities

**`RAG - Agentic RAG`** — อธิบาย classic vs agentic RAG, query planning, subquery decomposition, tool-augmented retrieval, iterative retrieval
→ paper เสริมได้: VLM-enhanced query mode เป็นรูปแบบใหม่ของ tool-augmented retrieval ที่ใช้ vision model วิเคราะห์ images ใน retrieved context

**`RAG - Hybrid Retrieval`** — อธิบาย keyword + vector fusion
→ paper เสริมได้: vector-graph fusion เป็น hybrid อีกแบบที่ผสม vector similarity กับ graph traversal

**ยังไม่มีใน vault เลย:**
- Multimodal RAG เป็น concept เฉพาะ (multimodal document parsing, modality-aware processing, multimodal knowledge graph index)
- Modality-aware ranking

### Ingest Tasks

| # | งาน | ปลายทาง | วิธี | รายละเอียด |
|---|---|---|---|---|
| 2.1 | Source Record | `00 Raw Sources/Source Records/` | สร้างใหม่ | ลงทะเบียน source |
| 2.2 | สร้าง note: RAG - Multimodal RAG | `02 AI Systems/RAG/Retrieval/` | **note ใหม่** | architecture ของ multimodal RAG pipeline: document parsing → content categorization → modality-specific analysis → multimodal KG index → modality-aware retrieval ลิงก์กลับ Knowledge Graph RAG, Hybrid Retrieval, Agentic RAG, Multimodal Foundations |
| 2.3 | เสริม `RAG - Knowledge Graph RAG` | `02 AI Systems/RAG/Retrieval/` | **merge section** | เพิ่ม section "Cross-Modal Knowledge Graph" ต่อจาก Graph Construction Cost — อธิบาย multi-modal entity extraction, cross-modal relationship mapping, weighted relationship scoring ไม่แก้ retrieval patterns เดิม |
| 2.4 | เสริม `RAG - Agentic RAG` | `02 AI Systems/RAG/Core/` | **merge section** | เพิ่ม section "VLM-Enhanced Query" ใน "รูปแบบที่พบบ่อย" — อธิบายว่า retrieved context ที่มี images สามารถส่งเข้า VLM เพื่อวิเคราะห์ร่วมกับ text ได้ เป็น pattern ใหม่ของ tool-augmented retrieval |
| 2.5 | เสริม `RAG - Hybrid Retrieval` | `02 AI Systems/RAG/Retrieval/` | **merge section** | เพิ่ม section "Vector-Graph Fusion" — อธิบาย hybrid ที่ผสม vector similarity กับ graph traversal (ต่างจาก keyword+vector ที่มีอยู่) |
| 2.6 | อัปเดต RAG MOC | `02 AI Systems/RAG/RAG - MOC` | **update links** | เพิ่ม link ไป Multimodal RAG note ใหม่ |
| 2.7 | อัปเดต cross-links | หลายไฟล์ | **update links** | เชื่อม Multimodal Foundations ↔ Multimodal RAG, Use Cases - Design a RAG System ↔ Multimodal RAG |

### Quality Gates

- [ ] อ่าน note ปลายทางก่อนเขียนทุกครั้ง
- [ ] merge sections ต้องไม่เปลี่ยน heading structure หรือ claims เดิม
- [ ] ทุก claim ใหม่ต้องมี source citation (RAG-Anything paper / repo)
- [ ] Multimodal RAG note ใหม่ต้องลิงก์กลับ notes ที่เกี่ยวข้องอย่างน้อย 5 ตัว
- [ ] ตรวจว่า RAG MOC learning path ยังอ่านได้ต่อเนื่องหลังเพิ่ม note

---

## Phase 3: S4 — llm-engineer-toolkit (optional, ถ้ามีเวลา)

### Gap Analysis

vault มี framework landscape อยู่แล้ว — ต้องอ่าน `01 - Landscape` ก่อนเพื่อเช็กว่ามี libraries ตัวไหนแล้ว

### Ingest Tasks

| # | งาน | ปลายทาง | วิธี | รายละเอียด |
|---|---|---|---|---|
| 3.1 | Source Record | `00 Raw Sources/Source Records/` | สร้างใหม่ | ลงทะเบียน source |
| 3.2 | เสริม Agent Frameworks Landscape | `02 AI Systems/Agent Frameworks/Core/01 - Landscape` | **merge** | เพิ่มเฉพาะ libraries ที่ยังไม่มีและเกี่ยวกับ agent/orchestration โดยตรง ไม่เพิ่ม libraries ที่อยู่นอก scope |

---

## Phase 4: S3 — ai-engineering-from-scratch (ไม่แนะนำ ingest)

### เหตุผล

- เนื้อหาส่วนใหญ่อยู่นอก scope ของ vault (math, classical ML, CV, speech, RL)
- ส่วนที่ overlap (LLMs, agents, RAG, MCP) vault มีลึกกว่าอยู่แล้ว
- เป็น breadth-first curriculum ขณะที่ vault เป็น depth-first knowledge base
- ไม่มีเนื้อหาที่จะเสริมความลึกให้ notes เดิมได้

### Ingest Tasks

| # | งาน | ปลายทาง | วิธี | รายละเอียด |
|---|---|---|---|---|
| 4.1 | Source Record (optional) | `00 Raw Sources/Source Records/` | สร้างใหม่ | เก็บไว้เป็น reference เฉย ๆ |

---

## Checklist รวม

### Phase 1 — Dive into Claude Code
- [x] 1.1 Source Record
- [x] 1.2 เสริม `01 - Claude Code คืออะไร` (merge: architecture overview + 7 components + 5 values)
- [x] 1.3 เสริม `09 - Permissions และ Settings` (merge: 7 modes, ML classifier, 7-layer pipeline)
- [x] 1.4 สร้าง Context Compaction Pipeline (note ใหม่: 5-layer graduated compaction)
- [x] 1.5 สร้าง Extensibility Mechanisms (note ใหม่: 4 mechanisms, context cost ordering)
- [x] 1.6 เสริม `03 - Orchestrator Pattern` (merge: Agent Tool types, isolation, sidechain, permission override)
- [x] 1.7 สร้าง Claude Code vs OpenClaw (note ใหม่: comparative architecture 6 มิติ)
- [x] 1.8 สร้าง Open Design Directions (note ใหม่ ใน Synthesis: 6 directions + value tensions)
- [x] 1.9 อัปเดต Claude Code MOC
- [x] 1.10 อัปเดต cross-links + Synthesis MOC
- [x] 1.11 เพิ่ม 13 Design Principles table ใน `01 - Claude Code คืออะไร`
- [x] 1.12 เสริม `12 - CLAUDE File` (merge: 4-level hierarchy, lazy loading, @include, context delivery, memory retrieval)
- [x] 1.13 เพิ่ม Recovery Mechanisms + Stop Conditions ใน `25 - Context Compaction Pipeline`
- [x] 1.14 สร้าง Session Persistence and Recovery (note ใหม่: transcript model, resume/fork, permission non-restoration)
- [x] 1.15 เพิ่ม Value Tensions + Empirical Signals ใน Open Design Directions

### Phase 2 — RAG-Anything
- [x] 2.1 Source Record
- [x] 2.2 สร้าง Multimodal RAG (note ใหม่)
- [x] 2.3 เสริม Knowledge Graph RAG (merge: cross-modal KG section)
- [x] 2.4 เสริม Agentic RAG (merge: VLM-Enhanced Retrieval pattern)
- [x] 2.5 เสริม Hybrid Retrieval (merge: Vector-Graph Fusion section)
- [x] 2.6 อัปเดต RAG MOC
- [x] 2.7 อัปเดต cross-links

### Phase 3 — llm-engineer-toolkit (optional)
- [x] 3.1 Source Record
- [x] 3.2 เสริม Landscape (merge: Extended Landscape tables)

### Phase 4 — ai-engineering-from-scratch (skip)
- [x] 4.1 Source Record (reference only)

---

## Cross-Links

- [[00 Raw Sources/Raw Sources - MOC]]
- [[00 Raw Sources/Source Intake Checklist]]
- [[Knowledge Topic Registry]]
- [[03 Tools/Claude Code/Claude Code - Multi-Agent MOC]]
- [[02 AI Systems/RAG/RAG - MOC]]
- [[02 AI Systems/Agent Frameworks/Agent Frameworks - MOC]]
