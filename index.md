---
tags:
  - index
  - catalog
  - navigation
type: index
status: evergreen
source: ""
parent_note: "[[Home]]"
---

# Index

Catalog กลางของ vault นี้สำหรับใช้ค้นหาเนื้อหาแบบเร็ว ทั้งสำหรับคนอ่านและ LLM agent

---

## วิธีใช้

- ถ้าต้องการภาพรวมและ reading path ให้เริ่มที่ [[Home]]
- ถ้าต้องการดูชั้นข้อมูลต้นฉบับ ให้เริ่มที่ [[00 Raw Sources/Raw Sources - MOC|Raw Sources - MOC]]
- ถ้าต้องการดูทั้งหมวดอย่างเป็นระบบ ให้เปิด MOC ของหมวดนั้นก่อน
- ถ้าต้องการหา note เฉพาะ ให้ไล่ตามหมวดด้านล่าง

---

## Raw Sources

- [[00 Raw Sources/Raw Sources - MOC|Raw Sources - MOC]] — หน้าแม่ของชั้นข้อมูลต้นฉบับ
- [[00 Raw Sources/Articles/Articles - README|Articles]] — บทความเว็บ, docs exports, clipped markdown
- [[00 Raw Sources/Articles/Source Manifests - MOC|Source Manifests - MOC]] — entry points สำหรับชุด source ที่ใช้ใน vault แล้ว
- [[00 Raw Sources/Papers/Papers - README|Papers]] — papers, reports, whitepapers
- [[00 Raw Sources/Assets/Assets - README|Assets]] — รูปภาพ, attachments, diagrams, PDFs ประกอบ
- [[00 Raw Sources/Source Records/Source Records - MOC|Source Records - MOC]] — ทะเบียนแหล่งอ้างอิงที่กู้คืนจาก `source:` fields
- [[00 Raw Sources/Source Intake Checklist]] — checklist สำหรับ ingest sources เข้าสู่ wiki

---

## Foundations

### LLM Foundations

- [[01 Foundations/LLM Foundations/LLM Foundations - MOC|LLM Foundations - MOC]] — หน้าแม่ของพื้นฐาน LLM ทั้งหมวด
- [[01 Foundations/LLM Foundations/01 - LLM คืออะไรและพื้นฐาน]] — นิยาม LLM และภาพรวมพื้นฐาน
- [[01 Foundations/LLM Foundations/02 - สถาปัตยกรรม Transformer]] — โครงสร้าง Transformer ระดับแกน
- [[01 Foundations/LLM Foundations/03 - การฝึกและ Post-Training]] — training, fine-tuning, post-training
- [[01 Foundations/LLM Foundations/04 - Inference, Context และ RAG]] — inference runtime, context, และ RAG เบื้องต้น
- [[01 Foundations/LLM Foundations/05 - ข้อจำกัดและการประเมินผล LLM]] — failure modes, evaluation, และข้อจำกัด
- [[01 Foundations/LLM Foundations/06 - Attention และ Representations]] — attention, token interactions, representations
- [[01 Foundations/LLM Foundations/07 - Logits, Decoding และ Sampling]] — decoding, logits, sampling strategies
- [[01 Foundations/LLM Foundations/08 - Data, Pretraining และ Model Modes]] — data pipeline, pretraining, model modes
- [[01 Foundations/LLM Foundations/09 - Serving Metrics และระบบ Production LLM]] — serving, latency, throughput, production metrics
- [[01 Foundations/LLM Foundations/10 - Embeddings และ Semantic Similarity]] — embeddings, similarity, retrieval foundations
- [[01 Foundations/LLM Foundations/11 - Multimodal Foundations]] — multimodal model foundations และ input/output modes
- [[01 Foundations/LLM Foundations/12 - Weights, Context, Retrieval และ Tools]] — แยกความต่างของ 4 แหล่งความสามารถในระบบ LLM
- [[01 Foundations/LLM Foundations/13 - Evaluation Foundations]] — พื้นฐาน evaluation ก่อนลงหมวด Evals
- [[01 Foundations/LLM Foundations/14 - Vector Representations และ Similarity Search]] — vector layer, dense/sparse vectors, และ similarity search

### Prompt Engineering

