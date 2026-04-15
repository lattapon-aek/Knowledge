---
tags:
  - rawsources
  - manifest
  - microsoft
  - search
  - rag
  - officialdocs
type: reference
status: evergreen
source: "https://learn.microsoft.com/en-us/azure/search/vector-search-overview"
parent_note: "[[Source Manifests - MOC]]"
---

# Microsoft Learn Search and RAG Docs - Manifest

## Source Family

Official docs family:
- `https://learn.microsoft.com/en-us/azure/search/vector-search-overview`
- `https://learn.microsoft.com/en-us/azure/search/hybrid-search-overview`
- `https://learn.microsoft.com/en-us/azure/search/hybrid-search-how-to-query`
- `https://learn.microsoft.com/en-us/azure/search/semantic-ranking`
- `https://learn.microsoft.com/en-us/azure/search/semantic-how-to-query-request`
- `https://learn.microsoft.com/en-us/azure/search/semantic-how-to-query-rewrite`
- `https://learn.microsoft.com/en-us/azure/search/semantic-how-to-configure`
- `https://learn.microsoft.com/en-us/azure/search/search-how-to-semantic-chunking`
- `https://learn.microsoft.com/en-us/azure/search/search-agentic-retrieval-concept`
- `https://learn.microsoft.com/en-us/azure/search/search-get-started-agentic-retrieval`
- `https://learn.microsoft.com/en-us/azure/search/search-what-is-azure-search`
- `https://learn.microsoft.com/en-us/azure/search/search-sku-manage-costs`

---

## Used By

- [[02 AI Systems/RAG/Retrieval/RAG - Hybrid Retrieval]]
- [[02 AI Systems/RAG/Retrieval/03 - Embeddings and Vector Databases]]
- [[02 AI Systems/RAG/Retrieval/05 - Reranking]]
- [[02 AI Systems/RAG/Core/02 - Chunking Strategies]]
- [[02 AI Systems/RAG/Core/04 - Query Transformation]]
- [[02 AI Systems/RAG/Core/RAG - Agentic RAG]]
- [[02 AI Systems/RAG/Core/09 - Cost and Latency Tradeoffs]]

---

## Ingest Notes

- กลุ่มนี้เป็น backbone ของหมวด `RAG` ฝั่ง retrieval infrastructure
- เหมาะกับการ ingest ต่อเมื่อจะขยาย `hybrid`, `semantic ranking`, `agentic retrieval`, และ `cost tradeoffs`
- ใช้ร่วมกับ [[00 Raw Sources/Source Records/Official Documentation Bundles - Source Record|Official Documentation Bundles - Source Record]]
