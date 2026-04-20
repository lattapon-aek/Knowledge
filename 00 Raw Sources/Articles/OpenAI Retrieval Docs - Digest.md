---
tags:
  - rawsources
  - digest
  - openai
  - retrieval
type: reference
status: draft
source: "https://developers.openai.com/api/docs/guides/retrieval"
parent_note: "[[OpenAI Retrieval Docs - Manifest]]"
---

# OpenAI Retrieval Docs - Digest

## Scope

digest นี้สรุปกลุ่มเอกสาร OpenAI ที่เกี่ยวกับ:
- retrieval
- file search
- vector stores

---

## Key Points

- OpenAI วาง retrieval เป็น pattern ที่ให้ระบบค้นข้อมูลจาก knowledge base ก่อนแล้วค่อย synthesize คำตอบ
- `file_search` เป็น tool สำหรับให้โมเดลค้นข้อมูลจากไฟล์ที่ถูกเตรียมไว้
- `vector_stores` เป็น container ของไฟล์ที่ถูก parse, chunk, embed, และ index แล้ว
- retrieval layer รองรับ search, filters, และ ranking options
- retrieval stack ของ OpenAI เหมาะกับงานที่ต้องการ semantic search บน corpus ที่เตรียมไว้ล่วงหน้า

---

## Operational Implications

- retrieval ไม่ใช่แค่ generation enhancement แต่เป็น search infrastructure ของระบบ
- chunking, vector store storage, filters, และ ranking options เป็น knobs สำคัญของ design
- file search เหมาะกับ use cases ที่ต้องให้โมเดลค้นข้อมูลจากเอกสารก่อนตอบ
- note ในหมวด `RAG` ของ vault นี้ใช้กลุ่ม docs นี้เป็นฐานสำคัญของ:
  - retrieval basics
  - embeddings/vector stores
  - chunking
  - context assembly
  - query transformation

---

## Related Notes

- [[00 Raw Sources/Articles/OpenAI Retrieval Docs - Manifest]]
- [[02 AI Systems/RAG/Core/01 - Retrieval Basics]]
- [[02 AI Systems/RAG/Retrieval/03 - Embeddings and Vector Databases]]
- [[02 AI Systems/RAG/Core/02 - Chunking Strategies]]
- [[02 AI Systems/RAG/Core/06 - Context Assembly]]
- [[02 AI Systems/RAG/Core/04 - Query Transformation]]
- [[02 AI Systems/Evals/Application/07 - RAG Evals]]

---

## Official References

- Retrieval: https://developers.openai.com/api/docs/guides/retrieval
- File Search: https://developers.openai.com/api/docs/guides/tools-file-search
- Vector Store Search API: https://developers.openai.com/api/reference/resources/vector_stores/methods/search