- [[01 Foundations/Prompt Engineering/Prompt Engineering - MOC|Prompt Engineering - MOC]] — หน้าแม่ของ prompting ทั้งหมวด
- [[01 Foundations/Prompt Engineering/01 - Prompt Engineering คืออะไร]] — แนวคิดพื้นฐานของ prompt engineering
- [[01 Foundations/Prompt Engineering/02 - องค์ประกอบของ Prompt]] — ส่วนประกอบหลักของ prompt
- [[01 Foundations/Prompt Engineering/03 - Prompt Patterns พื้นฐาน]] — รูปแบบ prompt ที่ใช้บ่อย
- [[01 Foundations/Prompt Engineering/04 - หลักการจากหลายบริษัท]] — หลักการ prompting จากหลายผู้ให้บริการ
- [[01 Foundations/Prompt Engineering/05 - Evaluation และ Failure Modes]] — วิธีวัดผลและข้อผิดพลาดของ prompts
- [[01 Foundations/Prompt Engineering/06 - Template และ Common Problems]] — template patterns และปัญหาที่พบบ่อย
- [[01 Foundations/Prompt Engineering/07 - Structured Generation และ Output Formats]] — structured outputs, schemas, output contracts

### Context Windows

- [[01 Foundations/Context Windows/Context Windows - MOC|Context Windows - MOC]] — หน้าแม่ของ context windows ทั้งหมวด
- [[01 Foundations/Context Windows/01 - Context Window คืออะไร]] — นิยาม context window, token budget, context rot
- [[01 Foundations/Context Windows/02 - การบริหารและ Context Engineering]] — layout, token counting, RAG vs long context
- [[01 Foundations/Context Windows/03 - Prompt Caching]] — prompt caching, ROI, และ cost/latency tradeoffs

### Tokenizer in AI

- [[01 Foundations/Tokenizer in AI/Tokenizer in AI - MOC|Tokenizer in AI - MOC]] — หน้าแม่ของ tokenizer ทั้งหมวด
- [[01 Foundations/Tokenizer in AI/01 - Tokenization คืออะไร]] — นิยาม tokenization
- [[01 Foundations/Tokenizer in AI/02 - ประเภทของ Tokenization]] — ประเภทของ tokenization
- [[01 Foundations/Tokenizer in AI/03 - อัลกอริทึม BPE และ Byte-level BPE]] — BPE และ byte-level BPE
- [[01 Foundations/Tokenizer in AI/04 - WordPiece และ SentencePiece]] — WordPiece และ SentencePiece
- [[01 Foundations/Tokenizer in AI/05 - Tokenizer Pipeline]] — pipeline ของ tokenizer
- [[01 Foundations/Tokenizer in AI/06 - ทำไม Tokenization ถึงสำคัญ]] — ผลกระทบของ tokenization ต่อระบบ
- [[01 Foundations/Tokenizer in AI/07 - เปรียบเทียบ Tokenizer รายโมเดล]] — เปรียบเทียบ tokenizer ของโมเดลต่าง ๆ

---

## AI Systems

### AI Agent Fundamentals

- [[02 AI Systems/AI Agent Fundamentals/AI Agent Fundamentals - MOC|AI Agent Fundamentals - MOC]] — หน้าแม่ของ agent fundamentals
- [[02 AI Systems/AI Agent Fundamentals/01 - AI Agent คืออะไร]] — นิยาม agent
- [[02 AI Systems/AI Agent Fundamentals/02 - วิวัฒนาการ LLM สู่ Agent]] — การเปลี่ยนจาก LLM application ไปสู่ agent
- [[02 AI Systems/AI Agent Fundamentals/03 - คุณสมบัติ 5 อย่างของ Agent]] — properties หลักของ agent
- [[02 AI Systems/AI Agent Fundamentals/04 - สถาปัตยกรรม Agent: Model + Tools + Orchestration]] — architecture หลักของ agent
- [[02 AI Systems/AI Agent Fundamentals/05 - วงจร Perceive-Think-Act-Check]] — loop ระดับสูงของ agent
- [[02 AI Systems/AI Agent Fundamentals/06 - วงจร Thought-Action-Observation (TAO)]] — TAO / ReAct-style loop
- [[02 AI Systems/AI Agent Fundamentals/07 - รูปแบบ Agent Architectures]] — patterns ของ agent architectures
- [[02 AI Systems/AI Agent Fundamentals/08 - Workflow vs AI Agent]] — เปรียบเทียบ workflow กับ agent
- [[02 AI Systems/AI Agent Fundamentals/09 - เมื่อไรควรและไม่ควรใช้ Agent]] — decision framework สำหรับเลือกใช้ agent
- [[02 AI Systems/AI Agent Fundamentals/10 - Risks และ Best Practices]] — risks, guardrails, best practices
- [[02 AI Systems/AI Agent Fundamentals/11 - Key Takeaways และ Quick Reference]] — สรุปและ quick reference
- [[02 AI Systems/AI Agent Fundamentals/12 - LLM พื้นฐาน]] — พื้นฐาน LLM ที่จำเป็นต่อการเข้าใจ agent
- [[02 AI Systems/AI Agent Fundamentals/13 - Messages, System Prompt และ Chat Templates]] — runtime message structure และ templates
- [[02 AI Systems/AI Agent Fundamentals/14 - Tools: การออกแบบและทำงาน]] — tool design และ tool execution

