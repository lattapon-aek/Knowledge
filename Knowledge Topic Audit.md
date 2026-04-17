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

## Action Summary

สรุปภาพรวมจาก audit รอบนี้:

| Layer | Action | หมายเหตุ |
|---|---|---|
| `01 Foundations` | stay | เป็นฐาน primitives ที่นิ่ง |
| `02 AI Systems` | stay | แยก owner ย่อยชัดแล้ว: agent runtime, framework, memory, RAG, guardrails, evals, MCP |
| `04 Synthesis` | stay | เป็น bridge / comparison / decision layer |
| `05 Use Cases` | stay | เป็น decision path / application layer |
| `06 Engineering` | stay | เป็น implementation / recipe / project layer |
| `03 Tools/Claude Code` | stay | เป็น volatile tool layer |
| Bridge notes | keep | ใช้เฉพาะจุดที่ต้องเชื่อมข้าม topic |
| Move candidates | none in this pass | ยังไม่ต้องย้ายเนื้อหาหลักก่อนเริ่ม phase ใหม่ |

### Phase Status

- Phase 0 (`Foundations / base primitives`) = reviewed, no moves needed
- Phase 1 (`Agent runtime`) = reviewed, no moves needed
- Phase 2 (`Framework selection`) = reviewed, no moves needed
- Phase 3 (`Memory architecture`) = reviewed, no moves needed
- Phase 4 (`Retrieval / RAG`) = reviewed, no moves needed
- Phase 5 (`Guardrails / control`) = reviewed, no moves needed
- Phase 6 (`Evaluation`) = reviewed, no moves needed
- Phase 7 (`Use case decisions`) = reviewed, no moves needed
- Phase 8 (`Bridge / synthesis`) = reviewed, no moves needed
- Phase 9 (`Implementation`) = reviewed, no moves needed
- Phase 10 (`Claude Code / tooling`) = reviewed, no moves needed
- Execution จะเดินตามลำดับใน section `Execution Order`

### Bridge Notes ที่ควรคงไว้

- `AI Agent Fundamentals/12, 13, 14`
- `Synthesis - Memory in Agents`
- `Synthesis - Memory vs RAG vs Context`
- `Synthesis - Agent vs Workflow vs RAG`
- `Synthesis - Agent Runtime Layers`
- `Synthesis - LLM to Agent Stack`
- `Synthesis - Safety, Reliability, and Evals`
- `Synthesis - Single to Multi-Agent Infrastructure`

### Move Candidates ในอนาคต

- ไม่มีไฟล์ที่ต้อง move ทันทีในรอบนี้
- ถ้าจะ re-categorize ในรอบถัดไป ให้เริ่มจากการปรับลิงก์/bridge ก่อน แล้วค่อยพิจารณาย้ายเฉพาะกรณีที่ owner ยังไม่ชัด

---

## Execution Order

ลำดับลงมือจริงสำหรับรอบ re-categorize:

1. `01 Foundations`
   - ยืนยันว่า `LLM / prompt / context / tokenizer` อยู่ที่ owner เดิม
   - bridge notes คงไว้ ไม่ต้องย้าย

2. `02 AI Systems / AI Agent Fundamentals`
   - ตรวจว่า `12 / 13 / 14` เป็น bridge notes จริง
   - ยืน boundary ระหว่าง agent runtime กับ foundations / engineering

3. `02 AI Systems / Agent Frameworks`
   - คง framework selection ไว้ที่นี่
   - implementation notes อยู่ `06 Engineering`

4. `02 AI Systems / Memory Systems`
   - คง memory architecture / policy ไว้ที่นี่
   - bridge กับ `RAG` และ `Agent Frameworks` เท่านั้น

5. `02 AI Systems / RAG`
   - คง retrieval / grounding / evaluation ที่เกี่ยวกับ RAG ไว้ที่นี่
   - bridge กับ `Memory Systems` และ `Evals`

6. `02 AI Systems / Guardrails`
   - คง control layer ไว้ที่นี่
   - bridge ไป `Evals` เฉพาะกรณี measurement

