---
tags:
  - ingest
  - plan
  - harness-engineering
type: guide
status: draft
source: ""
parent_note: "[[00 Raw Sources/Raw Sources - MOC]]"
created: "2026-04-23"
updated: ""
---

# 2026-04 Harness Engineering - Ingest Plan

---

## หลักการ Ingest

> **เสริมลึก ไม่ทับเดิม** — อ่าน note ปลายทางก่อนเขียนทุกครั้ง

---

## แหล่งข้อมูล

### Tier A — Official / Primary Sources

| # | Source | องค์กร | URL |
|---|---|---|---|
| A1 | Harness design for long-running apps | Anthropic | https://www.anthropic.com/engineering/harness-design-long-running-apps |
| A2 | Managed Agents: Decoupling brain from hands | Anthropic | https://www.anthropic.com/engineering/managed-agents |
| A3 | Harness engineering: leveraging Codex | OpenAI | https://openai.com/index/harness-engineering/ |
| A4 | Harness engineering for coding agent users | Martin Fowler (Birgitta Böckeler) | https://martinfowler.com/articles/harness-engineering.html |
| A5 | The Anatomy of an Agent Harness | LangChain | https://www.langchain.com/blog/the-anatomy-of-an-agent-harness |

### Tier B — Expert Analysis

| # | Source | ผู้แต่ง | URL |
|---|---|---|---|
| B1 | The importance of Agent Harness in 2026 | Philipp Schmid | https://www.philschmid.de/agent-harness-2026 |
| B2 | What Is Harness Engineering? | MindStudio | https://www.mindstudio.ai/blog/what-is-harness-engineering-ai-coding |
| B3 | An Introduction to Harness Engineering | Rob Sherling (dev.to) | https://dev.to/robearlam/an-introduction-to-harness-engineering-3j9l |
| B4 | AI Harness Engineering guide | Medium/Be Open | https://medium.com/be-open/what-is-ai-harness-engineering-your-guide-to-controlling-autonomous-systems-30c9c8d2b489 |

---

## Gap Analysis — เทียบกับ Vault ที่มี

### มีอยู่แล้ว (บางส่วน)

| เนื้อหา | อยู่ใน Note | ระดับ |
|---|---|---|
| "minimal scaffolding, maximal operational harness" | `01 - Claude Code คืออะไร` | กล่าวถึงเป็น principle |
| 5-layer compaction pipeline | `25 - Context Compaction Pipeline` | ลึก (เป็น harness component) |
| 4 extensibility mechanisms | `26 - Extensibility Mechanisms` | ลึก (เป็น harness component) |
| Subagent delegation + isolation | `03 - Orchestrator Pattern` | ลึก (เป็น harness pattern) |
| Harness boundary evolution | `Open Design Directions` | กล่าวถึงเป็น open direction |
| Agent architecture patterns | `07 - รูปแบบ Agent Architectures` | 6 patterns (ReAct, CodeAct, Tool-Using, Self-Reflective, Multi-Agent, Agentic RAG) |
| Framework vs Custom Build | `02 - Framework vs Custom Build` | tradeoff analysis |
| Agent Runtime Layers | `Synthesis - Agent Runtime Layers` | bridge map |

### ยังไม่มีใน Vault

| เนื้อหา | ที่มา | ความสำคัญ |
|---|---|---|
| **Harness Engineering เป็น concept** — definition, Agent = Model + Harness, 3 layers (prompt → context → harness) | ทุก source | ⭐⭐⭐ สูงมาก |
| **Harness components taxonomy** — filesystem, bash/sandbox, memory/search, compaction/context rot, skills/progressive disclosure | LangChain, MindStudio | ⭐⭐⭐ สูงมาก |
| **Guides vs Sensors** (feedforward vs feedback) — computational vs inferential controls | Martin Fowler | ⭐⭐⭐ สูงมาก |
| **Harness patterns** — Generator-Evaluator loop, Ralph Loop, Decompose-Solve-Merge, Sprint Contracts, Speculative Execution | Anthropic, OpenAI, LangChain, MindStudio | ⭐⭐⭐ สูงมาก |
| **Harness co-evolution** — assumptions go stale, build-to-delete, Bitter Lesson, space moves not shrinks | Anthropic, LangChain, Philipp Schmid | ⭐⭐ สูง |
| **Harness = OS analogy** — model=CPU, context=RAM, harness=OS, agent=application | Philipp Schmid, Anthropic (Managed Agents) | ⭐⭐ สูง |
| **Harnessability** — not every codebase is equally amenable, greenfield vs legacy | Martin Fowler | ⭐⭐ สูง |
| **Harness regulation categories** — maintainability, architecture fitness, behaviour | Martin Fowler | ⭐⭐ สูง |
| **Managed Agents** — virtualized components (session, harness, sandbox), pets vs cattle | Anthropic | ⭐⭐ สูง |

---

## Ingest Tasks

### Phase H1: Core Concept + Components

