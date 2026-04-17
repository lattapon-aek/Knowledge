---
tags:
  - usecase
  - evals
  - agents
type: usecase
status: evergreen
source: ""
parent_note: "[[Home]]"
---

# Use Cases - Evaluate an AI Agent

## Summary

ใช้ note นี้เมื่อกำลังออกแบบ evaluation สำหรับ agent ที่มีทั้ง reasoning, tool use, state, และ safety requirements พร้อมกัน

รายละเอียด success criteria, benchmark design, judge, human review, regression, และ observability อยู่ใน `Evals` canonical notes แล้ว note นี้เป็น decision path สำหรับเลือก evaluation scope

## Canonical Notes

- [[02 AI Systems/Evals/Evals - MOC]]
- [[02 AI Systems/Evals/Core/01 - Success Criteria]]
- [[02 AI Systems/Evals/Core/02 - Benchmark Design]]
- [[02 AI Systems/Evals/Core/03 - LLM-as-Judge]]
- [[02 AI Systems/Evals/Core/05 - Regression Testing]]

---

## ใช้เมื่อไร

ใช้ note นี้เมื่อ:
- ต้องประเมินว่า agent ทำงานสำเร็จจริงหรือไม่
- ต้องแยกปัญหาระหว่าง prompt, planning, tool use, และ guardrails
- ต้องออกแบบ regression set สำหรับ agent runtime

---

## Step 1: แยก objective ของ agent

ก่อนทำ eval ต้องตอบให้ได้ว่า:
- success ของงานนี้คืออะไร
- completion หมายถึงอะไร
- มี safety constraints อะไรห้ามละเมิด
- human approval อยู่ตรงไหน
- logs หรือ traces อะไรเก็บได้บ้าง

---

## Step 2: แยก evaluation เป็นหลายชั้น

อย่าวัดแค่ final answer ให้แยกอย่างน้อย:
- task completion
- tool correctness
- trajectory quality
- policy and safety adherence
- latency / cost / retries

---

## Step 3: ออกแบบ test set ให้ครอบจริง

ควรมีอย่างน้อย:
- happy paths
- edge cases
- failure-triggering cases
- ambiguous requests
- high-risk actions

---

## Step 4: เลือก evaluator ให้เหมาะ

โดยทั่วไปจะผสมกัน:
- deterministic checks สำหรับ format และ policy
- rubric-based checks สำหรับ quality
- trace review สำหรับ multi-step failures
- human review สำหรับ high-risk slices

---

## Heuristic แบบเร็ว

| สิ่งที่อยากรู้ | eval ที่ควรมี |
|---|---|
| agent ทำงานจบไหม | task completion eval |
| ใช้ tool ถูกไหม | tool correctness / trace eval |
| reasoning loop ดีไหม | trajectory review / LLM-as-judge |
| ปลอดภัยไหม | policy and guardrail checks |
| ปล่อยเวอร์ชันใหม่ได้ไหม | regression testing |

---

## Anti-Patterns

- วัดแค่ final answer แล้วสรุปว่า agent ดี
- ไม่มี trace-level visibility
- ไม่มี failure slices
- ไม่มี regression set ก่อนเปลี่ยน prompts หรือ tools
- ใช้ LLM-as-judge กับทุกอย่างโดยไม่มี deterministic checks ประกบ

---

## Recommended Reading

1. [[01 Foundations/LLM Foundations/13 - Evaluation Foundations]]
2. [[02 AI Systems/Evals/Core/01 - Success Criteria]]
3. [[02 AI Systems/Evals/Core/02 - Benchmark Design]]
4. [[02 AI Systems/Evals/Core/03 - LLM-as-Judge]]
5. [[02 AI Systems/Evals/Core/05 - Regression Testing]]
6. [[02 AI Systems/Evals/Application/08 - Agent Evals]]
7. [[02 AI Systems/Evals/Core/09 - Observability and Feedback Loops]]
8. [[02 AI Systems/Guardrails/Core/03 - Tool Safety]]
9. [[02 AI Systems/Guardrails/Operations/06 - Monitoring and Incidents]]

---

## Cross Links

- [[02 AI Systems/Evals/Evals - MOC]]
- [[02 AI Systems/AI Agent Fundamentals/AI Agent Fundamentals - MOC]]
- [[04 Synthesis/Synthesis - LLM to Agent Stack]]
- [[Home]]