7. `02 AI Systems / Evals`
   - คง measurement layer ไว้ที่นี่
   - bridge กลับไป `Guardrails` เฉพาะ policy implication

8. `02 AI Systems / MCP`
   - คง protocol layer ไว้ที่นี่
   - bridge ไป `AI Agent Fundamentals` และ `06 Engineering` ตาม context

9. `04 Synthesis`
   - ใช้เป็น bridge / compare / decision summary
   - ไม่ต้องย้ายถ้าเป็น synthesis จริง

10. `05 Use Cases`
    - ใช้เป็น decision path / application entry
    - ไม่ต้องย้ายถ้าเป็น use case จริง

11. `06 Engineering`
    - คง implementation, recipes, decisions, project notes ไว้
    - ถ้าเจอ theory ซ้ำ ค่อยระบุ bridge กลับไป owner

12. `03 Tools/Claude Code`
    - เก็บท้ายสุด
    - คงเป็น volatile tool layer

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

## File Audit: 01 Foundations

| File | Current Role | Recommended Owner | Action |
|---|---|---|---|
| `LLM Foundations - MOC` | canonical owner | `01 Foundations/LLM Foundations` | stay |
| `01 - LLM คืออะไรและพื้นฐาน` | core foundational note | `01 Foundations/LLM Foundations` | stay |
| `02 - สถาปัตยกรรม Transformer` | core foundational note | `01 Foundations/LLM Foundations` | stay |
| `03 - การฝึกและ Post-Training` | core foundational note | `01 Foundations/LLM Foundations` | stay |
| `04 - Inference, Context และ RAG` | inference / runtime foundation | `01 Foundations/LLM Foundations` | stay; bridge to Context/RAG |
| `05 - ข้อจำกัดและการประเมินผล LLM` | limitation / eval primitive | `01 Foundations/LLM Foundations` | stay; bridge to Evals |
| `06 - Attention และ Representations` | core foundational note | `01 Foundations/LLM Foundations` | stay |
| `07 - Logits, Decoding และ Sampling` | core foundational note | `01 Foundations/LLM Foundations` | stay |
| `08 - Data, Pretraining และ Model Modes` | core foundational note | `01 Foundations/LLM Foundations` | stay |
| `09 - Serving Metrics และระบบ Production LLM` | production foundation | `01 Foundations/LLM Foundations` | stay |
| `10 - Embeddings และ Semantic Similarity` | representation foundation | `01 Foundations/LLM Foundations` | stay; bridge to RAG |
| `11 - Multimodal Foundations` | multimodal foundation | `01 Foundations/LLM Foundations` | stay |
| `12 - Weights, Context, Retrieval และ Tools` | bridge note | `01 Foundations/LLM Foundations` | keep as bridge |
| `13 - Evaluation Foundations` | eval primitive | `01 Foundations/LLM Foundations` | stay; bridge to Evals |
| `14 - Vector Representations และ Similarity Search` | representation foundation | `01 Foundations/LLM Foundations` | stay; bridge to RAG |

---

## File Audit: 02 AI Systems / AI Agent Fundamentals