### MCP

- [[02 AI Systems/MCP/MCP - MOC|MCP - MOC]] — หน้าแม่ของ Model Context Protocol
- [[02 AI Systems/MCP/Core/01 - MCP คืออะไรและแก้ปัญหาอะไร]] — นิยาม MCP และปัญหา M×N
- [[02 AI Systems/MCP/Core/02 - Architecture: Host, Client, Server]] — architecture ของ host/client/server
- [[02 AI Systems/MCP/Core/03 - Core Primitives: Tools, Resources, Prompts]] — primitives หลักของ MCP
- [[02 AI Systems/MCP/Client/04 - Client Features: Sampling, Roots, Elicitation]] — capabilities ฝั่ง client
- [[02 AI Systems/MCP/Security/05 - Security, Consent และ Authorization]] — security และ consent model
- [[06 Engineering/Recipes/Recipe - HuggingFace MCP Course และ Implementation Guide]] — implementation-oriented guide

### RAG

- [[02 AI Systems/RAG/RAG - MOC|RAG - MOC]] — หน้าแม่ของ retrieval-augmented generation
- [[02 AI Systems/RAG/Core/01 - Retrieval Basics]] — พื้นฐาน retrieval
- [[02 AI Systems/RAG/Core/02 - Chunking Strategies]] — chunking strategies
- [[02 AI Systems/RAG/Core/04 - Query Transformation]] — query rewriting, expansion, decomposition
- [[02 AI Systems/RAG/Core/RAG - Agentic RAG]] — retrieval แบบมี planning, decomposition, และ orchestration
- [[02 AI Systems/RAG/Core/06 - Context Assembly]] — การประกอบ context ก่อนส่งเข้า model
- [[02 AI Systems/RAG/Core/07 - Grounding and Citation]] — grounded answers, citations, evidence traceability
- [[02 AI Systems/RAG/Core/09 - Cost and Latency Tradeoffs]] — trade-offs เชิงระบบของ RAG pipeline
- [[02 AI Systems/RAG/Retrieval/03 - Embeddings and Vector Databases]] — embeddings และ vector DB ใน RAG
- [[02 AI Systems/RAG/Retrieval/RAG - Hybrid Retrieval]] — ผสาน keyword/full-text กับ vector retrieval
- [[02 AI Systems/RAG/Retrieval/RAG - Knowledge Graph RAG]] — retrieval ที่ใช้ graph structures และ knowledge graphs
- [[02 AI Systems/RAG/Retrieval/05 - Reranking]] — reranking layer
- [[02 AI Systems/RAG/Evaluation/08 - Evaluation]] — evaluation สำหรับระบบ RAG

### Memory Systems

