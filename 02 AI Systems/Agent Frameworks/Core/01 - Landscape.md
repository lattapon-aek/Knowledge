---
tags:
  - agents
  - frameworks
  - landscape
type: note
status: draft
source: "LangGraph Docs · AutoGen Docs · Semantic Kernel Agent Framework Docs · CrewAI Concepts Docs"
parent_note: "[[Agent Frameworks - MOC]]"
---

# Agent Frameworks - Landscape

## Summary

framework ต่างกันที่ abstraction, runtime model, state model, orchestration style, observability, และความยืดหยุ่นในการเชื่อม tools ดังนั้นการมอง landscape ให้ถูกคือการเข้าใจ “แกนการออกแบบ” ไม่ใช่แค่จำชื่อ framework

---

## Scope

- ทำไมต้องใช้ framework
- framework vs custom build
- selection criteria
- common architecture patterns

---

## ทำไม agent frameworks ถึงเกิดขึ้น

เมื่อระบบ agent โตเกิน prompt + tool call ธรรมดา จะเริ่มมีปัญหาเรื่อง:
- orchestration
- state persistence
- multi-step execution
- human-in-the-loop
- observability
- retries and recovery

frameworks จึงเกิดขึ้นเพื่อยกระดับจาก “เรียก model เป็นครั้ง ๆ” ไปสู่ “runtime สำหรับ agent systems”

จาก official docs ของแต่ละค่ายจะเห็นจุดเน้นต่างกัน:
- LangGraph เน้น low-level orchestration, controllability, persistence, human-in-the-loop
- AutoGen Core เน้น event-driven, distributed, actor-style agent systems
- Semantic Kernel เน้น middleware/kernel-centric integration, plugins, enterprise extensibility
- CrewAI เน้น process-oriented multi-agent collaboration

```mermaid
flowchart LR
    A[Single model call] --> B[Tool calling]
    B --> C[Agent loop]
    C --> D[Stateful orchestration]
    D --> E[Multi-agent runtime]
    E --> F[Framework need grows]
```

---

## แกนที่ใช้มอง framework landscape

### 1. Abstraction Level

framework บางตัวอยู่ระดับ low-level orchestration primitives  
บางตัวอยู่ระดับ high-level workflows หรือ ready-made agent teams

คำถามสำคัญ:
- ต้องการ control มากแค่ไหน
- ต้องการ build custom runtime หรือแค่ prototype เร็ว

### 2. Runtime Model

บาง framework เป็น graph runtime  
บาง framework เป็น actor/message runtime  
บาง framework เป็น process/task orchestration model

นี่มีผลต่อ:
- composability
- resumability
- debugability
- scaling

### 3. State and Memory Model

framework ต่างกันมากตรง:
- เก็บ transient state ยังไง
- persist execution ยังไง
- รองรับ checkpoint หรือไม่
- เชื่อม long-term memory ยังไง

### 4. Tool and Integration Model

ดูว่า framework:
- มอง tools เป็น first-class citizens หรือไม่
- รองรับ plugins / MCP / external APIs อย่างไร
- คุม permission boundaries ได้แค่ไหน

### 5. Observability and Control

ดูว่า framework:
- trace execution ได้ไหม
- debug step-by-step ได้ไหม
- interrupt / resume / approve ได้ไหม

---

## Architecture Patterns ที่พบใน landscape

### Graph-Oriented

เช่น LangGraph  
เหมาะกับระบบที่ต้องการ:
- explicit nodes and edges
- branching
- checkpoints
- long-running stateful flows

### Actor / Message-Oriented

เช่น AutoGen Core  
เหมาะกับ:
- distributed systems
- event-driven communication
- multi-agent messaging
- runtime-level scaling

### Middleware / Kernel-Centric

เช่น Semantic Kernel  
เหมาะกับ:
- plugin-centric integration
- enterprise service composition
- model/tool abstraction in one central kernel

### Process / Team-Oriented

เช่น CrewAI  
เหมาะกับ:
- task delegation
- sequential or hierarchical processes
- explicit crew/task structures

```mermaid
flowchart TD
    A[Framework Landscape] --> B[Graph-oriented]
    A --> C[Actor/message-oriented]
    A --> D[Kernel-centric]
    A --> E[Process/team-oriented]
```

---

## Framework Families แบบใช้งานจริง

### LangGraph

