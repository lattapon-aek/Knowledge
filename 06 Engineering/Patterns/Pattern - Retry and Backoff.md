---
tags:
  - engineering
  - patterns
  - reliability
type: note
status: evergreen
source: "vault-local engineering"
parent_note: "[[06 Engineering/Patterns/Patterns - MOC]]"
---

# Pattern - Retry and Backoff

pattern สำหรับงานที่มี transient failure, network error, หรือ rate limit

---

## When to Use

- external API call ล้มเหลวชั่วคราว
- tool call หรือ job queue มี occasional failure
- task ต้องการ retry แบบมีเพดาน

## Design Rules

- retry เฉพาะ error ที่มีโอกาสหายเอง
- ใส่ max retry count ชัดเจน
- ใช้ exponential backoff หรือ jitter เมื่อเหมาะสม
- log ครั้งที่ retry และเหตุผลที่ retry
- ถ้าเป็น irreversible action ให้หยุดและ escalate แทน retry ตรง ๆ

## Notes

- pattern นี้ควรจับคู่กับ fallback policy และ observability เสมอ
- อย่าใช้ retry เป็นวิธีแก้ทุกอย่าง
