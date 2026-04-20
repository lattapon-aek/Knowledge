---
tags:
  - synthesis
  - agents
  - future-directions
  - design-space
type: synthesis
status: draft
source: "arxiv 2604.14228"
parent_note: "[[04 Synthesis/Synthesis - MOC]]"
created: "2026-04-20"
updated: ""
---

# Synthesis - Open Design Directions for Agent Systems

> สังเคราะห์จาก arxiv 2604.14228 (Dive into Claude Code) Section 12
> เป็น cross-domain directions ไม่ใช่เฉพาะ Claude Code — จึงอยู่ใน Synthesis ไม่ใช่ Tools

---

## ที่มา

paper วิเคราะห์ Claude Code architecture แล้วระบุ 6 open design directions ที่ยังไม่มีคำตอบชัดเจนสำหรับ agent systems ทั่วไป แต่ละ direction มี literature รองรับ

---

## 6 Open Directions

### 1. Silent Failure และ Observability–Evaluation Gap

- industry surveys ประมาณว่า ~78% ของ AI failures เป็น invisible (Bessemer 2026)
- observability adoption สูง (~89%) แต่ offline evaluation ต่ำ (52.4%) (LangChain survey)
- คำถามเปิด: scaffolding สำหรับ generator–evaluator separation ควรอยู่ **ใน** harness (เช่น hook events เพิ่ม) หรือ **นอก** harness เป็น evaluation layer แยก?
- เชื่อมกับ: [[02 AI Systems/Evals/Evals - MOC|Evals]], [[02 AI Systems/Evals/Core/09 - Observability and Feedback Loops|Observability]]

### 2. Cross-Session Persistence: Memory และ Longitudinal Relationships

- ช่องว่างระหว่าง static instructions (CLAUDE.md) กับ single-session transcripts
- ยังขาด: accumulating layer สำหรับ experiential knowledge (strategies learned จาก past sessions)
- คำถามเปิด: substrate เดียวสามารถรองรับทั้ง personal instruction hierarchy และ shared organizational context ได้ไหม โดยยังรักษา file-based transparency?
- เชื่อมกับ: [[02 AI Systems/Memory Systems/Memory Systems - MOC|Memory Systems]], [[04 Synthesis/Bridge/Synthesis - Memory in Agents|Memory in Agents]]

### 3. Harness Boundary Evolution: Where, When, What, With Whom

harness ไม่หดลงเมื่อ model ดีขึ้น แต่ **เลื่อน** ไปตาม 4 แกน:

| แกน | ตัวอย่าง |
|---|---|
| **Where** (harness รันที่ไหน) | virtualized components, harness เป็น compile target |
| **When** (agent ทำงานเมื่อไร) | proactive agents, tick-based heartbeats, presence-aware |
| **What** (agent ทำอะไร) | vision-language-action, physical actions, non-textual effects |
| **With whom** (agent ทำงานกับใคร) | role-differentiated multi-agent, debate, graph-structured workflows |

- คำถามเปิด: harness architecture เดียวสามารถ span ทั้ง 4 แกนได้ หรือจะ fragment เป็น specialized stacks?
- เชื่อมกับ: [[02 AI Systems/AI Agent Fundamentals/Core/07 - รูปแบบ Agent Architectures|Agent Architectures]], [[02 AI Systems/Agent Frameworks/Agent Frameworks - MOC|Agent Frameworks]]

### 4. Horizon Scaling: จาก Session ไป Scientific Program

- agent systems ปัจจุบันออกแบบรอบ turn/session/sub-agent
- autonomous research pipelines ทำงานข้ามวัน-สัปดาห์ (AI Scientist, AlphaEvolve)
- คำถามเปิด: context management, summary-only return, append-only persistence ยังเพียงพอเมื่อ sessions compose เป็น multi-session programs ไหม?
- เชื่อมกับ: [[04 Synthesis/Bridge/Synthesis - Single to Multi-Agent Infrastructure|Single to Multi-Agent Infrastructure]]

### 5. Governance และ Oversight at Scale

- EU AI Act fully applicable August 2026
- MIT AI Agent Index: แค่ 13.3% ของ agentic systems publish agent-specific safety cards
- คำถามเปิด: logging, transparency, human-oversight affordances แบบไหนที่ coding agent architectures ควร expose ภายใต้ regulatory constraints?
- เชื่อมกับ: [[02 AI Systems/Guardrails/Guardrails - MOC|Guardrails]], [[02 AI Systems/Guardrails/Operations/06 - Monitoring and Incidents|Monitoring]]

### 6. Long-Term Human Capability Preservation

