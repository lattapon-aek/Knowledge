---
tags:
  - rawsources
  - moc
  - ingest
type: moc
status: evergreen
source: ""
parent_note: "[[Home]]"
---

# Raw Sources - MOC

ชั้น `raw sources` คือแหล่งข้อมูลต้นฉบับของ vault นี้ และเป็น source of truth สำหรับการ ingest เข้าไปยังฝั่ง wiki

หลักสำคัญ:
- ไฟล์ในหมวดนี้เป็น **ต้นฉบับ** ไม่ใช่ synthesis
- LLM อ่านจากชั้นนี้ แต่ **ไม่ควรแก้ไขเนื้อหาต้นฉบับ**
- การสรุป, cross-link, synthesis, และโครงความรู้ทั้งหมดควรไปอยู่ใน `01 Foundations`, `02 AI Systems`, `04 Synthesis`, และหมวดอื่นของ wiki

---

## โครงสร้าง

- [[00 Raw Sources/Articles/Articles - README|Articles]] — บทความเว็บ, blog posts, docs exports, clipped markdown
- [[00 Raw Sources/Articles/Source Manifests - MOC|Source Manifests]] — entry points สำหรับชุด official docs และ source families ที่ใช้อยู่จริง
- [[00 Raw Sources/Papers/Papers - README|Papers]] — papers, reports, whitepapers, arXiv exports
- [[00 Raw Sources/Assets/Assets - README|Assets]] — รูปภาพ, diagrams, screenshots, PDFs, attachments
- [[00 Raw Sources/Source Records/Source Records - MOC|Source Records]] — ทะเบียนแหล่งอ้างอิงที่กู้คืนจาก `source:` fields เดิม
- [[00 Raw Sources/Source Intake Checklist|Source Intake Checklist]] — checklist สำหรับเอา source เข้าระบบ

---

## หลักการใช้งาน

1. เก็บ source ใหม่ไว้ในหมวดที่เหมาะก่อน
2. คงชื่อไฟล์ให้สื่อความหมาย และถ้าเป็นไปได้ให้มีวันที่หรือชื่อแหล่งที่มา
3. อย่าเขียนสรุปลงในไฟล์ต้นฉบับ
4. ถ้าจะสกัดความรู้ ให้สร้างหรืออัปเดต note ฝั่ง wiki แทน
5. ถ้าต้องอ้างอิงแหล่งที่มา ให้ใส่ไว้ใน `source:` ของ note ปลายทาง
6. ถ้าต้นฉบับเดิมหายไปแล้ว ให้เก็บร่องรอยไว้ใน `Source Records`

---

## ความสัมพันธ์กับ Layer อื่น

- [[index]] — catalog ของฝั่ง wiki
- [[Inbox]] — จุดรับไอเดียดิบหรือ quick captures ที่ยังไม่ใช่ source ต้นฉบับ
- [[Vault Workflow - Capture to Evergreen]] — workflow ฝั่ง note lifecycle

---

## หมายเหตุ

- `00 Raw Sources` คือชั้นข้อมูลดิบ
- `01–05` คือชั้นความรู้ที่ LLM และมนุษย์ใช้ร่วมกัน
- ถ้าต่อไปมี ingestion workflow จริง อาจเพิ่ม `log.md` เพื่อบันทึกว่า source ไหนถูกประมวลผลแล้วบ้าง
