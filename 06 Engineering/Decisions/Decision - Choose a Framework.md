---
tags:
  - engineering
  - decisions
  - framework
  - adr
type: note
status: evergreen
source: "vault-local engineering"
parent_note: "[[06 Engineering/Decisions/Decisions - MOC]]"
---

# Decision - Choose a Framework

decision note สำหรับบันทึกเหตุผลเลือก framework หรือ runtime stack

---

## Use When

- ต้องเลือก framework สำหรับ agent runtime
- มีหลาย option ที่ tradeoff ต่างกัน
- ต้องกลับมาทบทวนเหตุผลภายหลัง

## Decision Template

- Context: ปัญหาคืออะไร
- Options: มีอะไรให้เลือก
- Criteria: เกณฑ์ที่ใช้ตัดสิน
- Decision: เลือกอะไร
- Consequences: ได้อะไร เสียอะไร
- Follow-ups: สิ่งที่ต้องตรวจหลังเลือก

## Rules

- ตัดสินจาก runtime needs ก่อนชื่อ framework
- แยก architecture requirement ออกจาก brand preference
- ระบุสิ่งที่ยังไม่รู้ให้ชัด