| File | Current Role | Recommended Owner | Action |
|---|---|---|---|
| `AI Agent Fundamentals - MOC` | canonical owner | `02 AI Systems/AI Agent Fundamentals` | stay |
| `01 - AI Agent คืออะไร` | core runtime concept | `02 AI Systems/AI Agent Fundamentals` | stay |
| `02 - วิวัฒนาการ LLM สู่ Agent` | core runtime concept | `02 AI Systems/AI Agent Fundamentals` | stay |
| `03 - คุณสมบัติ 5 อย่างของ Agent` | core runtime concept | `02 AI Systems/AI Agent Fundamentals` | stay |
| `04 - สถาปัตยกรรม Agent: Model + Tools + Orchestration` | core runtime concept | `02 AI Systems/AI Agent Fundamentals` | stay |
| `05 - วงจร Perceive-Think-Act-Check` | core runtime loop | `02 AI Systems/AI Agent Fundamentals` | stay |
| `06 - วงจร Thought-Action-Observation (TAO)` | core runtime loop | `02 AI Systems/AI Agent Fundamentals` | stay |
| `07 - รูปแบบ Agent Architectures` | architecture concept | `02 AI Systems/AI Agent Fundamentals` | stay |
| `08 - Workflow vs AI Agent` | decision / comparison note | `02 AI Systems/AI Agent Fundamentals` | stay; bridge to Use Cases / Synthesis |
| `09 - เมื่อไรควรและไม่ควรใช้ Agent` | decision note | `02 AI Systems/AI Agent Fundamentals` | stay; bridge to Use Cases |
| `10 - Risks และ Best Practices` | runtime risk note | `02 AI Systems/AI Agent Fundamentals` | stay; bridge to Guardrails / Evals |
| `11 - Key Takeaways และ Quick Reference` | summary / reference | `02 AI Systems/AI Agent Fundamentals` | stay |
| `12 - LLM พื้นฐาน` | bridge note | `01 Foundations/LLM Foundations` | keep as bridge |
| `13 - Messages, System Prompt และ Chat Templates` | bridge note | `01 Foundations/Prompt Engineering` + `01 Foundations/Context Windows` | keep as bridge |
| `14 - Tools: การออกแบบและทำงาน` | bridge note | `02 AI Systems/MCP` + `06 Engineering` | keep as bridge |

---

## File Audit: 02 AI Systems / Agent Frameworks

| File | Current Role | Recommended Owner | Action |
|---|---|---|---|
| `Agent Frameworks - MOC` | canonical owner | `02 AI Systems/Agent Frameworks` | stay |
| `Core/01 - Landscape` | framework landscape overview | `02 AI Systems/Agent Frameworks` | stay |
| `Core/02 - Framework vs Custom Build` | decision / comparison note | `02 AI Systems/Agent Frameworks` | stay; bridge to Use Cases / Engineering |
| `Core/03 - State and Memory` | framework runtime concept | `02 AI Systems/Agent Frameworks` | stay; bridge to Memory Systems |
| `Core/04 - Tool Orchestration` | framework runtime concept | `02 AI Systems/Agent Frameworks` | stay; bridge to AI Agent Fundamentals / Engineering |
| `Core/06 - Evaluation and Observability` | framework runtime concept | `02 AI Systems/Agent Frameworks` | stay; bridge to Evals |
| `Core/07 - Checkpointing and Resumability` | framework runtime concept | `02 AI Systems/Agent Frameworks` | stay; bridge to Memory Systems / Engineering |
| `06 Engineering/Frameworks/Framework - LangGraph` | implementation note | `06 Engineering/Frameworks` | stay in engineering |
| `06 Engineering/Frameworks/Framework - LangChain Agents` | implementation note | `06 Engineering/Frameworks` | stay in engineering |
| `06 Engineering/Frameworks/Framework - AutoGen vs CrewAI` | implementation note | `06 Engineering/Frameworks` | stay in engineering |
| `06 Engineering/Frameworks/Framework - OpenAI Agents and Responses Patterns` | implementation note | `06 Engineering/Frameworks` | stay in engineering |

---

## File Audit: 02 AI Systems / Memory Systems

| File | Current Role | Recommended Owner | Action |
|---|---|---|---|
| `Memory Systems - MOC` | canonical owner | `02 AI Systems/Memory Systems` | stay |
| `Core/01 - Working Memory vs Long-Term Memory` | core memory concept | `02 AI Systems/Memory Systems` | stay |
| `Core/02 - Episodic vs Semantic vs Procedural Memory` | core memory taxonomy | `02 AI Systems/Memory Systems` | stay |
| `Core/03 - Memory Read and Write Policies` | core memory policy | `02 AI Systems/Memory Systems` | stay |
| `Core/06 - Memory Retrieval vs RAG` | bridge note | `02 AI Systems/Memory Systems` | keep as bridge to RAG |
| `Application/04 - Agent Memory Patterns` | application pattern | `02 AI Systems/Memory Systems` | stay; bridge to Agent Frameworks / Use Cases |
| `Application/05 - Memory Failure Modes` | risk / failure note | `02 AI Systems/Memory Systems` | stay; bridge to Evals / Guardrails |

