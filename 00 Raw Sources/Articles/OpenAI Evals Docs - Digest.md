---
tags:
  - rawsources
  - digest
  - openai
  - evals
type: reference
status: draft
source: "https://developers.openai.com/api/docs/guides/evals"
parent_note: "[[OpenAI Evals Docs - Manifest]]"
---

# OpenAI Evals Docs - Digest

## Scope

digest นี้สรุปกลุ่มเอกสาร OpenAI ที่เกี่ยวกับ:
- evals
- evaluation best practices
- agent evals
- trace grading

---

## Key Points

- OpenAI วาง evals เป็น workflow ที่เริ่มจาก task definition, test inputs, graders, และผลลัพธ์ที่นำไปใช้ iterate ต่อ
- evaluation best practices เน้น:
  - log everything
  - build representative datasets
  - grow the eval set over time
  - keep prior failures
- agent evals เน้น workflow-level behavior, traces, และ trajectory analysis
- trace grading ช่วยประเมินทั้ง decisions, tool calls, และ behavior ตาม criteria ที่ตั้งไว้

---

## Operational Implications

- หมวด `Evals` ใน vault นี้ควรถูกมองเป็นระบบต่อเนื่อง ไม่ใช่ benchmark ครั้งเดียว
- production logs และ traces ควรถูกแปลงเป็น benchmark และ regression cases
- success criteria มาก่อน grader choice
- agent systems ต้องมี trace-aware evaluation ไม่ใช่มองแค่ final answer

---

## Related Notes

- [[00 Raw Sources/Articles/OpenAI Evals Docs - Manifest]]
- [[02 AI Systems/Evals/Core/01 - Success Criteria]]
- [[02 AI Systems/Evals/Core/03 - LLM-as-Judge]]
- [[02 AI Systems/Evals/Application/06 - Prompt Evals]]
- [[02 AI Systems/Evals/Application/08 - Agent Evals]]
- [[02 AI Systems/Evals/Core/05 - Regression Testing]]
- [[02 AI Systems/Evals/Core/09 - Observability and Feedback Loops]]

---

## Official References

- Evals Guide: https://developers.openai.com/api/docs/guides/evals
- Evaluation Best Practices: https://developers.openai.com/api/docs/guides/evaluation-best-practices
- Agent Evals: https://developers.openai.com/api/docs/guides/agent-evals
- Trace Grading: https://developers.openai.com/api/docs/guides/trace-grading
