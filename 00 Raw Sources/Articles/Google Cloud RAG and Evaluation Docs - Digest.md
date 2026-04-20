---
tags:
  - rawsources
  - digest
  - googlecloud
  - rag
  - evals
type: reference
status: draft
source: "https://docs.cloud.google.com/vertex-ai/generative-ai/docs/rag-engine/rag-overview"
parent_note: "[[Google Cloud RAG and Evaluation Docs - Manifest]]"
---

# Google Cloud RAG and Evaluation Docs - Digest

## Scope

digest นี้สรุปกลุ่มเอกสาร Google Cloud ที่เกี่ยวกับ:
- Vertex AI RAG Engine
- grounding with RAG
- groundedness checking
- evaluation overview

---

## Key Points

- Google อธิบาย RAG เป็น pipeline ที่มี ingestion, chunking, embedding, indexing, retrieval, และ generation
- grounding เป็นมิติสำคัญแยกจาก text quality
- ระบบสามารถตรวจ support / groundedness ของคำตอบจาก evidence ที่ถูกดึงมา
- evaluation service ของ Vertex AI เน้นให้กำหนด evaluation goals และ metrics ก่อนรัน eval

---

## Operational Implications

- หมวด `RAG` ของ vault นี้ควรให้ความสำคัญกับ grounding และ citation quality มากพอ ๆ กับ answer quality
- หมวด `Evals` ควรเชื่อมกับ groundedness metrics และ support-based evaluation
- docs ชุดนี้เหมาะกับ use cases ที่เน้น trust, evidence traceability, และ enterprise-quality RAG

---

## Related Notes

- [[00 Raw Sources/Articles/Google Cloud RAG and Evaluation Docs - Manifest]]
- [[02 AI Systems/RAG/Core/01 - Retrieval Basics]]
- [[02 AI Systems/RAG/Core/07 - Grounding and Citation]]
- [[02 AI Systems/RAG/Evaluation/08 - Evaluation]]
- [[02 AI Systems/Evals/Application/07 - RAG Evals]]
- [[02 AI Systems/Evals/Core/01 - Success Criteria]]

---

## Official References

- Vertex AI RAG Engine Overview: https://docs.cloud.google.com/vertex-ai/generative-ai/docs/rag-engine/rag-overview
- Ground Responses Using RAG: https://docs.cloud.google.com/vertex-ai/generative-ai/docs/grounding/ground-responses-using-rag
- Check Grounding with RAG: https://cloud.google.com/generative-ai-app-builder/docs/check-grounding
- Gen AI Evaluation Service Overview: https://docs.cloud.google.com/vertex-ai/generative-ai/docs/models/evaluation-overview
