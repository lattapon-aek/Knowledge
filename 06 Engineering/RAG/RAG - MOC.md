---
tags:
  - engineering
  - rag
  - moc
type: moc
status: evergreen
source: "vault-local engineering hub"
parent_note: "[[06 Engineering/Engineering - MOC]]"
---

# RAG - MOC

implementation layer สำหรับงาน retrieval pipeline, chunking, ranking, context assembly, และ grounding

---

## Notes Map

- [[06 Engineering/RAG/Recipe - Build a RAG Pipeline|Build a RAG Pipeline]]
- [[06 Engineering/RAG/Decision - Choose a Retrieval Strategy|Choose a Retrieval Strategy]]

---

## Related Hubs

- [[02 AI Systems/RAG/RAG - MOC|RAG - MOC]]
- [[01 Foundations/LLM Foundations/LLM Foundations - MOC|LLM Foundations - MOC]]
- [[01 Foundations/Context Windows/Context Windows - MOC|Context Windows - MOC]]
- [[04 Synthesis/Decision/Synthesis - Agent vs Workflow vs RAG|Synthesis - Agent vs Workflow vs RAG]]
- [[04 Synthesis/Decision/Synthesis - Prompting vs Fine-tuning vs RAG|Synthesis - Prompting vs Fine-tuning vs RAG]]
- [[06 Engineering/README|Engineering - README]]

---

## Use This Layer When

- ต้องแปลง RAG concept ให้กลายเป็น pipeline ที่ลงมือทำได้
- ต้องคุม chunking, retrieval, reranking, และ context packing
- ต้องออกแบบ implementation ที่ผูกกับ app หรือ framework ใด framework หนึ่ง
