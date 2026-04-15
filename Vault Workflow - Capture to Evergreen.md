---
tags:
  - workflow
  - capture
  - evergreen
type: guide
status: evergreen
source: ""
parent_note: "[[Home]]"
---

# Vault Workflow - Capture to Evergreen

## Goal

ทำให้การเพิ่มความรู้ใหม่ไม่ชนกับโครงสร้างหลัก และค่อยยกระดับ note ตามคุณภาพแทนการพยายามเขียนให้สมบูรณ์ตั้งแต่ครั้งแรก

---

## Flow

1. Capture ที่ [[Inbox]]
2. ถ้ายังดิบมาก ใช้ `seed`
3. เมื่อเริ่มเรียบเรียง ให้ย้ายไปโน้ตจริงและเปลี่ยนเป็น `draft`
4. เมื่อลิงก์ครบและเนื้อหานิ่ง ค่อย promote เป็น `evergreen`

---

## Decision Rules

- ยังไม่ชัดว่าจะอยู่หมวดไหน: อยู่ `Inbox`
- รู้หมวดแล้วแต่ยังไม่สรุปดี: ไปเป็น note `draft`
- เป็นบทสรุปใช้ซ้ำ/หน้าแม่/คู่มือ: ใช้ `evergreen`

---

## Weekly Maintenance

- clear `Inbox`
- promote draft ที่พร้อม
- merge notes ที่ซ้ำกัน
- เพิ่ม cross-links ที่ยังหาย

---

## Cross Links

- [[Inbox]]
- [[Vault Standards - Note Lifecycle]]
- [[Home]]
