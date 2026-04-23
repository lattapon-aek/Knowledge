---
tags:
  - ingest
  - plan
  - ibm
  - ml-primitives
  - governance
  - multi-agent
  - prompting
  - gap-closure
type: guide
status: draft
source: ""
parent_note: "[[00 Raw Sources/Raw Sources - MOC]]"
created: "2026-04-23"
updated: "2026-04-23"
---

# 2026-04 IBM Supplement + Vault Gap Closure - Ingest Plan

---

## หลักการ Ingest

> **เสริมลึก ไม่ทับเดิม** — อ่าน note ปลายทางก่อนเขียนทุกครั้ง

---

## แหล่งข้อมูล

### IBM Sources

| # | ชื่อ | URL |
|---|---|---|
| 1 | IBM AI Agents Hub | https://www.ibm.com/think/ai-agents |
| 2 | IBM Components of AI Agents | https://www.ibm.com/think/topics/components-of-ai-agents |
| 3 | IBM Agentic Architecture | https://www.ibm.com/think/topics/agentic-architecture |
| 4 | IBM AI Agent Governance | https://www.ibm.com/think/insights/ai-agent-governance |
| 5 | IBM Prompt Engineering Hub | https://www.ibm.com/think/prompt-engineering |
| 6 | IBM Machine Learning Hub | https://www.ibm.com/think/machine-learning |

### ML Primitives — Official Sources

| # | ชื่อ | องค์กร | URL |
|---|---|---|---|
| 7 | ML Crash Course | Google | https://developers.google.com/machine-learning/crash-course/ |
| 8 | Fundamentals of ML | Microsoft Learn | https://learn.microsoft.com/en-us/training/modules/fundamentals-machine-learning/ |
| 9 | ML Specialization | DeepLearning.AI / Stanford | https://www.deeplearning.ai/courses/machine-learning-specialization/ |
| 10 | CS229 Machine Learning | Stanford | https://cs229.stanford.edu/ |

### MCP Restore — Official Source

| # | ชื่อ | URL |
|---|---|---|
| 11 | MCP Official Docs | https://modelcontextprotocol.io/ |

### LLM Training / Optimization — Official Sources

| # | ชื่อ | องค์กร |
|---|---|---|
| 12 | OpenAI Fine-tuning Docs | OpenAI |
| 13 | Anthropic Fine-tuning / Constitutional AI | Anthropic |
| 14 | Google Vertex AI Model Tuning | Google |
| 15 | Hugging Face PEFT / Quantization Docs | Hugging Face |

---

## Phase C: CRITICAL — ต้องทำก่อน

| # | งาน | ปัญหา | ปลายทาง | วิธี |
|---|---|---|---|---|
| C.1 | MCP Core Notes restore | notes 02, 03, 04 หายเพราะ colon ในชื่อไฟล์บน Windows | `02 AI Systems/MCP/Core/` + `Client/` + `Bridge/` | recreate จาก MCP official docs (เปลี่ยนชื่อไฟล์ไม่ใช้ colon) |
| C.2 | ตรวจ Prompt Injection note | ตรวจว่า `Guardrails - Prompt Injection and Content Attacks` มี depth พอไหม | `02 AI Systems/Guardrails/Core/` | ตรวจ + เสริมถ้าจำเป็น |

---

## Phase I: IMPORTANT — IBM Supplement

| # | งาน | ที่มา | ปลายทาง | วิธี |
|---|---|---|---|---|
| I.1 | Multi-Agent Topology (Vertical/Horizontal/Hybrid) | IBM Agentic Architecture | `04 Synthesis/Bridge/Synthesis - Single to Multi-Agent Infrastructure` | merge section |
| I.2 | Agent-Level Governance (governance agents, drift, sandboxing) | IBM AI Agent Governance | `02 AI Systems/Guardrails/Operations/06 - Monitoring and Incidents` + `Open Design Directions` | merge sections |
| I.3 | Agentic Prompting (plan/tool-use/reflect/delegate) | IBM Prompt Hub + Anthropic | `01 Foundations/Prompt Engineering/Core/03 - Prompt Patterns พื้นฐาน` | merge section |
| I.4 | ML Primitives for LLM | Google/Microsoft/Stanford/IBM | `01 Foundations/LLM Foundations/Bridge/` | bridge note ใหม่ |

