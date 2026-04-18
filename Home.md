---
tags: []
type: home
status: evergreen
source: ""
---

# Home

Second brain สำหรับความรู้ด้าน AI systems, LLMs, agents, prompting, และ tooling

---

## Layers

- [[00 Raw Sources/Raw Sources - MOC|Raw Sources]] — ชั้นข้อมูลต้นฉบับที่ใช้เป็น source of truth
- [[00 Raw Sources/Articles/Source Manifests - MOC|Source Manifests]] — entry points สำหรับชุดแหล่งข้อมูลที่ใช้อยู่จริง
- [[00 Raw Sources/Source Records/Source Records - MOC|Source Records]] — ทะเบียนแหล่งอ้างอิงที่กู้คืนจากโน้ตเดิม
- [[index]] — catalog กลางของฝั่ง wiki
- [[Knowledge Topic Registry]] — แผนที่กลางของ topic canonical ownership

---

## Domains

- [[02 AI Systems/AI Agent Fundamentals/AI Agent Fundamentals - MOC|AI Agent Fundamentals]]
- [[01 Foundations/LLM Foundations/LLM Foundations - MOC|LLM Foundations]]
- [[01 Foundations/Prompt Engineering/Prompt Engineering - MOC|Prompt Engineering]]
- [[01 Foundations/Context Windows/Context Windows - MOC|Context Windows]]
- [[02 AI Systems/MCP/MCP - MOC|MCP]]
- [[02 AI Systems/RAG/RAG - MOC|RAG]]
- [[02 AI Systems/Memory Systems/Memory Systems - MOC|Memory Systems]]
- [[02 AI Systems/Agent Frameworks/Agent Frameworks - MOC|Agent Frameworks]]
- [[02 AI Systems/Evals/Evals - MOC|Evals]]
- [[02 AI Systems/Guardrails/Guardrails - MOC|Guardrails]]
- [[01 Foundations/Tokenizer in AI/Tokenizer in AI - MOC|Tokenizer in AI]]
- [[03 Tools/Claude Code/Claude Code - Multi-Agent MOC|Claude Code]]
- [[04 Synthesis/Synthesis - MOC|Synthesis]]
- [[05 Use Cases/Use Cases - MOC|Use Cases]]
- [[06 Engineering/Engineering - MOC|Engineering]]

---

## Reading Paths

### Core LLM Path

1. [[01 Foundations/LLM Foundations/Core/01 - LLM คืออะไรและพื้นฐาน]]
2. [[01 Foundations/Tokenizer in AI/Core/01 - Tokenization คืออะไร]]
3. [[01 Foundations/LLM Foundations/Core/02 - สถาปัตยกรรม Transformer]]
4. [[01 Foundations/LLM Foundations/Core/04 - Inference, Context และ RAG]]
5. [[01 Foundations/Context Windows/Core/01 - Context Window คืออะไร]]
6. [[01 Foundations/LLM Foundations/Core/14 - Vector Representations และ Similarity Search]]

### Systems Designer Path

1. [[01 Foundations/LLM Foundations/Core/10 - Embeddings และ Semantic Similarity]]
2. [[01 Foundations/LLM Foundations/Core/14 - Vector Representations และ Similarity Search]]
3. [[04 Synthesis/Bridge/Synthesis - Weights, Context, Retrieval และ Tools]]
4. [[01 Foundations/Prompt Engineering/Core/07 - Structured Generation และ Output Formats]]
5. [[01 Foundations/LLM Foundations/Core/11 - Multimodal Foundations]]
6. [[01 Foundations/LLM Foundations/Core/13 - Evaluation Foundations]]

### Build Better Prompts

1. [[01 Foundations/Prompt Engineering/Core/01 - Prompt Engineering คืออะไร]]
2. [[01 Foundations/Prompt Engineering/Core/02 - องค์ประกอบของ Prompt]]
3. [[01 Foundations/Prompt Engineering/Core/03 - Prompt Patterns พื้นฐาน]]
4. [[01 Foundations/Prompt Engineering/Core/05 - Evaluation และ Failure Modes]]

