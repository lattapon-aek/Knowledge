---
tags:
  - ingest
  - plan
  - ibm
  - ml-primitives
  - governance
  - multi-agent
  - prompting
type: guide
status: draft
source: ""
parent_note: "[[00 Raw Sources/Raw Sources - MOC]]"
created: "2026-04-23"
updated: ""
---

# 2026-04 IBM Supplement - Ingest Plan

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

### ML Primitives — เสริมจาก Official Sources

| # | ชื่อ | องค์กร | URL |
|---|---|---|---|
| 7 | ML Crash Course | Google | https://developers.google.com/machine-learning/crash-course/ |
| 8 | Fundamentals of ML | Microsoft Learn | https://learn.microsoft.com/en-us/training/modules/fundamentals-machine-learning/ |
| 9 | ML Specialization | DeepLearning.AI / Stanford | https://www.deeplearning.ai/courses/machine-learning-specialization/ |
| 10 | CS229 Machine Learning | Stanford | https://cs229.stanford.edu/ |

---

## 4 Tasks

### Task I.1: Multi-Agent Topology (Vertical / Horizontal / Hybrid)

**Gap**: vault มี `Synthesis - Single to Multi-Agent Infrastructure` ที่อธิบาย orchestration, messaging, state, observability แต่ยังไม่มี topology taxonomy

**Source**: IBM Agentic Architecture

**วิธี**: merge section ใน `04 Synthesis/Bridge/Synthesis - Single to Multi-Agent Infrastructure`

**เนื้อหา**:
- Vertical: leader agent ดูแล subtasks, centralized control, clear accountability, bottleneck risk
- Horizontal: peer collaboration, decentralized decisions, parallel processing, coordination challenges
- Hybrid: dynamic leadership shifts ตาม task phase, versatile, complex
- ตารางเปรียบเทียบ strengths/weaknesses/best use cases

---

### Task I.2: Agent-Level Governance

**Gap**: vault มี Guardrails ครบเรื่อง input/output/tool/permission/fallback แต่ยังไม่มี agent-specific governance

**Source**: IBM AI Agent Governance

**วิธี**: merge section ใน `02 AI Systems/Guardrails/Operations/06 - Monitoring and Incidents` + เสริม `Open Design Directions` (governance section)

**เนื้อหา**:
- Governance agents — agents ที่ monitor/evaluate agents อื่น
- Agent-to-agent monitoring — ตรวจ interactions, conflict resolution rules
- Behavioral drift detection — agent ที่ adapt จาก interactions อาจ drift
- AI sandboxing — simulated environments สำหรับ test ethical dilemmas ก่อน deploy
- Emergency shutdown mechanisms

---

### Task I.3: Agentic Prompting

**Gap**: vault มี Prompt Engineering 7 notes แต่ยังไม่มี agentic prompting เป็น concept เฉพาะ

**Source**: IBM Prompt Engineering Hub + Anthropic "Building Effective Agents"

**วิธี**: merge section ใน `01 Foundations/Prompt Engineering/Core/03 - Prompt Patterns พื้นฐาน`

**เนื้อหา**:
- Agentic prompting คืออะไร — prompts ที่ guide agents ให้ plan, use tools, self-reflect, delegate
- Patterns: ReAct prompting, tool-use prompting, planning prompts, self-evaluation prompts
- Context engineering → harness engineering connection (3 layers)
- Anthropic workflow patterns: prompt chaining, routing, parallelization, orchestrator-workers, evaluator-optimizer

---

### Task I.4: ML Primitives for LLM

**Gap**: vault มี LLM Foundations 14 notes แต่ขาด ML primitives ที่เป็นรากฐาน

**Source**: Google ML Crash Course, Microsoft Learn, DeepLearning.AI/Stanford, IBM ML Hub

**วิธี**: สร้าง bridge note ใหม่ ใน `01 Foundations/LLM Foundations/Bridge/`

**เนื้อหา**:

| ML Primitive | เชื่อมกับ LLM note | ทำไมสำคัญ |
|---|---|---|
| Supervised vs Unsupervised vs RL | `03 - การฝึกและ Post-Training` | pretraining = unsupervised, fine-tuning = supervised |
| Loss Functions (cross-entropy) | `03`, `07 - Logits, Decoding` | cross-entropy เป็นหัวใจของ LLM training |
| Gradient Descent / Optimization | `03` | optimizer ทำให้ model เรียนรู้ |
| Overfitting / Regularization | `05 - ข้อจำกัด`, `08 - Data` | data mixture, model size เกี่ยวกับ overfitting |
| Bias-Variance Tradeoff | `05`, `08` | model ใหญ่ขึ้นไม่ได้ดีขึ้นเสมอ |
| Evaluation Metrics | `05`, `13 - Evaluation Foundations` | precision, recall, F1, perplexity |
| Neural Network Basics | `02 - สถาปัตยกรรม Transformer` | Transformer เป็น NN architecture เฉพาะทาง |
| Classification vs Regression | `13` | next-token prediction เป็น classification |
| Feature Engineering → Embeddings | `10 - Embeddings`, `14 - Vector` | embeddings คือ learned features |

---

## Registration Tasks

| # | งาน |
|---|---|
| I.5 | Source Record |
| I.6 | อัปเดต LLM Foundations MOC (เพิ่ม ML Primitives bridge note) |
| I.7 | อัปเดต index, Home, Topic Registry |
| I.8 | Cross-links audit |

---

## Checklist รวม

- [ ] I.1 Multi-Agent Topology (merge)
- [ ] I.2 Agent-Level Governance (merge)
- [ ] I.3 Agentic Prompting (merge)
- [ ] I.4 ML Primitives for LLM (bridge note ใหม่)
- [ ] I.5 Source Record
- [ ] I.6 Update LLM Foundations MOC
- [ ] I.7 Update index, Home, Topic Registry
- [ ] I.8 Cross-links audit

---

## Cross-Links

- [[00 Raw Sources/Raw Sources - MOC]]
- [[01 Foundations/LLM Foundations/LLM Foundations - MOC]]
- [[01 Foundations/Prompt Engineering/Prompt Engineering - MOC]]
- [[02 AI Systems/Guardrails/Guardrails - MOC]]
- [[04 Synthesis/Bridge/Synthesis - Single to Multi-Agent Infrastructure]]
- [[04 Synthesis/Bridge/Synthesis - Open Design Directions for Agent Systems]]