---

## File Audit: 02 AI Systems / RAG

| File | Current Role | Recommended Owner | Action |
|---|---|---|---|
| `RAG - MOC` | canonical owner | `02 AI Systems/RAG` | stay |
| `Core/01 - Retrieval Basics` | core retrieval concept | `02 AI Systems/RAG` | stay |
| `Core/02 - Chunking Strategies` | core retrieval concept | `02 AI Systems/RAG` | stay |
| `Retrieval/03 - Embeddings and Vector Databases` | retrieval infrastructure concept | `02 AI Systems/RAG` | stay |
| `Core/04 - Query Transformation` | retrieval pipeline concept | `02 AI Systems/RAG` | stay |
| `Retrieval/05 - Reranking` | retrieval pipeline concept | `02 AI Systems/RAG` | stay |
| `Core/06 - Context Assembly` | retrieval pipeline concept | `02 AI Systems/RAG` | stay |
| `Core/07 - Grounding and Citation` | grounding concept | `02 AI Systems/RAG` | stay |
| `Evaluation/08 - Evaluation` | RAG evaluation concept | `02 AI Systems/RAG` + `02 AI Systems/Evals` | stay; bridge to Evals |
| `Core/09 - Cost and Latency Tradeoffs` | operational RAG concept | `02 AI Systems/RAG` | stay |
| `Core/RAG - Agentic RAG` | advanced RAG concept | `02 AI Systems/RAG` | stay |
| `Retrieval/RAG - Hybrid Retrieval` | advanced retrieval pattern | `02 AI Systems/RAG` | stay |
| `Retrieval/RAG - Knowledge Graph RAG` | advanced retrieval pattern | `02 AI Systems/RAG` | stay |

---

## File Audit: 02 AI Systems / Guardrails

| File | Current Role | Recommended Owner | Action |
|---|---|---|---|
| `Guardrails - MOC` | canonical owner | `02 AI Systems/Guardrails` | stay |
| `Core/01 - Input and Output Controls` | core control concept | `02 AI Systems/Guardrails` | stay |
| `Core/Guardrails - Prompt Injection and Content Attacks` | core safety concept | `02 AI Systems/Guardrails` | stay |
| `Core/02 - Output Validation` | core control concept | `02 AI Systems/Guardrails` | stay |
| `Core/03 - Tool Safety` | core control concept | `02 AI Systems/Guardrails` | stay |
| `Operations/04 - Permission Models` | operational control concept | `02 AI Systems/Guardrails` | stay |
| `Core/05 - Fallback Policies` | operational control concept | `02 AI Systems/Guardrails` | stay |
| `Operations/06 - Monitoring and Incidents` | operational control concept | `02 AI Systems/Guardrails` | stay |
| `Core/07 - Safety vs Usability Tradeoffs` | decision / tradeoff concept | `02 AI Systems/Guardrails` | stay |

---

## File Audit: 02 AI Systems / Evals

| File | Current Role | Recommended Owner | Action |
|---|---|---|---|
| `Evals - MOC` | canonical owner | `02 AI Systems/Evals` | stay |
| `Core/01 - Success Criteria` | core evaluation concept | `02 AI Systems/Evals` | stay |
| `Core/02 - Benchmark Design` | core evaluation concept | `02 AI Systems/Evals` | stay |
| `Core/03 - LLM-as-Judge` | core evaluation concept | `02 AI Systems/Evals` | stay |
| `Core/04 - Human Evaluation` | core evaluation concept | `02 AI Systems/Evals` | stay |
| `Core/05 - Regression Testing` | core evaluation concept | `02 AI Systems/Evals` | stay |
| `Core/09 - Observability and Feedback Loops` | operational evaluation concept | `02 AI Systems/Evals` | stay |
| `Application/06 - Prompt Evals` | applied evaluation note | `02 AI Systems/Evals` | stay |
| `Application/07 - RAG Evals` | applied evaluation note | `02 AI Systems/Evals` | stay |
| `Application/08 - Agent Evals` | applied evaluation note | `02 AI Systems/Evals` | stay |
| `Application/09 - Multi-Agent Evals` | applied evaluation note | `02 AI Systems/Evals` | stay |

