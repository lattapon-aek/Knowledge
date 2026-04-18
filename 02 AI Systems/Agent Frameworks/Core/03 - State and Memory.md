---
tags:
  - agents
  - frameworks
  - state
  - memory
type: note
status: evergreen
source: "LangGraph Persistence Docs · Google ADK Sessions and Memory Docs · AutoGen Core Docs · Semantic Kernel Agent Framework Docs"
parent_note: "[[Agent Frameworks - MOC]]"
---

# Agent Frameworks - State and Memory

## ภาพรวม

framework แตกต่างกันมากตรงวิธีเก็บ state, resume execution, checkpoint, และ external memory integration

---

## ขอบเขต

- transient state
- persistent state
- checkpointing
- resumability
- memory interfaces

---

## ทำไม state และ memory เป็นแกนสำคัญ

agent systems ที่ซับซ้อนแทบทุกระบบต้องตอบคำถาม:
- state ตอนนี้อยู่ที่ไหน
- state นี้อยู่ได้แค่ turn เดียวหรือข้าม thread ได้
- resume จากจุดเดิมได้ไหม
- memory ระยะยาวเชื่อมเข้ามายังไง
- ใครเป็นคนควบคุม lifecycle ของ state

frameworks จึงต่างกันมากตรงนี้ เพราะ state model เป็นหัวใจของ runtime

```mermaid
flowchart TD
    A[Current turn context] --> B[Session / Thread State]
    B --> C[Checkpoint / Persistence]
    C --> D[Long-Term Memory]
    D --> E[Future turns]
```

---

## แยก State ออกจาก Memory ก่อน

ในกรอบของ vault นี้:

- `working memory` = current context
- `session state` = ข้อมูลที่ต้องคงอยู่ใน thread/runtime เดิม
- `long-term memory` = persistent recallable knowledge ข้าม sessions

framework หลายตัวรองรับสองอย่างแรกชัดเจน แต่ long-term memory มักต้อง integrate เพิ่ม

Google ADK แยก `Session`, `State`, และ `Memory` อย่างชัดเจน  
LangGraph docs เน้น persistence และ cross-thread memory/store  
AutoGen docs เน้น stateful agents และ runtime/message lifecycles  
Semantic Kernel วาง kernel เป็นศูนย์กลางของ services/plugins ที่ agent ใช้เข้าถึง stateful capabilities

---

## State แบบชั่วคราว

transient state คือ state ที่มีค่าเฉพาะระหว่าง execution ปัจจุบัน เช่น:
- current plan step
- intermediate tool outputs
- local variables
- temporary reasoning artifacts

สิ่งนี้มักไม่ควรถูกเก็บเป็น long-term memory

---

## State แบบ persistent

persistent state คือข้อมูลที่ยังต้องมีอยู่แม้ execution จะข้าม turn หรือข้าม process boundary

ตัวอย่าง:
- thread history
- workflow state
- pending tasks
- approval status
- partially completed execution

LangGraph docs เน้น persistence สำหรับ long-running workflows  
AutoGen Core เน้น runtime/lifecycle/message-driven execution

---

## Checkpointing และ Resumability

checkpointing และ resumability เป็นหัวข้อสำคัญมากพอที่จะดูแยกเฉพาะ  
ถ้าต้องการดูเรื่องนี้แบบเต็ม ให้ดู [[07 - Checkpointing and Resumability]]

---

## โมเดล State ที่พบบ่อย

### State แบบยึด thread เป็นหลัก

state ผูกกับ conversation thread หรือ session

เหมาะกับ:
- assistants
- support flows
- in-thread planning

### State แบบ graph / node

state ผูกกับ graph execution และ transitions

เหมาะกับ:
- branching workflows
- stepwise orchestration
- explicit execution control

### State แบบ actor / message

state กระจายตาม agents และ messages

เหมาะกับ:
- distributed systems
- asynchronous messaging
- multi-agent communication

### State แบบ kernel / middleware

state ถูกเข้าถึงผ่าน central kernel/services/plugins

เหมาะกับ:
- enterprise integrations
- plugin-rich architectures

---

## Interface ของ memory ใน framework

framework ต่างกันตรงว่ามอง memory เป็นอะไร:

### Primitive สำหรับ persistence ที่มีในตัว

เช่น thread/store/checkpoint abstraction

### การเชื่อม external store

framework เปิด interface ให้เชื่อม vector store, DB, profile store, หรือ custom memory service