### Build Agents

1. [[02 AI Systems/AI Agent Fundamentals/Core/01 - AI Agent คืออะไร]]
2. [[02 AI Systems/AI Agent Fundamentals/Core/04 - สถาปัตยกรรม Agent: Model + Tools + Orchestration]]
3. [[02 AI Systems/AI Agent Fundamentals/Core/05 - วงจร Perceive-Think-Act-Check]]
4. [[02 AI Systems/MCP/Bridge/14 - Tools: การออกแบบและทำงาน]]
5. [[02 AI Systems/MCP/Core/01 - MCP คืออะไรและแก้ปัญหาอะไร]]

---

## Learning Domains

- [[02 AI Systems/AI Agent Fundamentals/AI Agent Fundamentals - MOC|AI Agent Fundamentals]] — core runtime concepts สำหรับ agents
- [[02 AI Systems/MCP/MCP - MOC|MCP]] — protocol layer สำหรับ tools/resources/prompts
- [[02 AI Systems/RAG/RAG - MOC|RAG]] — retrieval-centric system design
- [[02 AI Systems/Memory Systems/Memory Systems - MOC|Memory Systems]] — working vs long-term memory และ policies
- [[02 AI Systems/Guardrails/Guardrails - MOC|Guardrails]] — safety, validation, permission, fallback
- [[02 AI Systems/Evals/Evals - MOC|Evals]] — metrics, regression, observability, feedback loops
- [[02 AI Systems/Agent Frameworks/Agent Frameworks - MOC|Agent Frameworks]] — framework thinking ก่อนลง implementation

---

## Synthesis And Application

- [[04 Synthesis/Synthesis - MOC|Synthesis - MOC]]
- [[04 Synthesis/Bridge/Synthesis - Agent Runtime Layers]]
- [[04 Synthesis/Bridge/Synthesis - Safety, Reliability, and Evals]]
- [[04 Synthesis/Bridge/Synthesis - Memory vs RAG vs Context]]
- [[04 Synthesis/Decision/Synthesis - Agent vs Workflow vs RAG]]
- [[05 Use Cases/Use Cases - MOC|Use Cases - MOC]]
- [[05 Use Cases/Application/Use Cases - Design a RAG System]]
- [[05 Use Cases/Application/Use Cases - Design Guardrails for Tool Use]]
- [[05 Use Cases/Application/Use Cases - Design Memory for an AI Agent]]
- [[05 Use Cases/Application/Use Cases - Evaluate an AI Agent]]
- [[06 Engineering/Engineering - MOC|Engineering - MOC]]

> Detailed implementation subdomains live under [[index]] and [[06 Engineering/Engineering - MOC|Engineering - MOC]].

---

## Workflow And Standards

- [[00 Raw Sources/Raw Sources - MOC|Raw Sources]]
- [[Inbox]]
- [[index]]
- [[AGENTS]]
- [[Knowledge Refactor - Task Board]]
- [[Vault Workflow - Capture to Evergreen]]
- [[_Templates/Standard Note Template|Standard Note Template]]
- [[_Templates/Quick Capture Template|Quick Capture Template]]
- [[Vault Standards - Note Lifecycle]]
- [[Vault Standards - Properties]]
- [[Knowledge Topic Registry]]

ใช้หลักง่าย ๆ:

- แต่ละหมวดมี 1 MOC และใช้ MOC เป็น entry point หลัก
- โน้ตแบบลำดับใช้ชื่อ `NN - หัวข้อ`
- ในหมวด systems ไฟล์ที่มีเลขคือ core learning path ส่วนไฟล์ไม่มีเลขคือ advanced หรือ implementation notes
- โน้ตสังเคราะห์ใช้ชื่อ `Synthesis - ...`
- glossary ใช้สำหรับนิยามศัพท์กลางข้ามหลายหมวด
- note ใหม่เริ่มที่ `draft` ก่อน ถ้ายังเป็น capture ดิบมากค่อยใช้ `seed`