- RCT พบว่า AI tools ทำให้ developers ช้าลง 19% แม้รู้สึกว่าเร็วขึ้น 20%
- code complexity เพิ่ม 40.7% หลัง adopt AI coding tools
- EEG study พบ weakened neural connectivity ที่ persist หลังหยุดใช้ AI
- คำถามเปิด: architecture สามารถ treat sustainability gap เป็น first-class design problem ได้ไหม แทนที่จะเป็นแค่ downstream evaluation metric?
- หมายเหตุ: paper ระบุว่านี่เป็น **evaluative lens** ไม่ใช่ design value ที่ Claude Code implement อยู่จริง — เป็น concern ที่ยังไม่มี architectural mechanism รองรับ

---

## Pattern ที่เห็นข้าม Directions

- **Harness layer เป็นจุดที่ต้องแก้** — ส่วนใหญ่ของ open questions อยู่ที่ harness ไม่ใช่ model
- **Tension ระหว่าง values** — capability amplification vs long-term sustainability, safety vs autonomy, extensibility vs attack surface → ดูเพิ่มที่ section Value Tensions ด้านล่าง
- **Measurement gap** — หลาย directions ต้องการ metrics ที่ยังไม่มี (session-level comprehension, convention drift, silent failure detection)

---

## Value Tensions

> สรุปจาก paper Section 11.2 Table 4

5 values ที่ขับเคลื่อน architecture สร้าง tensions ที่หลีกเลี่ยงไม่ได้ — ไม่ใช่ design failures แต่เป็นผลจากการไล่ตามหลาย values พร้อมกัน:

| Value Pair | Tension | หลักฐาน |
|---|---|---|
| Authority x Safety | Approval fatigue vs protection | ผู้ใช้ approve 93% ของ permission prompts → human vigilance ไม่น่าเชื่อถือ ระบบต้องชดเชยด้วย classifier + sandboxing |
| Safety x Capability | Performance vs defense depth | commands >50 subcommands fallback เป็น generic prompt เพราะ parsing ทำ UI ค้าง → safety layers แชร์ performance constraints |
| Adaptability x Safety | Extensibility vs attack surface | CVEs หลายตัวเกิดจาก pre-trust initialization ของ hooks และ MCP servers |
| Capability x Adaptability | Proactivity vs disruption | proactive AI เพิ่ม task completion 12-18% แต่ preference ลดที่ high frequencies |
| Capability x Reliability | Velocity vs coherence | bounded context ป้องกัน full codebase awareness, subagent isolation จำกัด cross-agent consistency |

### Empirical Signals จาก Adjacent Systems

paper รวบรวมหลักฐานจากระบบที่มี architecture คล้ายกัน:

- **Productivity paradox**: RCT พบ developers ช้าลง 19% แม้รู้สึกเร็วขึ้น 20%
- **Complexity accrual**: code complexity เพิ่ม 40.7% หลัง adopt AI coding tools, velocity spike หายภายใน 3 เดือน
- **Technical debt**: audit 304,000 AI-authored commits พบ ~25% ของ AI-introduced issues persist, security issues persist สูงกว่า
- **Cognitive impact**: EEG study พบ weakened neural connectivity ที่ persist หลังหยุดใช้ AI

> หมายเหตุ: หลักฐานเหล่านี้มาจาก adjacent systems ไม่ใช่ Claude Code โดยตรง แต่ architectural parallels (bounded context, tool-use loops, single-pass generation) ทำให้ findings เกี่ยวข้อง

---

## ความสัมพันธ์กับโน้ตอื่น

- [[03 Tools/Claude Code/Core/01 - Claude Code คืออะไร|Claude Code คืออะไร]] — architecture ที่เป็นจุดเริ่มต้นของ analysis
- [[03 Tools/Claude Code/Core/27 - Claude Code vs OpenClaw|Claude Code vs OpenClaw]] — comparative architecture ที่ inform directions เหล่านี้
- [[02 AI Systems/AI Agent Fundamentals/AI Agent Fundamentals - MOC|AI Agent Fundamentals - MOC]] — agent concepts พื้นฐาน
- [[02 AI Systems/Evals/Evals - MOC|Evals - MOC]] — observability-evaluation gap
- [[02 AI Systems/Guardrails/Guardrails - MOC|Guardrails - MOC]] — governance และ safety
- [[02 AI Systems/Memory Systems/Memory Systems - MOC|Memory Systems - MOC]] — cross-session persistence
- [[04 Synthesis/Bridge/Synthesis - Safety, Reliability, and Evals|Safety, Reliability, and Evals]] — เชื่อม safety กับ evaluation
- [[04 Synthesis/Synthesis - MOC|Synthesis - MOC]]