- [[02 AI Systems/Memory Systems/Memory Systems - MOC|Memory Systems - MOC]] — หน้าแม่ของ memory systems
- [[02 AI Systems/Memory Systems/Core/01 - Working Memory vs Long-Term Memory]] — ความต่างของ memory ใน context กับ memory ภายนอก
- [[02 AI Systems/Memory Systems/Core/02 - Episodic vs Semantic vs Procedural Memory]] — ประเภทของ memory หลัก
- [[02 AI Systems/Memory Systems/Core/03 - Memory Read and Write Policies]] — กติกาการอ่านและเขียน memory
- [[02 AI Systems/Memory Systems/Application/04 - Agent Memory Patterns]] — รูปแบบ memory ที่ใช้ใน agents
- [[02 AI Systems/Memory Systems/Application/05 - Memory Failure Modes]] — failure modes ของ memory systems

### Agent Frameworks

- [[02 AI Systems/Agent Frameworks/Agent Frameworks - MOC|Agent Frameworks - MOC]] — หน้าแม่ของ agent frameworks
- [[02 AI Systems/Agent Frameworks/Core/01 - Landscape]] — landscape ของ frameworks
- [[02 AI Systems/Agent Frameworks/Core/02 - Framework vs Custom Build]] — framework vs custom build
- [[02 AI Systems/Agent Frameworks/Core/03 - State and Memory]] — state และ memory ใน frameworks
- [[02 AI Systems/Agent Frameworks/Core/04 - Tool Orchestration]] — orchestration ของ tools ใน agent runtimes
- [[06 Engineering/Frameworks/Framework - OpenAI Agents and Responses Patterns]] — มอง OpenAI agent stack ในฐานะ runtime pattern
- [[02 AI Systems/Agent Frameworks/Core/06 - Evaluation and Observability]] — การวัดและสังเกตพฤติกรรมของ agent runtimes
- [[06 Engineering/Frameworks/Framework - LangGraph]] — LangGraph
- [[06 Engineering/Frameworks/Framework - LangChain Agents]] — LangChain agents
- [[06 Engineering/Frameworks/Framework - AutoGen vs CrewAI]] — เปรียบเทียบ AutoGen กับ CrewAI

### Evals

- [[02 AI Systems/Evals/Evals - MOC|Evals - MOC]] — หน้าแม่ของ evaluation systems
- [[02 AI Systems/Evals/Core/01 - Success Criteria]] — ตั้ง success criteria ให้ระบบ
- [[02 AI Systems/Evals/Core/03 - LLM-as-Judge]] — LLM-as-judge patterns และข้อควรระวัง
- [[02 AI Systems/Evals/Application/06 - Prompt Evals]] — prompt evals
- [[02 AI Systems/Evals/Application/07 - RAG Evals]] — RAG evals
- [[02 AI Systems/Evals/Application/08 - Agent Evals]] — agent evals

### Guardrails

- [[02 AI Systems/Guardrails/Guardrails - MOC|Guardrails - MOC]] — หน้าแม่ของ guardrails
- [[02 AI Systems/Guardrails/Core/01 - Input and Output Controls]] — input/output controls
- [[02 AI Systems/Guardrails/Core/03 - Tool Safety]] — ความปลอดภัยในการใช้ tools
- [[02 AI Systems/Guardrails/Core/05 - Fallback Policies]] — fallback, retry, escalation policies
- [[02 AI Systems/Guardrails/Operations/06 - Monitoring and Incidents]] — monitoring และ incident response
- [[02 AI Systems/Guardrails/Operations/04 - Permission Models]] — permission models

### Synthesis

- [[04 Synthesis/Synthesis - MOC|Synthesis - MOC]] — หน้าแม่ของโน้ตสังเคราะห์
- [[04 Synthesis/Synthesis - Agent Runtime Layers]] — runtime layering ของ agent systems
- [[04 Synthesis/Synthesis - Agent vs Workflow vs RAG]] — แยก agent, workflow, และ RAG
- [[04 Synthesis/Synthesis - Memory vs RAG vs Context]] — แยก memory, RAG, และ context
- [[04 Synthesis/Synthesis - Prompting vs Fine-tuning vs RAG]] — เปรียบเทียบ prompting, fine-tuning, และ RAG

### Use Cases

