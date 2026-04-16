---
tags:
  - agents
  - frameworks
  - architecture
type: note
status: draft
source: "LangGraph Docs · AutoGen Docs · Semantic Kernel Docs · CrewAI Concepts Docs"
parent_note: "[[Agent Frameworks - MOC]]"
---

# Agent Frameworks - Framework vs Custom Build

## ภาพรวม

framework ช่วยลดเวลาประกอบระบบ แต่เพิ่ม abstraction, dependency, และข้อจำกัดบางอย่าง จึงต้องแยกให้ชัดว่าเมื่อไรควรใช้ framework และเมื่อไรควรเขียน runtime หรือ orchestration เอง

---

## ขอบเขต

- speed of development
- observability
- extensibility
- lock-in risk
- custom orchestration needs

---

## คำถามจริงไม่ใช่ “framework ดีไหม”

คำถามที่ถูกกว่าคือ:
- use case นี้ต้องการ orchestration complexity ระดับไหน
- ต้องการความเร็วในการพัฒนา หรือ control ระยะยาว
- ต้องการ distributed runtime หรือแค่ local workflow
- ต้องการ human approval, checkpoints, tracing, หรือไม่

framework กับ custom build จึงเป็นเรื่อง tradeoff ไม่ใช่คำตอบตายตัว

---

## เมื่อ framework ช่วยมาก

framework มักคุ้มเมื่อระบบเริ่มมี:
- multi-step execution
- state persistence
- retry/fallback paths
- human-in-the-loop
- multi-agent communication
- observability needs

official docs ของ LangGraph, AutoGen, และ Semantic Kernel ต่างชี้ไปทางเดียวกันว่า framework มีคุณค่าเมื่อ orchestration และ integration complexity สูงขึ้น

### สิ่งที่ framework มักให้มา

- runtime model
- tool integration
- state and memory interfaces
- tracing or debugging hooks
- orchestration primitives
- reusable patterns

---

## เมื่อ custom build คุ้มกว่า

custom build มักคุ้มเมื่อ:
- problem เล็กและชัด
- workflow ตรงไปตรงมา
- abstraction ของ framework หนักเกินความจำเป็น
- ต้องการ tight integration เฉพาะทางมาก
- team ต้องการ full control ของ execution semantics

ตัวอย่าง:
- simple retrieval assistant
- single-step tool-calling service
- domain-specific workflow ที่ deterministic มาก

---

## ข้อได้เปรียบของ Framework

### 1. ประกอบระบบได้เร็วขึ้น

เริ่มได้เร็วและได้ primitive หลายอย่างพร้อมกัน

### 2. ภาษากลางร่วมกัน

ทีมคุยกันง่ายขึ้นด้วย concepts ที่ framework กำหนด

### 3. มี orchestration ในตัว

เช่น graph execution, message passing, crews, plugins

### 4. มี hooks สำหรับ state / persistence

หลาย framework มีแนวคิดเรื่อง threads, checkpoints, store, หรือ session state มาให้

### 5. Observability และการควบคุม

framework บางตัวออกแบบมาเพื่อ trace, debug, interrupt, หรือ scale ตั้งแต่ต้น

---

## ข้อเสียของ Framework

### 1. ภาระจาก abstraction

ต้องเรียน mental model ของ framework ก่อน

### 2. ความเสี่ยงจาก lock-in

architecture อาจผูกกับ abstractions ของ framework มากเกินไป

### 3. ความซับซ้อนที่ซ่อนอยู่

ของที่ดูง่ายตอน prototype อาจซับซ้อนตอน production

### 4. ทางออกนอก abstraction

บางครั้ง use case จริงต้องออกนอก abstraction ของ framework

### 5. พื้นที่พึ่งพาเพิ่มขึ้น

เพิ่ม dependency, version churn, และ operational complexity

---

## ข้อได้เปรียบของ Custom Build

### 1. ควบคุมได้แม่นยำ

คุณกำหนด semantics ของ runtime เองทั้งหมด

### 2. พื้นที่ของระบบน้อย

มีเท่าที่ use case ต้องใช้จริง

### 3. เข้ากับโดเมนง่ายกว่า

ไม่ต้องบังคับ problem ให้เข้ากับ abstraction ของ framework

### 4. ภาระทางความคิดน้อยกว่า

ถ้าระบบเล็ก อาจง่ายกว่าการเรียน framework ใหญ่

---

## ข้อเสียของ Custom Build

### 1. ต้องสร้าง runtime เอง

ต้องสร้างเองเรื่อง:
- retries
- tracing
- state handling
- approval points
- orchestration

