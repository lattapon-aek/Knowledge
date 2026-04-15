---
tags:
  - evals
  - humanreview
type: note
status: draft
source: "OpenAI Evaluation Best Practices · Google Cloud Evaluation Overview"
parent_note: "[[Evals - MOC]]"
---

# Evals - Human Evaluation

## Summary

human evaluation ยังจำเป็นในงานที่ rubric ยังไม่นิ่ง, task มี nuance สูง, หรือความเสี่ยงของการตัดสินผิดสูงเกินกว่าจะพึ่ง automated eval อย่างเดียว

---

## Scope

- when human review is needed
- reviewer rubrics
- calibration
- disagreement handling
- human-in-the-loop evaluation

---

## เมื่อไร Human Evaluation ยังจำเป็น

human evaluation ควรใช้เมื่อ:
- rubric ยังไม่ชัด
- task มี nuance สูง
- output มีผลกระทบสูง
- automated grader ยังไม่น่าเชื่อถือพอ
- ต้องวัด usefulness หรือ UX จริง

OpenAI best practices reinforce ว่า automated eval มีประโยชน์มาก แต่ไม่ใช่ replacement ของ human review ทุกกรณี

---

## Reviewer Rubrics

human review ที่ดีไม่ควรเป็น “อ่านแล้วรู้สึก”

ควรมี:
- criteria ชัด
- scoring guide
- examples ของ pass/fail
- edge cases

ยิ่ง rubric ชัด human agreement ก็ยิ่งดี

---

## Calibration

ก่อนใช้ reviewer หลายคน ควร calibrate ด้วย:
- gold examples
- anchor samples
- discussion on disagreements
- rubric refinement

เป้าหมายไม่ใช่ให้ทุกคนคิดเหมือนกันทุกอย่าง แต่ให้ตัดสินในกรอบเดียวกัน

---

## Disagreement Handling

ควรออกแบบล่วงหน้าว่า:
- ถ้า reviewer ไม่ตรงกันจะทำอย่างไร
- ใช้ majority vote หรือ escalation
- เก็บ disagreement cases เป็น training data ของ rubric หรือ automated grader ได้ไหม

disagreement cases มักมีคุณค่าสูง เพราะบอกว่าระบบหรือ rubric ยังไม่ชัดพอ

---

## Human-in-the-Loop Evaluation

pattern ที่พบบ่อย:
- ใช้ automated eval คัดกรองส่วนใหญ่
- ส่ง sample หรือ edge cases ให้ human review
- ใช้ human review validate grader quality อีกชั้น

นี่ช่วย balance ระหว่าง scale กับ reliability

---

## Design Rules

- ใช้ human review กับงานที่ high stakes หรือยัง rubric ไม่ชัด
- สร้าง reviewer rubric ก่อนเริ่ม review จำนวนมาก
- calibrate reviewers เสมอ
- เก็บ disagreement cases ไว้ refine system และ grading rubric
- ใช้ human review คู่กับ automated eval ไม่ใช่แทนกันทั้งหมด

---

## ความสัมพันธ์กับโน้ตอื่น

- [[02 AI Systems/Evals/Core/01 - Success Criteria]] — human review ต้องยึด criteria เดียวกัน
- [[02 AI Systems/Evals/Core/03 - LLM-as-Judge]] — ใช้ human review เพื่อตรวจความน่าเชื่อถือของ judge
- [[Evals - MOC]]

---

## Official References

- OpenAI Evaluation Best Practices: https://platform.openai.com/docs/guides/evaluation-best-practices
- Google Cloud Evaluation Overview: https://cloud.google.com/vertex-ai/generative-ai/docs/models/evaluation-overview