- [[05 Use Cases/Use Cases - MOC|Use Cases - MOC]] — หน้าแม่ของ reading paths แบบใช้งานจริง
- [[05 Use Cases/Use Cases - Build an AI Agent]] — เส้นทางสร้าง agent
- [[05 Use Cases/Use Cases - Choose an Agent Framework]] — เลือก framework จาก runtime needs
- [[05 Use Cases/Use Cases - Design a RAG System]] — ออกแบบ RAG system
- [[05 Use Cases/Use Cases - Design Guardrails for Tool Use]] — วาง guardrails สำหรับ tool use
- [[05 Use Cases/Use Cases - Design Memory for an AI Agent]] — วาง memory สำหรับ agent
- [[05 Use Cases/Use Cases - Evaluate an AI Agent]] — ออกแบบ evals สำหรับ agent
- [[05 Use Cases/Use Cases - Explain MCP Quickly]] — อธิบาย MCP เร็ว ๆ
- [[05 Use Cases/Use Cases - Improve Prompt Reliability]] — ปรับ prompt reliability

### Engineering

- [[06 Engineering/Engineering - MOC|Engineering - MOC]] — หน้าแม่ของ implementation, frameworks, และ project-specific engineering notes
- [[06 Engineering/Architecture to Code/Architecture to Code - MOC|Architecture to Code - MOC]] — แปลง architecture ไปสู่ implementation plan
- [[06 Engineering/Frameworks/Frameworks - MOC|Frameworks - MOC]] — notes ของ frameworks ที่เปลี่ยนตาม ecosystem
- [[06 Engineering/RAG/RAG - MOC|RAG - MOC]] — implementation ของ retrieval pipeline
- [[06 Engineering/Guardrails/Guardrails - MOC|Guardrails - MOC]] — implementation ของ validation, review gates, และ policy enforcement
- [[06 Engineering/Evals/Evals - MOC|Evals - MOC]] — implementation ของ eval harness และ regression gates
- [[06 Engineering/MCP/MCP - MOC|MCP - MOC]] — implementation ของ MCP integration
- [[06 Engineering/Memory/Memory - MOC|Memory - MOC]] — implementation ของ memory layer
- [[06 Engineering/Patterns/Patterns - MOC|Patterns - MOC]] — reusable coding patterns
- [[06 Engineering/Recipes/Recipes - MOC|Recipes - MOC]] — step-by-step implementation notes
- [[06 Engineering/Decisions/Decisions - MOC|Decisions - MOC]] — architecture และ implementation decisions
- [[06 Engineering/Project Notes/Project Notes - MOC|Project Notes - MOC]] — notes ผูกกับระบบหรือ project เฉพาะ

---

## Tools

### Claude Code

- [[03 Tools/Claude Code/Claude Code - Multi-Agent MOC|Claude Code - Multi-Agent MOC]] — หน้าแม่ของ Claude Code
- [[03 Tools/Claude Code/01 - Claude Code คืออะไร]] — ภาพรวม Claude Code
- [[03 Tools/Claude Code/02 - เปรียบเทียบ Agentic Coding Tools]] — เปรียบเทียบเครื่องมือ coding agents
- [[03 Tools/Claude Code/03 - Orchestrator Pattern]] — orchestrator pattern
- [[03 Tools/Claude Code/04 - 1 Session vs Subagents vs Agent Teams]] — รูปแบบการแบ่งงานของ agents
- [[03 Tools/Claude Code/05 - รูปแบบการใช้งาน Multi-Agent]] — การใช้งาน multi-agent
- [[03 Tools/Claude Code/06 - การควบคุมต้นทุน]] — cost control
- [[03 Tools/Claude Code/07 - การติดตั้งและเริ่มใช้งาน]] — setup และ getting started
- [[03 Tools/Claude Code/08 - Display Mode (In-Process vs Split Panes)]] — display modes
- [[03 Tools/Claude Code/09 - Permissions และ Settings]] — permissions และ settings
- [[03 Tools/Claude Code/10 - Session Management และ Commands]] — session management และ commands
- [[03 Tools/Claude Code/11 - โครงสร้างโฟลเดอร์ .claude]] — โครงสร้าง `.claude`
- [[03 Tools/Claude Code/12 - CLAUDE File]] — ไฟล์ `CLAUDE`
- [[03 Tools/Claude Code/13 - Custom Commands]] — custom commands
- [[03 Tools/Claude Code/14 - Built-in Subagents]] — built-in subagents
- [[03 Tools/Claude Code/15 - สร้าง Subagent ด้วย agents]] — การสร้าง subagents
- [[03 Tools/Claude Code/16 - บทบาท Frontend, Backend, QA]] — role-based agents
- [[03 Tools/Claude Code/17 - Agent Tool]] — agent tool
- [[03 Tools/Claude Code/18 - Git Worktree]] — git worktree workflow
- [[03 Tools/Claude Code/19 - วิธีเริ่ม Agent Team]] — เริ่ม agent team
- [[03 Tools/Claude Code/20 - Multi-Provider AI]] — multi-provider setup
- [[03 Tools/Claude Code/21 - กรณีศึกษา]] — case studies
- [[03 Tools/Claude Code/22 - Error Handling]] — error handling
- [[03 Tools/Claude Code/23 - ข้อจำกัด Agent Teams]] — limitations ของ agent teams
- [[03 Tools/Claude Code/24 - Best Practices & Checklist]] — best practices และ checklist