---

## File Audit: 02 AI Systems / MCP

| File | Current Role | Recommended Owner | Action |
|---|---|---|---|
| `MCP - MOC` | canonical owner | `02 AI Systems/MCP` | stay |
| `Core/01 - MCP คืออะไรและแก้ปัญหาอะไร` | protocol concept | `02 AI Systems/MCP` | stay |
| `Core/02 - Architecture: Host, Client, Server` | protocol architecture | `02 AI Systems/MCP` | stay |
| `Core/03 - Core Primitives: Tools, Resources, Prompts` | protocol primitives | `02 AI Systems/MCP` | stay |
| `Client/04 - Client Features: Sampling, Roots, Elicitation` | client capability note | `02 AI Systems/MCP` | stay |
| `Security/05 - Security, Consent และ Authorization` | protocol security note | `02 AI Systems/MCP` | stay |

---

## File Audit: 04 Synthesis

| File | Current Role | Recommended Owner | Action |
|---|---|---|---|
| `Synthesis - MOC` | canonical owner | `04 Synthesis` | stay |
| `Synthesis - Agent Runtime Layers` | bridge / stack view | `04 Synthesis` | stay |
| `Synthesis - Agent vs Workflow vs RAG` | comparison / decision bridge | `04 Synthesis` | stay |
| `Synthesis - LLM to Agent Stack` | stack / bridge view | `04 Synthesis` | stay |
| `Synthesis - Memory in Agents` | bridge note | `04 Synthesis` | stay |
| `Synthesis - Memory vs RAG vs Context` | bridge / decision note | `04 Synthesis` | stay |
| `Synthesis - Prompting vs Fine-tuning vs RAG` | comparison / decision bridge | `04 Synthesis` | stay |
| `Synthesis - Safety, Reliability, and Evals` | bridge / control synthesis | `04 Synthesis` | stay |
| `Synthesis - Single to Multi-Agent Infrastructure` | bridge / architecture synthesis | `04 Synthesis` | stay |
| `Synthesis - Multi-Agent Failure Modes` | bridge / negative index | `04 Synthesis` | stay |

---

## File Audit: 05 Use Cases

| File | Current Role | Recommended Owner | Action |
|---|---|---|---|
| `Use Cases - MOC` | canonical owner | `05 Use Cases` | stay |
| `Use Cases - Build an AI Agent` | application / decision path | `05 Use Cases` | stay |
| `Use Cases - Choose an Agent Framework` | application / decision path | `05 Use Cases` | stay |
| `Use Cases - Design a RAG System` | application / decision path | `05 Use Cases` | stay |
| `Use Cases - Design Guardrails for Tool Use` | application / decision path | `05 Use Cases` | stay |
| `Use Cases - Design Memory for an AI Agent` | application / decision path | `05 Use Cases` | stay |
| `Use Cases - Evaluate an AI Agent` | application / decision path | `05 Use Cases` | stay |
| `Use Cases - Explain MCP Quickly` | application / decision path | `05 Use Cases` | stay |
| `Use Cases - Improve Prompt Reliability` | application / decision path | `05 Use Cases` | stay |
| `Use Cases - Move from Single to Multi-Agent` | application / decision path | `05 Use Cases` | stay |

---

## File Audit: 06 Engineering

