---
tags:
  - agent
  - properties
type: note
status: evergreen
source: "Google Skills — Agent Fundamentals (Module 1)"
parent_note: "[[AI Agent Fundamentals - MOC]]"
---

# คุณสมบัติ 5 อย่างของ Agent



---

## ภาพรวม

ไม่ใช่ทุกระบบที่ใช้ LLM และ tools จะนับเป็น agent จริง Google แยกคุณสมบัติหลักของ agent ไว้ 5 อย่าง:

1. **Goal-directed behavior** — ทำงานเพื่อเป้าหมาย
2. **Autonomous operation** — ทำงานได้โดยไม่ต้องสั่งทุก step
3. **Proactive initiative** — ขยับงานเข้าใกล้ goal อย่างต่อเนื่อง
4. **Environmental awareness** — สังเกตและอัปเดต world model
5. **Tool use** — กระทำผ่านเครื่องมือจริง

---

## 1. Goal-directed behavior

Agent ทำงานเพื่อ **"เป้าหมาย"** ไม่ใช่แค่ตอบคำถาม

เชิงระบบ:
- เข้าใจ current state
- เข้าใจ desired state
- หาวิธีลดช่องว่างระหว่างสองสถานะนี้

---

## 2. Autonomous operation

เมื่อได้รับ goal แล้ว agent สามารถ:
- คิดลำดับงานเอง
- เลือกเครื่องมือเอง
- ตัดสินใจ next step เอง

**โดยไม่ต้องให้มนุษย์บอกทุก function call**

---

## 3. Proactive initiative

Agent ไม่ได้แค่รอคำสั่ง แต่จะพยายามขยับงานให้เข้าใกล้ goal อย่างต่อเนื่อง:
- หา context เพิ่มเอง
- ถามคำถามเฉพาะเมื่อจำเป็นจริง ๆ
- ใช้ข้อมูลที่มีอยู่ก่อน
- ดำเนินการขั้นถัดไปเมื่อยังไม่จบงาน

---

## 4. Environmental awareness

Agent สังเกต environment ผ่านข้อมูลหลายแบบ:
- คำขอจากผู้ใช้
- ผลลัพธ์จาก API
- สถานะในฐานข้อมูล
- error messages
- calendar state
- monitoring systems

แล้วอัปเดต **mental model / world model** ของตนเองตามสิ่งที่พบ

---

## 5. Tool use

Agent ไม่ได้หยุดอยู่ที่ข้อความ แต่สามารถกระทำผ่าน:
- APIs
- databases
- external services
- business systems
- application functions

เปลี่ยนจาก "อธิบายว่าจะทำอะไร" ไปเป็น **"ทำจริง"**

---

## ตัวอย่าง: คุณสมบัติครบ 5 อย่างใน 1 use case

Use case: "Should I wear a jacket today?"

| คุณสมบัติ | สิ่งที่ agent ทำ |
|---|---|
| Goal-directed | เข้าใจว่าเป้าหมายคือช่วยตัดสินใจเรื่องแจ็กเก็ต |
| Environmental awareness | เช็ก weather API + calendar |
| Tool use | เรียก weather tool และ calendar tool จริง |
| Autonomous operation | ทำได้เองโดยไม่ต้องถูกสั่งทีละขั้น |
| Proactive initiative | เช็กช่วงเวลาที่ผู้ใช้ต้องออกนอก ไม่รอให้ถาม |

---

## ดูต่อ

- [[04 - สถาปัตยกรรม Agent_ Model + Tools + Orchestration]]
- [[05 - วงจร Perceive-Think-Act-Check]]