official docs ระบุชัดว่าเป็น low-level orchestration framework สำหรับ controllable agents และเน้น:
- persistence
- human-in-the-loop
- customizable architectures

### AutoGen

official docs ระบุ Core ว่าเป็น event-driven, distributed, scalable agent framework และ AgentChat เป็นชั้นที่ง่ายขึ้นสำหรับ conversational single/multi-agent apps

### Semantic Kernel

Microsoft docs วางตำแหน่ง Semantic Kernel เป็น lightweight development kit / middleware ที่มี kernel เป็นศูนย์กลางของ services และ plugins และมี Agent Framework ซ้อนอยู่บน core นี้

### CrewAI

official docs วางจุดเด่นที่ processes เช่น sequential และ hierarchical process สำหรับ crew/task orchestration

---

## เลือก framework จากอะไร

ควรถามก่อนว่า use case ต้องการอะไร:

### ถ้าต้องการ explicit control สูง

มักเอนไปทาง graph or low-level runtime

### ถ้าต้องการ distributed multi-agent messaging

มักเอนไปทาง actor/message runtime

### ถ้าต้องการ enterprise integration and plugins

มักเอนไปทาง kernel-centric middleware

### ถ้าต้องการ task orchestration เข้าใจง่าย

มักเอนไปทาง process/team-oriented frameworks

---

## สิ่งที่ framework ไม่ได้แก้ให้เอง

แม้ใช้ framework แล้ว ยังต้องออกแบบเองเรื่อง:
- evaluation
- guardrails
- permission boundaries
- memory write policies
- tool semantics
- source grounding

framework ช่วยเรื่อง orchestration แต่ไม่ได้แทน system design

---

## Failure Modes

### 1. Choose by Popularity Only

เลือก framework จากกระแส ไม่ใช่ runtime needs

### 2. Overfit to a Framework Abstraction

พยายามบีบ problem ทุกแบบให้เข้ากับ abstraction เดียว

### 3. Confuse Framework with Architecture

คิดว่าใช้ framework แล้ว architecture ดีโดยอัตโนมัติ

### 4. Ignore Operational Requirements

เลือก framework โดยไม่ดู traceability, resumability, approval flow

---

## Design Rules

- เริ่มจาก runtime needs ก่อนชื่อ framework
- แยก orchestration concern ออกจาก model/tool concern
- มอง framework เป็น biasing layer ไม่ใช่ architecture สำเร็จรูป
- ถ้างานต้องการ control สูง ให้เลือก framework ที่ abstraction ต่ำพอ
- ถ้างานยังเล็ก อย่ารีบแบก framework หนักเกินความจำเป็น

---

## ความสัมพันธ์กับโน้ตอื่น

- [[02 AI Systems/AI Agent Fundamentals/07 - รูปแบบ Agent Architectures]] — pattern ระดับ concept ก่อนเลือก framework
- [[02 AI Systems/Agent Frameworks/Core/02 - Framework vs Custom Build]] — tradeoffs ในการตัดสินใจ
- [[02 AI Systems/Agent Frameworks/Core/03 - State and Memory]] — จุดต่างสำคัญของ frameworks
- [[02 AI Systems/MCP/MCP - MOC]] — integration layer ที่หลาย frameworks เชื่อมด้วย
- [[04 Synthesis/Synthesis - LLM to Agent Stack]] — ตำแหน่ง framework ใน stack
- [[Agent Frameworks - MOC]]

---

## Related Notes

- [[02 AI Systems/AI Agent Fundamentals/07 - รูปแบบ Agent Architectures]]
- [[04 Synthesis/Synthesis - LLM to Agent Stack]]
- [[Agent Frameworks - MOC]]

---

## Official References

- LangGraph Overview: https://langchain-ai.github.io/langgraphjs/reference/modules/langgraph.html
- LangGraph Cross-thread Persistence: https://langchain-ai.github.io/langgraphjs/how-tos/cross-thread-persistence-functional/
- AutoGen Overview: https://microsoft.github.io/autogen/stable/index.html
- AutoGen Core: https://microsoft.github.io/autogen/stable/user-guide/core-user-guide/index.html
- Semantic Kernel Overview: https://learn.microsoft.com/en-us/semantic-kernel/overview/
- Semantic Kernel Agent Framework: https://learn.microsoft.com/en-us/semantic-kernel/frameworks/agent/
- CrewAI Processes: https://docs.crewai.com/en/concepts/processes