### Memory เป็น service

บาง framework หรือ ecosystem แยก memory ออกเป็น service layer ชัด

---

## Tradeoff ของ State และ Memory

### เมื่อ persist state มากขึ้น

ข้อดี:
- resume ได้ดี
- continuity สูง

ข้อเสีย:
- complexity สูง
- debugging ยากขึ้น
- storage and privacy burden เพิ่ม

### เมื่อใช้ external memory มากขึ้น

ข้อดี:
- personalization
- long-term continuity

ข้อเสีย:
- retrieval complexity
- stale memory risk
- scope and retention challenges

### เมื่อใช้ state น้อยลง

ข้อดี:
- simpler
- easier to reason about

ข้อเสีย:
- limited workflow sophistication

---

## เลือก framework จากความต้องการด้าน state

### ถ้าต้องการ long-running และควบคุม execution ได้

ให้มอง framework ที่มี persistence/checkpoint model ชัด

### ถ้าต้องการ distributed multi-agent messaging

ให้มอง runtime/message model ก่อน UI abstraction

### ถ้าต้องการ plugin-centric enterprise integration

ให้มอง kernel/service-centric model

### ถ้าต้องการ task orchestration แบบเรียบง่าย

อาจไม่ต้องใช้ heavy state model ตั้งแต่แรก

---

## Failure Modes

### 1. สับสน session state กับ long-term memory

คิดว่า thread persistence = memory architecture ครบแล้ว

### 2. ไม่มี checkpoints สำหรับงานยาว

workflow ยาวแต่ restart ทุกครั้งเมื่อหลุด

### 3. persist ทุกอย่างมากเกินไป

persist state ทุกอย่างจน debug และ privacy ยาก

### 4. state ที่ซ่อนอยู่

framework จัดการ state ให้หมดจนทีมไม่เห็น execution semantics จริง

### 5. ไม่มี memory interface

framework ใช้งานได้ใน demo แต่ต่อ long-term memory หรือ external store ยากมาก

---

## หลักออกแบบ

- แยก working context, session state, และ long-term memory ให้ชัด
- เลือก framework จาก state requirements ไม่ใช่แค่ popularity
- ถ้างานต้อง pause/resume ได้ ให้คิด checkpointing ตั้งแต่ต้น
- อย่า persist ทุกอย่างโดยไม่มี lifecycle policy
- memory integration ควรถูกมองเป็น interface problem ไม่ใช่ prompt trick

---

## ความสัมพันธ์กับโน้ตอื่น

- [[02 AI Systems/Memory Systems/Core/01 - Working Memory vs Long-Term Memory]] — memory layers หลัก
- [[02 AI Systems/Memory Systems/Application/04 - Agent Memory Patterns]] — รูปแบบการประกอบ memory ใน runtime
- [[02 AI Systems/Agent Frameworks/Core/01 - Landscape]] — landscape ของ runtime models
- [[02 AI Systems/Agent Frameworks/Core/02 - Framework vs Custom Build]] — tradeoffs ด้าน state complexity
- [[02 AI Systems/Agent Frameworks/Core/07 - Checkpointing and Resumability]] — execution continuity และ recovery
- [[02 AI Systems/Evals/Core/09 - Observability and Feedback Loops]] — stateful systems ต้อง trace ได้
- [[Agent Frameworks - MOC]]

---

## โน้ตที่เกี่ยวข้อง

- [[04 Synthesis/Bridge/Synthesis - Memory in Agents]]
- [[02 AI Systems/Memory Systems/Memory Systems - MOC]]
- [[07 - Checkpointing and Resumability]]
- [[Agent Frameworks - MOC]]

---

## แหล่งอ้างอิงทางการ

- LangGraph Overview: https://langchain-ai.github.io/langgraphjs/reference/modules/langgraph.html
- LangGraph Cross-thread Persistence: https://langchain-ai.github.io/langgraphjs/how-tos/cross-thread-persistence-functional/
- AutoGen Core: https://microsoft.github.io/autogen/stable/user-guide/core-user-guide/index.html
- AutoGen Agents: https://microsoft.github.io/autogen/stable/user-guide/agentchat-user-guide/tutorial/agents.html
- Google ADK Sessions: https://google.github.io/adk-docs/sessions/session/
- Google ADK Memory: https://google.github.io/adk-docs/sessions/memory/
- Semantic Kernel Agent Framework: https://learn.microsoft.com/en-us/semantic-kernel/frameworks/agent/
