---
tags:
  - engineering
  - evals
  - moc
type: moc
status: evergreen
source: ""
parent_note: "[[06 Engineering/Engineering - MOC]]"
---

# Evals - MOC

implementation layer สำหรับ eval harness, regression checks, benchmark sets, และ gating ก่อน release

---

## Notes Map

- [[06 Engineering/Evals/Recipe - Build an Eval Harness|Build an Eval Harness]]

---

## Related Hubs

- [[02 AI Systems/Evals/Evals - MOC|Evals - MOC]]
- [[05 Use Cases/Use Cases - Evaluate an AI Agent|Use Cases - Evaluate an AI Agent]]
- [[05 Use Cases/Use Cases - Improve Prompt Reliability|Use Cases - Improve Prompt Reliability]]
- [[06 Engineering/README|Engineering - README]]

---

## Use This Layer When

- ต้องเอา eval concept ไปทำเป็น pipeline ที่รันซ้ำได้
- ต้องมี regression gate ก่อน deploy
- ต้องแยก dataset, metric, และ evaluator ให้ชัด
- ต้องจับผล eval มาใช้กับ release decision