| File | Current Role | Recommended Owner | Action |
|---|---|---|---|
| `Engineering - MOC` | canonical owner | `06 Engineering` | stay |
| `README.md` | vault documentation | `06 Engineering` / repo docs | stay |
| `Architecture to Code/Architecture - Multi-Agent Infrastructure` | implementation architecture | `06 Engineering/Architecture to Code` | stay |
| `Architecture to Code/Architecture - Multi-Agent Ownership and Handoffs` | implementation architecture | `06 Engineering/Architecture to Code` | stay |
| `Architecture to Code/Architecture - Multi-Agent Security and Permissions` | implementation architecture | `06 Engineering/Architecture to Code` | stay |
| `Architecture to Code/Architecture - Multi-Agent Deployment and Topology` | implementation architecture | `06 Engineering/Architecture to Code` | stay |
| `Architecture to Code/Architecture - Tool Schemas and Runtime Integration` | implementation architecture | `06 Engineering/Architecture to Code` | stay |
| `Frameworks/Framework - LangGraph` | framework implementation note | `06 Engineering/Frameworks` | stay |
| `Frameworks/Framework - LangChain Agents` | framework implementation note | `06 Engineering/Frameworks` | stay |
| `Frameworks/Framework - AutoGen vs CrewAI` | framework implementation note | `06 Engineering/Frameworks` | stay |
| `Frameworks/Framework - OpenAI Agents and Responses Patterns` | framework implementation note | `06 Engineering/Frameworks` | stay |
| `Patterns/Pattern - Retry and Backoff` | reusable implementation pattern | `06 Engineering/Patterns` | stay |
| `Patterns/Pattern - Sync vs Async Agent Communication` | reusable implementation pattern | `06 Engineering/Patterns` | stay |
| `Recipes/Recipe - Add a New Framework Note` | recipe / maintenance note | `06 Engineering/Recipes` | stay |
| `Recipes/Recipe - Build a RAG Pipeline` | recipe note | `06 Engineering/Recipes` | stay |
| `Recipes/Recipe - Add MCP Server Integration` | recipe note | `06 Engineering/Recipes` | stay |
| `Recipes/Recipe - Add Output Validation` | recipe note | `06 Engineering/Recipes` | stay |
| `Recipes/Recipe - Add a Memory Layer` | recipe note | `06 Engineering/Recipes` | stay |
| `Recipes/Recipe - Build an Eval Harness` | recipe note | `06 Engineering/Recipes` | stay |
| `Recipes/Recipe - HuggingFace MCP Course และ Implementation Guide` | derived implementation guide | `06 Engineering/Recipes` | stay; derived |
| `Decisions/Decision - Choose a Framework` | engineering decision note | `06 Engineering/Decisions` | stay |
| `Decisions/Decision - Choose a Retrieval Strategy` | engineering decision note | `06 Engineering/Decisions` | stay |
| `Decisions/Decision - Choose a Validation Boundary` | engineering decision note | `06 Engineering/Decisions` | stay |
| `Decisions/Decision - Choose an Evaluation Gate` | engineering decision note | `06 Engineering/Decisions` | stay |
| `Decisions/Decision - Choose MCP Integration Boundary` | engineering decision note | `06 Engineering/Decisions` | stay |
| `Decisions/Decision - Choose a Memory Policy` | engineering decision note | `06 Engineering/Decisions` | stay |
| `Project Notes/Project Note - Example Implementation Log` | project note | `06 Engineering/Project Notes` | stay |

---

## File Audit: 03 Tools / Claude Code

