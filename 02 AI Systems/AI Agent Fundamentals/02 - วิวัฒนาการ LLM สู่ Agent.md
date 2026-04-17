---
tags:
  - agent
  - llm
  - evolution
type: note
status: evergreen
source: "Google Skills — Agent Fundamentals (Module 1)"
parent_note: "[[AI Agent Fundamentals - MOC]]"
---

# วิวัฒนาการ LLM สู่ Agent



---

## 3 ระยะของวิวัฒนาการ

```
Stage 1: LLM API  →(+ Functions)→  Stage 2: LLM + Function Calling  →(+ Autonomy)→  Stage 3: AI Agent
```

---

## Stage 1: LLM API

**ลักษณะ:**
- เก่งด้านภาษาและความรู้
- สนทนา สรุป ให้คำแนะนำ อธิบายเหตุผลได้ดี

**ข้อจำกัด:**
- ไม่มี environmental awareness แบบปัจจุบัน
- ไม่มี tool use จริง
- ไม่มี execution capability

---

## Stage 2: LLM + Function Calling

**ลักษณะ:**
- เรียก function ได้
- ใช้ API ได้
- แตะระบบภายนอกได้

**ข้อจำกัด:**
- ยังไม่ autonomous
- ยังไม่ proactive
- ผู้ใช้ยังเป็นคนจัดลำดับงาน

---

## Stage 3: AI Agent

**ลักษณะ:**
- รับ **goal** แทนการรับคำสั่งย่อยทีละคำสั่ง
- รักษา context ได้ต่อเนื่อง
- วางแผนและตัดสินใจ next step ได้เอง
- ใช้ tools หลายตัวร่วมกันได้
- ทำงานวนซ้ำจนจบเป้าหมาย

---

## เปรียบเทียบ: Book a trip to Paris

| ระดับ | พฤติกรรม |
|---|---|
| LLM | Advice only — บอกวิธีจองทีละขั้น |
| Function Calling | Needs direction — ถาม: วันไหน? สายการบินไหน? โซนไหน? |
| Agent | Ready to act — หาเที่ยวบิน จับคู่โรงแรม พร้อมจองได้เลย |

Agent รวม **reasoning + context + tool use + execution planning** เข้าด้วยกัน

---

## ดูต่อ

- [[03 - คุณสมบัติ 5 อย่างของ Agent]]
- [[04 - สถาปัตยกรรม Agent: Model + Tools + Orchestration]]
