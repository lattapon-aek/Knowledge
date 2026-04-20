---
tags:
  - agent
  - risks
  - best-practices
  - security
type: note
status: evergreen
source: "Medium — Nishan Jain, \"What Are AI Agents? Fundamentals, Examples & Best Practices\" (May 2025)"
parent_note: "[[AI Agent Fundamentals - MOC]]"
---

# Risks และ Best Practices



---

## Common Drawbacks ของ AI Agents

### 1. Compliance and Security Risks

ความเสี่ยง:
- Privacy violations
- Unauthorized data access
- Prompt injection

แนวทางลด:
- Data anonymization
- Access controls
- Input sanitization
- Regular audits

> ถ้า agent แตะข้อมูลจริงของลูกค้า ต้องคิดเรื่อง privacy และ security ตั้งแต่แรก ถ้าไม่มี access control agent อาจเข้าถึงข้อมูลเกินสิทธิ์

---

### 2. Hallucinations and Inaccuracies

ความเสี่ยง:
- โมเดลสร้างคำตอบที่ผิด
- ให้ข้อมูลชวนเข้าใจผิดอย่างมั่นใจ

แนวทางลด:
- ใช้ RAG เพื่อ ground คำตอบ
- Validate outputs ด้วย logic หรือ rules
- ใช้หลาย agents ช่วยกัน verify facts

> Agent ที่มี tool ไม่ได้แปลว่าจะไม่ hallucinate ถ้า retrieval ไม่ดีหรือ reasoning ผิด ก็ยังตอบผิดได้

---

### 3. Overreliance and Lack of Oversight

ความเสี่ยง:
- ผู้ใช้ไว้ใจ AI มากเกินไป
- ไม่มี human oversight ในเรื่องสำคัญ

แนวทางลด:
- Human checks for important decisions
- Make agent behavior transparent
- Educate users

> ใน use cases สำคัญ เช่น กฎหมาย การแพทย์ การเงิน ต้องมี human oversight เสมอ

---

### 4. Scalability Challenges

ความเสี่ยง:
- ระบบช้าลงหรือล้มเหลวเมื่อ workload โตขึ้น

แนวทางลด:
- Modular systems
- Cloud infrastructure
- Load balancing
- Performance monitoring

> ตอน prototype มักดูง่าย แต่พอ scale จริงจะเจอ cost, latency, orchestration complexity และ reliability issues

---

## Best Practices 6 ข้อ

### 1. Adopt a Privacy-by-Design Approach

ผสาน privacy เข้าไปตั้งแต่ทุกช่วงของการพัฒนา:
- Data collection → storage → access → retention → decision-making

### 2. Regular Training and Awareness

ทุกฝ่ายที่เกี่ยวข้องควรเข้าใจ:
- Security protocols
- Ethical guidelines
- Compliance standards

ไม่ใช่แค่ทีม AI — ทีม operation และผู้ใช้ก็ต้องรู้ข้อจำกัดและความเสี่ยง

### 3. Continuous Monitoring and Evaluation

Monitor แบบต่อเนื่อง ติดตาม:
- Accuracy
- Anomalies
- Performance
- Cost
- Failure patterns

> Agent ที่ไม่มี observability จะดูแลใน production ยากมาก

### 4. Engage with Regulatory Bodies

ติดตามข้อกำกับดูแลและกฎหมายที่เปลี่ยนแปลง โดยเฉพาะใน regulated domains ควรมี legal review หรือ policy alignment ที่ชัดเจน

### 5. Implement Robust Incident Response Plans

มีแผนตอบสนองเมื่อเกิดเหตุผิดปกติ:
- Security breaches
- Compliance violations
- Harmful outputs
- Data handling incidents

> อย่าคิดแค่จะป้องกัน ต้องคิดด้วยว่าเมื่อพลาดแล้วจะรับมืออย่างไร

### 6. ตั้ง Guardrails เพื่อพฤติกรรมที่ปลอดภัย

**Guardrails** คือขอบเขตความปลอดภัยของ agent — สิ่งที่ต้องกำหนด:
- อะไรที่ agent ทำได้
- อะไรที่ทำไม่ได้
- เรื่องอ่อนไหวที่ต้องจำกัด
- พฤติกรรมที่เป็น harmful output
- จุดที่ต้องขอ human approval

> Guardrails, monitoring, และ validation เป็นของจำเป็น **ไม่ใช่ของเสริม**

---

## Practical Takeaways

