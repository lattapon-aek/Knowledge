---
tags:
  - rawsources
  - manifests
  - officialdocs
type: moc
status: evergreen
source: ""
parent_note: "[[Raw Sources - MOC]]"
---

# Source Manifests - MOC

หมวดนี้ใช้เก็บ `source manifest` สำหรับแหล่งข้อมูลที่ถูกใช้อยู่จริงใน vault แล้ว  
manifest ไม่ใช่ต้นฉบับเต็ม แต่เป็น entry point เชิงปฏิบัติสำหรับการ ingest, revisit, และ trace กลับไปยัง official sources

---

## Ingest Plans

- [[00 Raw Sources/Articles/Advanced RAG and Agentic RAG - Ingest Plan|Advanced RAG and Agentic RAG - Ingest Plan]]
- [[00 Raw Sources/Articles/2026-04 New Sources - Ingest Plan|2026-04 New Sources - Ingest Plan]]
- [[00 Raw Sources/Articles/2026-04 Harness Engineering - Ingest Plan|2026-04 Harness Engineering - Ingest Plan]]
- [[00 Raw Sources/Articles/2026-04 IBM Supplement - Ingest Plan|2026-04 IBM Supplement - Ingest Plan]]

---

## Manifests

- [[00 Raw Sources/Articles/Claude Code Official Docs - Manifest|Claude Code Official Docs]]
- [[00 Raw Sources/Articles/OpenAI Evals Docs - Manifest|OpenAI Evals Docs]]
- [[00 Raw Sources/Articles/OpenAI Retrieval Docs - Manifest|OpenAI Retrieval Docs]]
- [[00 Raw Sources/Articles/Google Cloud RAG and Evaluation Docs - Manifest|Google Cloud RAG and Evaluation Docs]]
- [[00 Raw Sources/Articles/Microsoft Learn Search and RAG Docs - Manifest|Microsoft Learn Search and RAG Docs]]
- [[00 Raw Sources/Articles/Legacy Internal Knowledge Bases - Manifest|Legacy Internal Knowledge Bases]]

---

## Digests

- [[00 Raw Sources/Articles/Claude Code Official Docs - Digest|Claude Code Official Docs - Digest]]
- [[00 Raw Sources/Articles/OpenAI Evals Docs - Digest|OpenAI Evals Docs - Digest]]
- [[00 Raw Sources/Articles/OpenAI Retrieval Docs - Digest|OpenAI Retrieval Docs - Digest]]
- [[00 Raw Sources/Articles/Google Cloud RAG and Evaluation Docs - Digest|Google Cloud RAG and Evaluation Docs - Digest]]
- [[00 Raw Sources/Articles/Microsoft Learn Search and RAG Docs - Digest|Microsoft Learn Search and RAG Docs - Digest]]

---

## วิธีใช้

- ถ้ามีต้นฉบับจริงแล้ว ให้เก็บไว้ใน `Articles/` หรือ `Papers/` แล้วใช้ manifest นี้เป็นตัวเชื่อม
- ถ้ายังไม่มีต้นฉบับเต็ม manifest จะทำหน้าที่เป็น source stub และ registry สำหรับ ingest รอบต่อไป
- ทุก manifest ควรบอก:
  - แหล่งข้อมูลหลัก
  - กลุ่มโน้ตที่อิงอยู่
  - สิ่งที่ควร ingest หรือ refresh ต่อ
