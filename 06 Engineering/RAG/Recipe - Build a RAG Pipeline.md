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
3. ออกแบบ ingestion pipeline: parse, clean, normalize, และ preserve structure
4. ออกแบบ chunking strategy ให้เหมาะกับข้อมูล
5. เติม metadata สำหรับ filtering, permission, citation, และ lifecycle
6. เลือก embedding model และ indexing backend
7. เลือก retrieval mode ที่ใช้จริงในระบบ
8. เพิ่ม reranking หรือ filtering ถ้าต้องการ precision สูงขึ้น
9. จัด context assembly ให้เหมาะกับ token budget
10. วาง grounding / citation / answer formatting
11. ทดสอบกับชุด queries ที่แทน use case จริง
12. เพิ่ม monitoring สำหรับ ingestion, retrieval, answer quality, และ stale index

---

## Checklist

- มี source of truth สำหรับ corpus แล้ว
- รู้ว่า retrieval success วัดจากอะไร
- มี lifecycle สำหรับ refresh, delete, expiration, และ reindex
- มี policy ว่าจะส่งอะไรเข้า context และไม่ส่งอะไร
- มี fallback เมื่อ retrieval ไม่พอ
- มี eval case สำหรับ regressions

---

## Related System Notes

- [[02 AI Systems/RAG/Core/RAG - Ingestion and Indexing Pipeline]]
- [[02 AI Systems/RAG/Retrieval/RAG - Metadata Filtering and Permission-Aware Retrieval]]
- [[02 AI Systems/RAG/Core/02 - Chunking Strategies]]
- [[02 AI Systems/RAG/Core/06 - Context Assembly]]
