---
tags:
  - standards
  - workflow
  - notes
type: guide
status: evergreen
source: ""
parent_note: "[[Home]]"
---

# Vault Standards - Note Lifecycle

## Status Meanings

ใช้ `status` แค่ 3 ค่าเพื่อให้ตีความง่ายและดูแลต่อได้จริง

- `seed` = ไอเดียดิบ, capture เร็ว, ยังไม่จัดรูป, ยังไม่เชื่อมโยงดีพอ
- `draft` = มีเนื้อหาพอใช้งานแล้ว แต่ยังควร refine, เชื่อมโยง, หรือสังเคราะห์ต่อ
- `evergreen` = โครงสร้างนิ่ง, ใช้อ้างอิงซ้ำได้, เหมาะเป็นหน้าแม่หรือหน้าอธิบายหลัก

---

## Recommended Rules

- หน้า `Home`, `MOC`, `Synthesis`, `Glossary`, `Use Case` ใช้ `evergreen`
- โน้ตรายหัวข้อทั่วไปใช้ `draft` เป็นค่าเริ่มต้น
- ถ้าเป็นแค่ note dump, clipping, หรือเก็บไว้อ่านทีหลัง ให้ใช้ `seed`

---

## Promote a Note

เลื่อนสถานะจาก `draft` ไป `evergreen` เมื่อ:

- เนื้อหากระชับและโครงสร้างนิ่งแล้ว
- มี cross-links ที่เหมาะสม
- มี takeaway หรือ decision value ชัด
- อ่านซ้ำแล้วไม่ต้องแก้หลักคิดบ่อย

---

## Practical Workflow

1. capture เป็น `seed`
2. เรียบเรียงและเชื่อมโยงเป็น `draft`
3. สรุปให้ reusable แล้วค่อย promote เป็น `evergreen`

---

## Cross Links

- [[Home]]
- [[Inbox]]
- [[Vault Workflow - Capture to Evergreen]]
- [[Vault Standards - Properties]]
- [[_Templates/Standard Note Template|Standard Note Template]]