| File | Current Role | Recommended Owner | Action |
|---|---|---|---|
| `Claude Code - Multi-Agent MOC` | canonical owner | `03 Tools/Claude Code` | stay |
| `01 - Claude Code คืออะไร` | stable concept / tool intro | `03 Tools/Claude Code` | stay |
| `02 - เปรียบเทียบ Agentic Coding Tools` | stable comparison note | `03 Tools/Claude Code` | stay |
| `03 - Orchestrator Pattern` | stable concept note | `03 Tools/Claude Code` | stay |
| `04 - 1 Session vs Subagents vs Agent Teams` | volatile workflow note | `03 Tools/Claude Code` | stay |
| `05 - รูปแบบการใช้งาน Multi-Agent` | stable concept note | `03 Tools/Claude Code` | stay |
| `06 - การควบคุมต้นทุน` | stable concept note | `03 Tools/Claude Code` | stay |
| `07 - การติดตั้งและเริ่มใช้งาน` | volatile setup note | `03 Tools/Claude Code` | stay |
| `08 - Display Mode (In-Process vs Split Panes)` | volatile setup note | `03 Tools/Claude Code` | stay |
| `09 - Permissions และ Settings` | volatile setup note | `03 Tools/Claude Code` | stay |
| `10 - Session Management และ Commands` | volatile workflow note | `03 Tools/Claude Code` | stay |
| `11 - โครงสร้างโฟลเดอร์ .claude.md` | volatile workflow note | `03 Tools/Claude Code` | stay |
| `12 - CLAUDE File` | volatile workflow note | `03 Tools/Claude Code` | stay |
| `13 - Custom Commands` | volatile workflow note | `03 Tools/Claude Code` | stay |
| `14 - Built-in Subagents` | volatile workflow note | `03 Tools/Claude Code` | stay |
| `15 - สร้าง Subagent ด้วย agents.md` | volatile workflow note | `03 Tools/Claude Code` | stay |
| `16 - บทบาท Frontend, Backend, QA` | stable concept note | `03 Tools/Claude Code` | stay |
| `17 - Agent Tool` | volatile tool note | `03 Tools/Claude Code` | stay |
| `18 - Git Worktree` | volatile workflow note | `03 Tools/Claude Code` | stay |
| `19 - วิธีเริ่ม Agent Team` | volatile workflow note | `03 Tools/Claude Code` | stay |
| `20 - Multi-Provider AI` | stable concept note | `03 Tools/Claude Code` | stay |
| `21 - กรณีศึกษา` | stable case note | `03 Tools/Claude Code` | stay |
| `22 - Error Handling` | volatile workflow note | `03 Tools/Claude Code` | stay |
| `23 - ข้อจำกัด Agent Teams` | volatile workflow note | `03 Tools/Claude Code` | stay |
| `24 - Best Practices & Checklist` | volatile reference note | `03 Tools/Claude Code` | stay |

---

## Use With Registry

- อ่านหน้านี้คู่กับ `Knowledge Topic Registry`
- ใช้ Registry เป็นแผนที่ owner
- ใช้ Audit นี้เป็น checklist ว่า topic ไหนควร stay, bridge, หรือ move

---

## Final Summary

ผลสรุปรอบ audit แรก:

- `01 Foundations` = stay
- `02 AI Systems` = stay
- `04 Synthesis` = stay
- `05 Use Cases` = stay
- `06 Engineering` = stay
- `03 Tools/Claude Code` = stay

### สิ่งที่คงไว้

- bridge notes ที่ตั้งใจให้เชื่อมข้าม topic
- implementation notes ที่อยู่ใน `06 Engineering`
- volatile tool notes ที่อยู่ใน `03 Tools/Claude Code`

### สิ่งที่ยังไม่ต้องย้าย

- ไม่มี move candidate ที่ต้องย้ายเนื้อหาหลักในรอบนี้

### สิ่งที่ใช้ต่อรอบหน้า

- `Knowledge Topic Registry` = แผนที่ owner
- `Knowledge Topic Audit` = checklist สำหรับดูว่าเรื่องไหน stay / bridge / move
- `Knowledge Refactor - Task Board` = แผนงานกลางของ phase ถัดไป

### Bridge Note Check เริ่มต้น

รอบเริ่มต้นของ recategorization ตรวจ bridge notes หลักแล้ว:

- `AI Agent Fundamentals/12 - LLM พื้นฐาน` = keep as bridge
- `AI Agent Fundamentals/13 - Messages, System Prompt และ Chat Templates` = keep as bridge
- `AI Agent Fundamentals/14 - Tools: การออกแบบและทำงาน` = keep as bridge

ผลสรุป:
- bridge notes เหล่านี้ยังไม่ใช่ move candidates
- บทบาทของมันคือเชื่อม `01 Foundations` / `02 AI Systems` / `06 Engineering` ให้ชัด
- รอบถัดไปค่อยประเมิน bridge note อื่น ๆ ทีละ topic ตาม execution order