---

## Synthesis

- [[04 Synthesis/Synthesis - Agent vs Workflow vs RAG]] — เปรียบเทียบ 3 แนวทางหลักของระบบ LLM
- [[04 Synthesis/Synthesis - Agent Runtime Layers]] — แยกชั้น runtime ของระบบ agent ให้เห็นภาพรวม
- [[04 Synthesis/Synthesis - LLM to Agent Stack]] — แผนที่จาก LLM ไปสู่ agent stack
- [[04 Synthesis/Synthesis - Safety, Reliability, and Evals]] — เชื่อม safety controls เข้ากับ reliability และ evaluation
- [[04 Synthesis/Synthesis - Memory vs RAG vs Context]] — แยกหน้าที่ของ context, memory, และ RAG
- [[04 Synthesis/Synthesis - Memory in Agents]] — memory patterns ใน agents
- [[04 Synthesis/Synthesis - Prompting vs Fine-tuning vs RAG]] — เปรียบเทียบ 3 วิธีปรับระบบให้ดีขึ้น
- [[Glossary - AI Systems]] — glossary กลางของศัพท์ข้ามหมวด

---

## Use Cases

- [[05 Use Cases/Use Cases - Build an AI Agent]] — เส้นทางใช้งานจริงในการสร้าง agent
- [[05 Use Cases/Use Cases - Choose an Agent Framework]] — วิธีคิดเลือก framework จาก runtime needs
- [[05 Use Cases/Use Cases - Design a RAG System]] — วิธีคิดออกแบบ retrieval pipeline, grounding, และ evaluation ของ RAG
- [[05 Use Cases/Use Cases - Design Guardrails for Tool Use]] — วิธีวาง guardrails สำหรับ tools, permissions, และ fallback
- [[05 Use Cases/Use Cases - Design Memory for an AI Agent]] — วิธีแยก memory, RAG, และ context ในระบบ agent
- [[05 Use Cases/Use Cases - Evaluate an AI Agent]] — วิธีออกแบบ evals สำหรับ agent ที่มี tools, state, และ safety constraints
- [[05 Use Cases/Use Cases - Explain MCP Quickly]] — อธิบาย MCP อย่างรวดเร็ว
- [[05 Use Cases/Use Cases - Improve Prompt Reliability]] — ปรับปรุง reliability ของ prompts

---

## Standards And Workflow

- [[Home]] — หน้าเริ่มต้นของ vault
- [[AGENTS]] — schema กลางสำหรับ agent ที่ดูแล vault นี้
- [[Inbox]] — จุดรับไอเดียหรือความรู้ดิบ
- [[Vault Workflow - Capture to Evergreen]] — workflow จาก capture ไปสู่ evergreen notes
- [[Vault Standards - Note Lifecycle]] — มาตรฐาน `seed / draft / evergreen`
- [[Vault Standards - Properties]] — สเปกของ properties/frontmatter
- [[_Templates/Standard Note Template|Standard Note Template]] — template สำหรับ note ปกติ
- [[_Templates/Quick Capture Template|Quick Capture Template]] — template สำหรับ quick capture

---

## หมายเหตุ

- `Home.md` ทำหน้าที่เป็น landing page และ reading paths
- `index.md` ทำหน้าที่เป็น catalog กลางของทั้ง vault
- MOC แต่ละหมวดใช้สำหรับนำทางภายใน domain นั้นโดยเฉพาะ
