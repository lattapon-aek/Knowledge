---
tags:
  - evals
  - regression
type: note
status: evergreen
source: "OpenAI Evals Guide · OpenAI Evaluation Best Practices"
parent_note: "[[02 AI Systems/Evals/Evals - MOC|Evals - MOC]]"
---

# Evals - Regression Testing

## Summary

regression testing คือการรันชุด eval เดิมซ้ำทุกครั้งที่มีการเปลี่ยน prompt, model, tool policy, retrieval stack, หรือ workflow เพื่อจับว่าของที่เคยดีแล้วพังลงหรือไม่

---

## Scope

- regression sets
- version comparison
- release gates
- failure preservation
- change management

---

## Regression Set คืออะไร

regression set คือชุดตัวอย่างที่เก็บ failure cases, representative cases, และ edge cases ไว้เพื่อรันซ้ำเมื่อระบบเปลี่ยน

สิ่งที่ควรรวม:
- happy path
- hard cases
- prior failures
- adversarial cases
- format-sensitive cases

---

## Version Comparison

regression testing มักใช้ compare:
- prompt เก่า vs prompt ใหม่
- model เก่า vs model ใหม่
- retrieval pipeline เดิม vs ใหม่
- tool policy เดิม vs ใหม่

เป้าหมายคือดูว่า:
- ดีขึ้นตรงไหน
- พังตรงไหน
- trade-off ใหม่ยอมรับได้ไหม

---

## Release Gates

regression testing ควรถูกใช้เป็น gate ก่อน release การเปลี่ยนสำคัญ

ตัวอย่าง gate:
- ห้าม exactness ลดลงเกิน threshold
- ห้าม format adherence ตก
- ห้าม safety failures เพิ่ม
- latency/cost ต้องยังอยู่ในงบ

ถ้าไม่มี gate การเปลี่ยนระบบจะกลายเป็น trial-and-error ที่เสี่ยงพังของเดิม

---

## Failure Preservation

failure cases เก่ามีค่ามาก

เมื่อเจอ bug หรือ failure ใหม่ ควรเพิ่มเข้า regression set เพื่อไม่ให้มันกลับมาอีก

นี่คือวิธีทำให้ eval suite ฉลาดขึ้นเรื่อย ๆ ตามระบบจริง

---

## Change Management

regression testing มีประโยชน์มากเมื่อระบบเปลี่ยนหลายมิติพร้อมกัน เช่น:
- model upgrade
- prompt rewrite
- retrieval tuning
- schema changes

การเปลี่ยนทีละอย่างและมี regression set จะช่วย isolate สาเหตุได้ดีขึ้น

---

## Design Rules

- ทุกการเปลี่ยนที่สำคัญควรผ่าน regression set
- เก็บ prior failures เข้า regression suite เสมอ
- compare versions แบบมี thresholds ไม่ใช่ดู impression
- ใช้ regression testing เป็น release discipline ไม่ใช่ optional task
- combine กับ human spot checks เมื่อเป็น high-stakes systems

---

## ความสัมพันธ์กับโน้ตอื่น

- [[02 AI Systems/Evals/Core/01 - Success Criteria]] — thresholds ของ regression ต้องผูกกับ success criteria
- [[02 AI Systems/Evals/Application/06 - Prompt Evals]] — prompt changes ควรมี regression set
- [[02 AI Systems/Evals/Application/08 - Agent Evals]] — agent workflows ต้องมี regression suite ของ trajectories
- [[02 AI Systems/Evals/Application/07 - RAG Evals]] — retrieval changes ต้องมี regression set แยก
- [[02 AI Systems/Evals/Evals - MOC|Evals - MOC]]

---

## Official References

- OpenAI Evals Guide: https://platform.openai.com/docs/guides/evals
- OpenAI Evaluation Best Practices: https://platform.openai.com/docs/guides/evaluation-best-practices
