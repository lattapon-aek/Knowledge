---
tags:
  - usecase
  - guardrails
  - tools
type: usecase
status: evergreen
source: ""
parent_note: "[[05 Use Cases/Use Cases - MOC]]"
---

# Use Cases - Design Guardrails for Tool Use

## Summary

ใช้ note นี้เมื่อ agent หรือ LLM application มี tool use แล้วต้องออกแบบ guardrails ให้ปลอดภัย ใช้งานได้จริง และไม่หนักจนทำให้ระบบใช้ไม่ได้

รายละเอียด control layers, validation, permission model, fallback, และ incident handling อยู่ใน `Guardrails` canonical notes แล้ว note นี้เป็น decision path สำหรับออกแบบ boundary ของ tool use

## Canonical Notes

- [[02 AI Systems/Guardrails/Guardrails - MOC]]
- [[02 AI Systems/Guardrails/Core/01 - Input and Output Controls]]
- [[02 AI Systems/Guardrails/Core/03 - Tool Safety]]
- [[02 AI Systems/Guardrails/Operations/04 - Permission Models]]
- [[02 AI Systems/Guardrails/Core/05 - Fallback Policies]]

---

## ใช้เมื่อไร

ใช้ note นี้เมื่อ:
- agent เริ่มเรียก tools ที่มีผลกระทบต่อข้อมูลหรือ systems ภายนอก
- ต้องกำหนด approval, permissions, หรือ confirmation gates
- ต้องแยก safe tools ออกจาก high-risk tools

---

## Step 1: แยกประเภท tools ก่อน

ถามให้ชัดว่า tools แต่ละตัวเป็น:
- read-only
- write-capable
- external side effects
- sensitive data access
- privileged operations

เครื่องมือแต่ละ class ต้องมี guardrails ไม่เท่ากัน

---

## Step 2: วาง control layers

โดยทั่วไปควรมีอย่างน้อย:
1. tool eligibility
2. input validation
3. parameter safety checks
4. confirmation or approval gates
5. execution boundaries
6. output validation and logging

---

## Step 3: ออกแบบ permission model

ต้องตอบให้ได้ว่า:
- อะไร auto-approve ได้
- อะไรต้องยืนยันทุกครั้ง
- อะไรต้องห้ามโดย policy
- ใครเป็นผู้อนุมัติ
- audit trail อยู่ตรงไหน

---

## Step 4: ออกแบบ fallback

ถ้า tool call ไม่ควรเกิดหรือไม่ผ่าน policy:
- deny พร้อมอธิบาย
- ask for confirmation
- degrade to read-only path
- escalate to human

---

## Heuristic แบบเร็ว

| ระดับความเสี่ยง | แนว guardrail ที่ควรมี |
|---|---|
| read-only, low impact | validation + logging |
| data mutation | validation + confirmation |
| external side effects | permission gate + containment |
| privileged operations | explicit approval + audit trail |
| ambiguous or unsafe intent | deny or escalate |

---

## Anti-Patterns

- ใช้ allowlist แบบตื้นโดยไม่ดู parameters
- มองข้าม tool outputs ว่าอาจเป็น attack surface
- ไม่มี confirmation สำหรับ irreversible actions
- ไม่มี audit logs
- guardrails แน่นเกินจนทีมเริ่ม bypass ระบบ

---

## Recommended Reading

1. [[02 AI Systems/Guardrails/Core/01 - Input and Output Controls]]
2. [[02 AI Systems/Guardrails/Core/02 - Output Validation]]
3. [[02 AI Systems/Guardrails/Core/03 - Tool Safety]]
4. [[02 AI Systems/Guardrails/Operations/04 - Permission Models]]
5. [[02 AI Systems/Guardrails/Core/05 - Fallback Policies]]
6. [[02 AI Systems/Guardrails/Operations/06 - Monitoring and Incidents]]
7. [[02 AI Systems/Guardrails/Core/07 - Safety vs Usability Tradeoffs]]
8. [[02 AI Systems/MCP/14 - Tools: การออกแบบและทำงาน]]

---

## Cross Links

- [[02 AI Systems/Guardrails/Guardrails - MOC]]
- [[02 AI Systems/MCP/Security/05 - Security, Consent และ Authorization]]
- [[05 Use Cases/Use Cases - Evaluate an AI Agent]]
- [[Home]]
