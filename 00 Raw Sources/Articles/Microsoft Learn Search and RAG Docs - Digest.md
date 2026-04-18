---
tags:
  - rawsources
  - digest
  - microsoft
  - search
  - rag
type: reference
status: evergreen
source: "https://learn.microsoft.com/en-us/azure/search/vector-search-overview · https://learn.microsoft.com/en-us/azure/search/retrieval-augmented-generation-overview · https://learn.microsoft.com/en-us/azure/search/agentic-retrieval-overview"
parent_note: "[[Microsoft Learn Search and RAG Docs - Manifest]]"
---

# Microsoft Learn Search and RAG Docs - Digest

## Scope

digest นี้สรุปกลุ่มเอกสาร Microsoft Learn ที่เกี่ยวกับ:
- vector search
- hybrid search
- semantic ranking
- semantic chunking
- agentic retrieval
- cost management

---

## Key Points

- Azure AI Search วาง retrieval infrastructure ที่ครอบทั้ง vector search, keyword search, hybrid search, semantic ranking, และ filters
- hybrid search ใช้ full-text + vector query พร้อม fusion
- semantic ranker เป็น L2 ranking layer ที่มาหลัง first-stage retrieval
- semantic chunking ช่วยให้ chunking ยึดโครงสร้างเอกสารได้ดีขึ้น
- agentic retrieval ชี้ไปสู่ retrieval ที่มี query decomposition และ orchestration มากขึ้น
- Microsoft RAG overview แยก RAG challenges เป็น query understanding, multi-source data access, token constraints, response time, และ security/governance
- Microsoft วาง classic RAG เป็น single-query pattern ที่ application orchestrates handoff ไป LLM เอง ส่วน agentic retrieval เป็น multi-query pipeline ที่มี LLM-assisted query planning
- agentic retrieval คืน structured response ที่มี grounding data, reference data, และ activity / execution details
- agentic retrieval เหมาะกับ chatbot/agent, complex conversational queries, high relevance, citations, และ query details แต่มี latency/cost เพิ่มจาก planning/reranking

---

## Operational Implications

- docs ชุดนี้เป็น backbone ของหมวด `RAG` ฝั่ง retrieval infrastructure ใน vault นี้
- เหมาะกับการคิดเรื่อง:
  - hybrid retrieval
  - reranking
  - chunking
  - query transformation
  - cost and latency tradeoffs
  - agentic retrieval

---

## Related Notes

- [[00 Raw Sources/Articles/Microsoft Learn Search and RAG Docs - Manifest]]
- [[02 AI Systems/RAG/Retrieval/RAG - Hybrid Retrieval]]
- [[02 AI Systems/RAG/Retrieval/05 - Reranking]]
- [[02 AI Systems/RAG/Core/02 - Chunking Strategies]]
- [[02 AI Systems/RAG/Core/04 - Query Transformation]]
- [[02 AI Systems/RAG/Retrieval/RAG - Query Routing and Retrieval Strategy]]
- [[02 AI Systems/RAG/Core/RAG - Agentic RAG]]
- [[02 AI Systems/RAG/Core/Agentic RAG - Planning and Retrieval Loop]]
- [[02 AI Systems/RAG/Core/09 - Cost and Latency Tradeoffs]]

---

## Official References

- Vector Search Overview: https://learn.microsoft.com/en-us/azure/search/vector-search-overview
- Hybrid Search Overview: https://learn.microsoft.com/en-us/azure/search/hybrid-search-overview
- Semantic Ranking Overview: https://learn.microsoft.com/en-us/azure/search/semantic-search-overview
- Chunk and Vectorize by Document Layout: https://learn.microsoft.com/en-us/azure/search/search-how-to-semantic-chunking
- Retrieval-Augmented Generation in Azure AI Search: https://learn.microsoft.com/en-us/azure/search/retrieval-augmented-generation-overview
- Agentic Retrieval Overview: https://learn.microsoft.com/en-us/azure/search/agentic-retrieval-overview
- Agentic Retrieval Quickstart: https://learn.microsoft.com/en-us/azure/search/search-get-started-agentic-retrieval