1. AI Agent คือระบบที่ให้ LLM ควบคุมการตัดสินใจของ workflow แบบ dynamic
2. โครงสร้างหลักคือ `Thought → Action → Observation`
3. Agent ต่างจาก workflow ตรงที่เลือกเส้นทางตาม context ได้
4. ความสามารถสำคัญ: reasoning, planning, tool use, environment interaction, autonomy
5. ควรเลือก architecture ตามลักษณะงาน ([[07 - รูปแบบ Agent Architectures]])
6. สิ่งที่ต้องคำนึงถึง: security, privacy, compliance, scalability, human oversight
7. Guardrails + monitoring + validation = ของจำเป็น ไม่ใช่ optional

---

## การวัด Agent ที่ดี

การสร้าง agent ที่ดีไม่ได้วัดแค่ความฉลาด ต้องวัดที่:
- ความปลอดภัย
- ความโปร่งใส
- การควบคุมได้
- ความน่าเชื่อถือ

---

## Evaluation Metrics — สิ่งที่ควรวัดใน Production

| Metric | ความหมาย |
|---|---|
| Task success rate | งานที่ agent ทำสำเร็จ / งานทั้งหมด |
| Tool-call success rate | tool call ที่ทำงานได้ถูกต้อง / ทั้งหมด |
| Hallucination rate | คำตอบที่ผิดหรือสร้างขึ้นเอง / ทั้งหมด |
| Latency per task | เวลาเฉลี่ยในการทำงาน 1 task |
| Cost per task | ต้นทุน LLM + tool calls ต่อ task |
| Escalation-to-human rate | งานที่ต้องส่งต่อมนุษย์ / ทั้งหมด |

---

## Production Guardrails Design — ชั้นของการควบคุม

Guardrails ที่ดีไม่ได้มีแค่ชั้นเดียว ควรออกแบบเป็นหลายชั้น:

```
User Request
    ↓
[Input Guardrails]       — กรอง input อันตราย, prompt injection
    ↓
[Planner / Agent]
    ↓
[Tool Permission Check]  — agent มีสิทธิ์ใช้ tool นี้ไหม?
    ↓
[Tool Execution]
    ↓
[Observation + Validation] — ผลลัพธ์สมเหตุสมผลไหม?
    ↓
[Output Guardrails]      — moderation, harmful content check
    ↓
Final Response

(ทุก step → Audit Log)
```

ชั้นที่ต้องมี:
- **Input guardrails** — กรอง prompt injection และ input ที่เป็นอันตราย
- **Tool permission guardrails** — กำหนด scope ที่ agent เข้าถึงได้
- **Output moderation** — ตรวจ output ก่อนส่งถึงผู้ใช้
- **Approval checkpoints** — จุดที่ต้องให้มนุษย์ยืนยันก่อน
- **Audit logging** — บันทึกทุก action เพื่อ traceability

---

## Failure Handling และ Fallback Paths

สิ่งที่ agent ควรมี policy ชัดเจน เมื่อเกิดสถานการณ์เหล่านี้:

| สถานการณ์ | แนวทาง |
|---|---|
| Tool ล้มเหลว | มี retry policy + fallback tool หรือ graceful error message |
| ข้อมูลไม่เพียงพอ | ถามผู้ใช้เพิ่ม หรือ escalate to human |
| Conflicting evidence | หยุดและแจ้งให้ผู้ใช้รู้ แทนที่จะเดา |
| เกิน budget / timeout | หยุดงาน แจ้งสถานะ และบันทึก audit log |

> อย่าออกแบบแค่ happy path — ระบบที่ดีต้องรู้ว่าจะทำอะไรเมื่อสิ่งผิดปกติเกิดขึ้น

---

## Keywords สำคัญ

`AI Agent` · `Agentic System` · `TAO Cycle` · `ReAct` · `CodeAct` · `Multi-Agent Workflows` · `Agentic RAG` · `Guardrails` · `Human-in-the-loop` · `Privacy-by-Design` · `Hallucination` · `Observability` · `Tool-Using Agents` · `Self-Reflective Agents`

---

## ดูต่อ

- [[05 Use Cases/Decision/Use Cases - When to Use an Agent|When to Use an Agent]]
- [[02 AI Systems/Guardrails/Guardrails - MOC|Guardrails - MOC]] — รวม input/output controls, tool safety, fallback, monitoring, และ permission models
- [[02 AI Systems/Evals/Evals - MOC|Evals - MOC]] — วัด reliability และตรวจ regression ของ agent behavior
- [[05 Use Cases/Application/Use Cases - Evaluate an AI Agent]]
- [[AI Agent Fundamentals - MOC]]

## ตัวอย่าง Implementation จริง

- [[03 Tools/Claude Code/Workflow/22 - Error Handling|Error Handling]] — Failure Handling ใน Claude Code จริง: Hallucination detection, fallback prompts, retry limits, permissions.deny สำหรับ irreversible actions