---

## Phase D: IMPORTANT — Vault Depth Gaps

| # | งาน | Gap จาก | ปลายทาง | วิธี |
|---|---|---|---|---|
| D.1 | Fine-tuning Deep Dive (RLHF, DPO, LoRA, when to fine-tune) | Gap Analysis — `03 - การฝึก` มีแต่ shallow | `01 Foundations/LLM Foundations/Core/03` | merge section เสริม depth |
| D.2 | Model Compression & Inference Optimization (quantization, distillation, pruning, KV cache optimization) | Gap Analysis — ไม่มีเลย | `01 Foundations/LLM Foundations/Core/` | note ใหม่ |
| D.3 | Scaling Laws & Emergence (Chinchilla, emergence thresholds, capability prediction) | Gap Analysis — shallow ใน `08 - Data` | `01 Foundations/LLM Foundations/Core/08` | merge section |

---

## Phase N: NICE-TO-HAVE — ถ้ามีเวลา

| # | งาน | ปลายทาง | วิธี |
|---|---|---|---|
| N.1 | Advanced Prompting (CoT, ToT, GoT, self-consistency) | `Prompt Patterns พื้นฐาน` | merge section |
| N.2 | Memory Compression & Summarization | `Memory Systems/Core/` | note ใหม่ |
| N.3 | RAG Failure Modes taxonomy | `RAG/Evaluation/` | note ใหม่ |

---

## Registration Tasks

| # | งาน |
|---|---|
| R.1 | Source Record (IBM + ML sources) |
| R.2 | อัปเดต MOCs ที่เกี่ยวข้อง (LLM Foundations, Prompt Engineering, Guardrails, MCP, Synthesis) |
| R.3 | อัปเดต index, Home, Topic Registry |
| R.4 | Cross-links audit |

---

## Checklist รวม

### Phase C — Critical
- [x] C.1 MCP Core Notes restore (02, 03, 04, 14 Bridge)
- [x] C.2 ตรวจ Prompt Injection note — depth พอแล้ว ไม่ต้องแก้

### Phase I — IBM Supplement
- [x] I.1 Multi-Agent Topology (merge)
- [x] I.2 Agent-Level Governance (merge)
- [x] I.3 Agentic Prompting (merge)
- [x] I.4 ML Primitives for LLM (bridge note ใหม่)

### Phase D — Depth Gaps
- [x] D.1 Fine-tuning Deep Dive (merge)
- [x] D.2 Model Compression & Optimization (note ใหม่)
- [x] D.3 Scaling Laws & Emergence (merge)

### Phase N — Nice-to-Have
- [ ] N.1 Advanced Prompting (merge)
- [ ] N.2 Memory Compression (note ใหม่)
- [ ] N.3 RAG Failure Modes (note ใหม่)

### Registration
- [ ] R.1 Source Record
- [ ] R.2 Update MOCs
- [ ] R.3 Update index, Home, Topic Registry
- [ ] R.4 Cross-links audit

---

## Cross-Links

- [[00 Raw Sources/Raw Sources - MOC]]
- [[01 Foundations/LLM Foundations/LLM Foundations - MOC]]
- [[01 Foundations/Prompt Engineering/Prompt Engineering - MOC]]
- [[02 AI Systems/Guardrails/Guardrails - MOC]]
- [[02 AI Systems/MCP/MCP - MOC]]
- [[04 Synthesis/Bridge/Synthesis - Single to Multi-Agent Infrastructure]]
- [[04 Synthesis/Bridge/Synthesis - Open Design Directions for Agent Systems]]
