---
tags:
  - usecase
  - prompting
  - evaluation
type: usecase
status: evergreen
created: "2026-04-12"
source: ""
parent_note: "[[05 Use Cases/Use Cases - MOC]]"
---

# Use Cases - Improve Prompt Reliability

## Goal

ใช้เมื่อ prompt ตอบไม่สม่ำเสมอ หลุด format หรือให้คำตอบไม่ตรง criteria

รายละเอียด prompt anatomy, patterns, structured generation, และ context engineering อยู่ใน canonical notes ของ `Prompt Engineering` และ `Context Windows` แล้ว

---

## Reading Order

1. [[01 Foundations/Prompt Engineering/Core/01 - Prompt Engineering คืออะไร]]
2. [[01 Foundations/Prompt Engineering/Core/02 - องค์ประกอบของ Prompt]]
3. [[01 Foundations/Prompt Engineering/Core/03 - Prompt Patterns พื้นฐาน]]
4. [[01 Foundations/Prompt Engineering/Core/04 - หลักการจากหลายบริษัท]]
5. [[01 Foundations/Prompt Engineering/Core/05 - Evaluation และ Failure Modes]]
6. [[01 Foundations/Prompt Engineering/Core/06 - Template และ Common Problems]]
7. [[01 Foundations/Context Windows/Core/02 - การบริหารและ Context Engineering]]

---

## Fix Order

1. เขียน success criteria ให้ชัด
2. lock output format
3. ลด noise ใน context
4. เพิ่ม examples เท่าที่จำเป็น
5. ทดสอบซ้ำกับ adversarial inputs

---

## Cross Links

- [[04 Synthesis/Synthesis - Prompting vs Fine-tuning vs RAG]]
- [[Home]]
