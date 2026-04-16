---
tags:
  - usecase
  - multi-agent
  - orchestration
  - infrastructure
  - version-sensitive
type: note
status: evergreen
source: "https://www.digitalocean.com/community/tutorials/single-to-multi-agent-infrastructure · https://platform.openai.com/docs/guides/trace-grading · https://docs.langchain.com/oss/javascript/langgraph/persistence · https://microsoft.github.io/autogen/stable/user-guide/core-user-guide/design-patterns/group-chat.html · https://docs.crewai.com/en/concepts/flows"
parent_note: "[[05 Use Cases/Use Cases - MOC]]"
---

# Use Cases - Move from Single to Multi-Agent

## เมื่อควรใช้กรณีนี้

ใช้ path นี้เมื่อ single agent เริ่มไม่พอ เพราะงานกลายเป็น:
- too broad for one prompt or one runtime loop
- naturally parallelizable into specialized subtasks
- dependent on explicit handoffs between roles
- long-running enough to need checkpointing or resume
- audit-sensitive enough to need traces and decision lineage

ตัวอย่าง:
- research agent + writer agent + reviewer agent
- data collection + analysis + reporting pipeline
- router agent that dispatches tasks to specialists
- workflow that requires human approval before continuing

---

## เส้นตัดสินใจ

1. เริ่มจาก single agent + tools ก่อน
2. ถามว่างานเป็นเส้นตรงและ deterministic หรือไม่
3. ถ้าใช่ ให้คงไว้ที่ workflow หรือ single-agent design
4. ถ้างานกว้าง ขนานได้ หรือแยกบทบาทชัด ค่อยพิจารณา multi-agent
5. ถ้า agent ต้อง handoff งาน, persist state, หรือ resume ภายหลัง, multi-agent infra เริ่มจำเป็น
6. ถ้ายังมอง handoff และ failure ไม่ออก ให้เพิ่ม observability ก่อนขยายต่อ

---

## สัญญาณที่ควรย้าย

- ต้องใช้ expertise หลายแบบแยกกันชัด
- subtasks ต่าง ๆ รันขนานกันได้
- state ต้องอยู่รอดผ่าน interrupts หรือ human approval
- ค่า coordination ต่ำกว่าการใช้ prompt ใหญ่ก้อนเดียว
- ต้องการ traceable ownership ของ decisions และ outputs

---

## สัญญาณที่ควรอยู่ single-agent

- งานยังแคบและเป็นเส้นตรง
- orchestration แพงกว่างานที่ต้องทำ
- ปัญหาหลักคือ prompt quality ไม่ใช่การแยกโครงระบบ
- output ไม่จำเป็นต้องแยกบทบาทหรือใช้ shared state

---

## รูปแบบความล้มเหลวที่พบบ่อย

- เพิ่ม agent ก่อนจะเข้าใจปัญหา orchestration
- ใช้ multi-agent เพื่อกลบงานที่ยังนิยามไม่ชัด
- แชร์ state โดยไม่มี rules เรื่อง ownership
- ใส่ asynchronous messaging โดยไม่มี retries หรือ idempotency
- ไม่มี traces จน diagnose failure ไม่ได้

---

## ควรสร้างอะไรก่อน

ถ้าคำตอบคือ “ควรไป multi-agent” ให้สร้างตามลำดับนี้:
1. role boundaries
2. orchestrator / router
3. shared state and persistence
4. communication channel
5. observability and evals
6. recovery policy

---

## ลิงก์ที่เกี่ยวข้อง

- [[04 Synthesis/Synthesis - Single to Multi-Agent Infrastructure]]
- [[02 AI Systems/AI Agent Fundamentals/08 - Workflow vs AI Agent]]
- [[02 AI Systems/AI Agent Fundamentals/09 - เมื่อไรควรและไม่ควรใช้ Agent]]
- [[06 Engineering/Architecture to Code/Architecture - Multi-Agent Infrastructure]]
- [[06 Engineering/Frameworks/Framework - OpenAI Agents and Responses Patterns]]
- [[06 Engineering/Frameworks/Framework - LangGraph]]
- [[06 Engineering/Frameworks/Framework - AutoGen vs CrewAI]]
- [[06 Engineering/Frameworks/Framework - LangChain Agents]]
- [[Home]]