| # | งาน | ปลายทาง | วิธี | รายละเอียด |
|---|---|---|---|---|
| H1.1 | Source Records (รวม 9 sources) | `00 Raw Sources/Source Records/` | สร้างใหม่ | 1 source record รวมทุก source |
| H1.2 | สร้าง note: Harness Engineering คืออะไร | `02 AI Systems/AI Agent Fundamentals/Core/` | **note ใหม่** | definition (Agent = Model + Harness), 3 layers (prompt → context → harness), OS analogy, harness components taxonomy (filesystem, bash/sandbox, memory, compaction, skills), ทำไมต้องมี harness |
| H1.3 | สร้าง note: Guides vs Sensors — Harness Control Taxonomy | `02 AI Systems/AI Agent Fundamentals/Core/` หรือ `02 AI Systems/Agent Frameworks/Core/` | **note ใหม่** | feedforward vs feedback, computational vs inferential, timing (keep quality left), regulation categories (maintainability, architecture fitness, behaviour), harnessability |

### Phase H2: Patterns + Architecture

| # | งาน | ปลายทาง | วิธี | รายละเอียด |
|---|---|---|---|---|
| H2.1 | สร้าง note: Harness Patterns | `02 AI Systems/Agent Frameworks/Core/` | **note ใหม่** | Generator-Evaluator loop (Anthropic), Ralph Loop (OpenAI/LangChain), Decompose-Solve-Merge, Sprint Contracts, Speculative Execution, Context Resets vs Compaction |
| H2.2 | เสริม `07 - รูปแบบ Agent Architectures` | `02 AI Systems/AI Agent Fundamentals/Core/` | **merge section** | เพิ่ม section เชื่อม harness patterns กับ agent architecture patterns ที่มีอยู่ |
| H2.3 | เสริม `02 - Framework vs Custom Build` | `02 AI Systems/Agent Frameworks/Core/` | **merge section** | เพิ่ม harness perspective — framework = pre-built harness, custom build = custom harness |

### Phase H3: Evolution + Synthesis

| # | งาน | ปลายทาง | วิธี | รายละเอียด |
|---|---|---|---|---|
| H3.1 | สร้าง note: Harness Co-Evolution and Lifecycle | `04 Synthesis/Bridge/` | **note ใหม่** | assumptions go stale, build-to-delete, Bitter Lesson, Managed Agents (virtualized components), harness as dataset for training, space moves not shrinks |
| H3.2 | เสริม `Open Design Directions` | `04 Synthesis/Bridge/` | **merge section** | เพิ่ม harness engineering references ที่ยืนยัน/ขยาย directions ที่มีอยู่ |
| H3.3 | เสริม `Synthesis - Agent Runtime Layers` | `04 Synthesis/Bridge/` | **merge section** | เพิ่ม harness layer ใน runtime stack |

### Phase H4: MOC + Cross-Links + Registration

| # | งาน | ปลายทาง | วิธี | รายละเอียด |
|---|---|---|---|---|
| H4.1 | อัปเดต AI Agent Fundamentals MOC | `02 AI Systems/AI Agent Fundamentals/` | **update links** | เพิ่ม Harness Engineering note |
| H4.2 | อัปเดต Agent Frameworks MOC | `02 AI Systems/Agent Frameworks/` | **update links** | เพิ่ม Harness Patterns + Guides vs Sensors |
| H4.3 | อัปเดต index.md, Home.md, Knowledge Topic Registry | root | **update** | ลงทะเบียน notes ใหม่ |
| H4.4 | อัปเดต cross-links ทั้งหมด | หลายไฟล์ | **update** | เชื่อม Claude Code notes ↔ harness notes, Context Windows ↔ harness, Guardrails ↔ harness |

---

## Quality Gates

- [ ] อ่าน note ปลายทางก่อนเขียนทุกครั้ง
- [ ] merge sections ต้องไม่เปลี่ยน heading structure เดิม
- [ ] ทุก claim ต้องมี source citation
- [ ] notes ใหม่ต้องมี metadata ครบตาม Vault Standards
- [ ] Mermaid diagrams ต้อง mobile-compatible (ไม่มี br tags, node สั้น)
- [ ] ตรวจว่า cross-links ไม่ broken หลัง update
- [ ] ลงทะเบียนใน index, Home, Topic Registry

---

## Checklist รวม

### Phase H1 — Core Concept
- [x] H1.1 Source Record
- [x] H1.2 Harness Engineering คืออะไร (note ใหม่)
- [x] H1.3 Guides vs Sensors (note ใหม่)

### Phase H2 — Patterns
- [x] H2.1 Harness Patterns (note ใหม่)
- [x] H2.2 เสริม Agent Architectures (merge)
- [x] H2.3 เสริม Framework vs Custom Build (merge)

### Phase H3 — Evolution + Synthesis
- [x] H3.1 Harness Co-Evolution (note ใหม่)
- [x] H3.2 เสริม Open Design Directions (merge)
- [x] H3.3 เสริม Agent Runtime Layers (merge)

### Phase H4 — Registration
- [x] H4.1 Update AI Agent Fundamentals MOC
- [x] H4.2 Update Agent Frameworks MOC
- [x] H4.3 Update index, Home, Topic Registry, Source Records MOC, Synthesis MOC
- [x] H4.4 Cross-links audit

---

## Cross-Links

- [[00 Raw Sources/Raw Sources - MOC]]
- [[00 Raw Sources/Source Intake Checklist]]
- [[Knowledge Topic Registry]]
- [[02 AI Systems/AI Agent Fundamentals/AI Agent Fundamentals - MOC]]
- [[02 AI Systems/Agent Frameworks/Agent Frameworks - MOC]]
- [[04 Synthesis/Synthesis - MOC]]
- [[03 Tools/Claude Code/Claude Code - Multi-Agent MOC]]