### 2. ทำให้มาตรฐานร่วมยากกว่า

ทีมอาจไม่มี shared framework vocabulary

### 3. ขยายช้ากว่า

พอระบบโต อาจต้องค่อย ๆ สร้างสิ่งที่ frameworks มีอยู่แล้ว

---

## ตารางเปรียบเทียบ tradeoff

| Dimension | Framework | Custom build |
|---|---|---|
| Speed to first system | สูง | ต่ำกว่า |
| Runtime control | ปานกลางถึงสูง ขึ้นกับ framework | สูงสุด |
| Conceptual overhead | สูงกว่า | ต่ำกว่าสำหรับระบบเล็ก |
| Lock-in risk | มี | ต่ำกว่า |
| Standardization | ดีกว่า | ขึ้นกับทีม |
| Escape hatches | อาจยาก | คุมเองได้ |

---

## เมื่อไรควรเริ่ม custom แล้วค่อย migrate

แนวทางที่ pragmatic คือ:
- เริ่ม custom ถ้าปัญหายังเล็กและชัด
- ย้ายไป framework เมื่อ orchestration complexity โตจริง

สัญญาณว่า custom build เริ่มไม่พอ:
- state handling ซับซ้อนขึ้น
- ต้องมี resume/checkpoints
- multi-agent patterns เริ่มเยอะ
- tracing/debugging เริ่มลำบาก
- approval/fallback logic กระจายหลายจุด

---

## เมื่อไรควรเริ่ม framework ตั้งแต่แรก

ควรเริ่ม framework ตั้งแต่ต้นเมื่อรู้ล่วงหน้าว่า:
- ต้องมี long-running workflows
- ต้องมี human-in-the-loop
- ต้องมี multi-agent coordination
- ต้องมี persistence and checkpoints
- team ต้องการ standardization เร็ว

---

## Failure Modes

### 1. รีบใช้ framework เกินไป

ระบบยังเล็กแต่แบก framework หนักเกินไป

### 2. ยึดมั่นจะเขียนเองเกินไป

ยืนยันจะเขียนเองหมดแม้ complexity โตจนควรใช้ framework

### 3. ใช้เกณฑ์ประเมินผิด

เลือกจาก demo UX แทน runtime needs

### 4. ผูก architecture กับคำของ vendor มากเกินไป

คิดและตั้งชื่อ architecture ตาม framework จนเปลี่ยนออกยาก

---

## หลักออกแบบ

- เริ่มจาก system requirements ไม่ใช่ framework brand
- ถ้าปัญหายังเล็ก ให้ optimize for clarity
- ถ้าปัญหามี orchestration/state complexity ให้ optimize for runtime control and observability
- design architecture ให้มี conceptual layer ของตัวเอง แม้จะใช้ framework ใด framework หนึ่ง
- ประเมิน cost ของ migration ตั้งแต่ต้น

---

## ความสัมพันธ์กับโน้ตอื่น

- [[02 AI Systems/Agent Frameworks/Core/01 - Landscape]] — ภาพรวมของ framework families
- [[02 AI Systems/Agent Frameworks/Core/03 - State and Memory]] — จุดตัดสินใจสำคัญอีกแกน
- [[02 AI Systems/AI Agent Fundamentals/04 - สถาปัตยกรรม Agent: Model + Tools + Orchestration]] — complexity ของ orchestration เป็นตัวผลักให้ใช้ framework
- [[02 AI Systems/Evals/Core/09 - Observability and Feedback Loops]] — observability เป็น factor สำคัญในการเลือก
- [[Agent Frameworks - MOC]]

---

## โน้ตที่เกี่ยวข้อง

- [[02 AI Systems/Agent Frameworks/Core/01 - Landscape]]
- [[02 AI Systems/Evals/Core/09 - Observability and Feedback Loops]]
- [[Agent Frameworks - MOC]]
- [[06 Engineering/Decisions/Decision - Choose a Framework]]

---

## แหล่งอ้างอิงทางการ

- LangGraph Overview: https://langchain-ai.github.io/langgraphjs/reference/modules/langgraph.html
- AutoGen Overview: https://microsoft.github.io/autogen/stable/index.html
- AutoGen Core: https://microsoft.github.io/autogen/stable/user-guide/core-user-guide/index.html
- Semantic Kernel Overview: https://learn.microsoft.com/en-us/semantic-kernel/overview/
- Semantic Kernel Agent Framework: https://learn.microsoft.com/en-us/semantic-kernel/frameworks/agent/
- CrewAI Processes: https://docs.crewai.com/en/concepts/processes
