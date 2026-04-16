---
tags:
  - engineering
  - rag
  - recipe
type: note
status: evergreen
source: "vault-local engineering"
parent_note: "[[06 Engineering/RAG/RAG - MOC]]"
---

# Recipe - Build a RAG Pipeline

recipe สำหรับเริ่มจาก RAG concept แล้วค่อยลง implementation แบบเป็นลำดับ

---

## Steps

1. กำหนด retrieval goal ให้ชัด
2. เลือกข้อมูลต้นทางและขอบเขตของ corpus
3. ออกแบบ chunking strategy ให้เหมาะกับข้อมูล
4. เลือก retrieval mode ที่ใช้จริงในระบบ
5. เพิ่ม reranking หรือ filtering ถ้าต้องการ precision สูงขึ้น
6. จัด context assembly ให้เหมาะกับ token budget
7. วาง grounding / citation / answer formatting
8. ทดสอบกับชุด queries ที่แทน use case จริง
9. เพิ่ม monitoring สำหรับ failure modes ที่พบบ่อย

---

## Checklist

- มี source of truth สำหรับ corpus แล้ว
- รู้ว่า retrieval success วัดจากอะไร
- มี policy ว่าจะส่งอะไรเข้า context และไม่ส่งอะไร
- มี fallback เมื่อ retrieval ไม่พอ
- มี eval case สำหรับ regressions
