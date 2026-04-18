---
tags:
  - rawsources
  - ingest
  - rag
  - agenticrag
  - officialdocs
type: plan
status: draft
source: "vault-local ingest plan"
parent_note: "[[Source Manifests - MOC]]"
created: "2026-04-18"
updated: "2026-04-18"
---

# Advanced RAG and Agentic RAG - Ingest Plan

แผนนี้ใช้เตรียม ingest แหล่งข้อมูลสำหรับขยายหมวด `RAG` จาก core pipeline ไปสู่ `Advanced RAG` และ `Agentic RAG`

หลักการ:
- ใช้เฉพาะ official docs, primary docs, หรือบริษัทเทคที่เป็นเจ้าของ ecosystem สำคัญ
- raw source / manifest อยู่ใน `00 Raw Sources`
- knowledge note ปลายทางอยู่ใน `02 AI Systems/RAG`, `04 Synthesis`, `05 Use Cases`, หรือ `06 Engineering`
- ไม่ rewrite เนื้อหาเดิมก่อนอ่าน source จริง
- ถ้า claim เป็น design inference ให้ระบุว่าเป็น `architectural inference`

---

## Current Baseline

vault ตอนนี้มี RAG core แล้ว:

- [[02 AI Systems/RAG/Core/01 - Retrieval Basics]]
- [[02 AI Systems/RAG/Core/02 - Chunking Strategies]]
- [[02 AI Systems/RAG/Retrieval/03 - Embeddings and Vector Databases]]
- [[02 AI Systems/RAG/Core/04 - Query Transformation]]
- [[02 AI Systems/RAG/Retrieval/05 - Reranking]]
- [[02 AI Systems/RAG/Core/06 - Context Assembly]]
- [[02 AI Systems/RAG/Core/07 - Grounding and Citation]]
- [[02 AI Systems/RAG/Evaluation/08 - Evaluation]]
- [[02 AI Systems/RAG/Core/09 - Cost and Latency Tradeoffs]]
- [[02 AI Systems/RAG/Retrieval/RAG - Hybrid Retrieval]]
- [[02 AI Systems/RAG/Retrieval/RAG - Knowledge Graph RAG]]
- [[02 AI Systems/RAG/Core/RAG - Agentic RAG]]

สิ่งที่ยังต้องเติมเพื่อให้เป็น advanced / agentic layer:
- multi-source retrieval
- query routing
- hierarchical / parent-child retrieval
- metadata filtering และ permission-aware retrieval
- ingestion and indexing pipeline
- retrieval observability
- RAG security และ source trust
- adaptive / fallback retrieval
- agentic retrieval loop
- agentic RAG evaluation และ failure modes

---

## Source Bundle 1: Advanced RAG Backbone

เป้าหมาย: เติมภาพรวม RAG ขั้นสูง, hybrid retrieval, reranking, grounding, และ managed RAG primitives

แหล่งข้อมูล:
- Microsoft Learn - RAG in Azure AI Search  
  `https://learn.microsoft.com/en-us/azure/search/retrieval-augmented-generation-overview`
- Microsoft Learn - Hybrid Search Overview  
  `https://learn.microsoft.com/en-us/azure/search/hybrid-search-overview`
- Microsoft Learn - Create a Hybrid Query  
  `https://learn.microsoft.com/en-us/azure/search/hybrid-search-how-to-query`
- Microsoft Learn - Semantic Ranker  
  `https://learn.microsoft.com/en-us/azure/search/semantic-search-overview`
- OpenAI - Retrieval Guide  
  `https://platform.openai.com/docs/guides/retrieval`
- OpenAI - File Search  
  `https://platform.openai.com/docs/guides/tools-file-search`
- AWS Bedrock - Retrieving information from Knowledge Bases  
  `https://docs.aws.amazon.com/bedrock/latest/userguide/kb-how-retrieval.html`
- AWS Bedrock - RetrieveAndGenerate  
  `https://docs.aws.amazon.com/bedrock/latest/userguide/kb-test-retrieve-generate.html`

Target notes:
- update [[02 AI Systems/RAG/Retrieval/RAG - Hybrid Retrieval]]
- update [[02 AI Systems/RAG/Retrieval/05 - Reranking]]
- update [[02 AI Systems/RAG/Core/06 - Context Assembly]]
- update [[02 AI Systems/RAG/Core/07 - Grounding and Citation]]
- update [[02 AI Systems/RAG/Evaluation/08 - Evaluation]]
- create `02 AI Systems/RAG/Retrieval/RAG - Multi-Source Retrieval.md`
- create `02 AI Systems/RAG/Retrieval/RAG - Query Routing and Retrieval Strategy.md`

Expected outputs:
- clear distinction between classic RAG, advanced RAG, and agentic retrieval
- diagram for advanced retrieval pipeline
- table of retrieval strategies: lexical, vector, hybrid, graph, file search, managed KB
- notes on reranking and context packing boundaries

---

## Source Bundle 2: Agentic RAG and Adaptive Retrieval

เป้าหมาย: เติม agentic retrieval loop, planning, subquery decomposition, iterative retrieval, fallback, และ trace

แหล่งข้อมูล:
- Microsoft Learn - Agentic Retrieval in Azure AI Search  
  `https://learn.microsoft.com/en-us/azure/search/search-agentic-retrieval-concept`
- Microsoft Learn - Agentic Retrieval Quickstart  
  `https://learn.microsoft.com/en-us/azure/search/search-get-started-agentic-retrieval`
- LlamaIndex - Agentic Strategies  
  `https://docs.llamaindex.ai/en/stable/optimizing/agentic_strategies/agentic_strategies/`
- LangGraph - Adaptive RAG  
  `https://langchain-ai.lang.chat/langgraph/tutorials/rag/langgraph_adaptive_rag/`
- LangGraph - Corrective RAG  
  `https://langchain-ai.lang.chat/langgraph/tutorials/rag/langgraph_crag/`
- OpenAI - File Search  
  `https://platform.openai.com/docs/guides/tools-file-search`

Target notes:
- expand [[02 AI Systems/RAG/Core/RAG - Agentic RAG]]
- create `02 AI Systems/RAG/Core/Agentic RAG - Planning and Retrieval Loop.md`
- create `02 AI Systems/RAG/Evaluation/Agentic RAG - Evaluation and Failure Modes.md`
- update [[02 AI Systems/AI Agent Fundamentals/Core/07 - รูปแบบ Agent Architectures]]
- update [[04 Synthesis/Decision/Synthesis - Agent vs Workflow vs RAG]]

Expected outputs:
- mermaid diagram: plan -> retrieve -> inspect -> decide -> retrieve again or answer
- stopping criteria and retrieval budget
- failure modes: bad decomposition, wrong tool/source, loop drift, over-retrieval, citation mismatch
- eval dimensions: planning quality, routing accuracy, retrieval usefulness, grounded final answer

---

## Source Bundle 3: Retrieval Controls, Metadata, Permissions, and Trust

เป้าหมาย: เติม control layer ที่ทำให้ RAG ใช้งานจริงได้ปลอดภัยและ trace ได้

แหล่งข้อมูล:
- OpenAI - Retrieval Guide: attribute filtering, ranking options, chunking  
  `https://platform.openai.com/docs/guides/retrieval`
- AWS - Knowledge Bases metadata filtering  
  `https://aws.amazon.com/about-aws/whats-new/2024/03/knowledge-bases-amazon-bedrock-metadata-filtering/`
- AWS Bedrock - RetrieveAndGenerate guardrails note  
  `https://docs.aws.amazon.com/bedrock/latest/userguide/kb-test-retrieve-generate.html`
- Google Cloud - Check grounding with RAG  
  `https://docs.cloud.google.com/generative-ai-app-builder/docs/check-grounding`
- Google Cloud - Ground responses using RAG  
  `https://docs.cloud.google.com/vertex-ai/generative-ai/docs/grounding/ground-responses-using-rag`

Target notes:
- create `02 AI Systems/RAG/Retrieval/RAG - Metadata Filtering and Permission-Aware Retrieval.md`
- create `02 AI Systems/RAG/Core/RAG - Security and Source Trust.md`
- update [[02 AI Systems/RAG/Core/07 - Grounding and Citation]]
- update [[02 AI Systems/Guardrails/Core/Guardrails - Prompt Injection and Content Attacks]]
- update [[02 AI Systems/Guardrails/Core/03 - Tool Safety]]
- update [[02 AI Systems/Evals/Application/07 - RAG Evals]]

Expected outputs:
- distinction between retrieval filtering, authorization, and generation guardrails
- note that retrieved references may not be covered by model guardrails unless the system explicitly controls them
- source trust taxonomy: official, internal approved, user-uploaded, web, unknown
- citation quality checklist

---

## Source Bundle 4: Graph, Hybrid, and Specialized Retrieval Patterns

เป้าหมาย: เติม advanced retrieval patterns ที่ beyond vector-only

แหล่งข้อมูล:
- Neo4j - GraphRAG  
  `https://neo4j.com/labs/genai-ecosystem/graphrag/`
- Pinecone - Hybrid Search  
  `https://docs.pinecone.io/docs/hybrid-search`
- Qdrant - Hybrid Search with Reranking  
  `https://qdrant.tech/documentation/advanced-tutorials/reranking-hybrid-search/`
- Weaviate - Retrieval Augmented Generation  
  `https://docs.weaviate.io/weaviate/search/generative`
- LangChain - Retrievers  
  `https://docs.langchain.com/oss/python/integrations/retrievers`
- LangChain - SelfQueryRetriever  
  `https://api.python.langchain.com/en/latest/langchain/retrievers/langchain.retrievers.self_query.base.SelfQueryRetriever.html`
- LangChain - ParentDocumentRetriever  
  `https://api.python.langchain.com/en/latest/langchain/retrievers/langchain.retrievers.parent_document_retriever.ParentDocumentRetriever.html`

Target notes:
- update [[02 AI Systems/RAG/Retrieval/RAG - Hybrid Retrieval]]
- update [[02 AI Systems/RAG/Retrieval/RAG - Knowledge Graph RAG]]
- create `02 AI Systems/RAG/Retrieval/RAG - Hierarchical and Parent-Child Retrieval.md`
- update [[06 Engineering/RAG/Decision - Choose a Retrieval Strategy]]

Expected outputs:
- graph vs vector vs hybrid decision table
- parent-child retrieval diagram
- notes on exact-match identifiers, metadata-heavy queries, relationship-heavy queries, and semantic queries

---

## Source Bundle 5: Ingestion and Indexing Pipeline

เป้าหมาย: เติมฝั่งก่อน retrieval ซึ่งตอนนี้ยังบางกว่า retrieval side

แหล่งข้อมูล:
- OpenAI - Retrieval Guide: vector store files, chunking strategy, attributes, expiration  
  `https://platform.openai.com/docs/guides/retrieval`
- Azure AI Search - indexing concepts and vector/hybrid search docs  
  `https://learn.microsoft.com/en-us/azure/search/retrieval-augmented-generation-overview`
- AWS Bedrock Knowledge Bases retrieval docs  
  `https://docs.aws.amazon.com/bedrock/latest/userguide/kb-how-retrieval.html`
- Weaviate RAG docs  
  `https://docs.weaviate.io/weaviate/search/generative`

Target notes:
- create `02 AI Systems/RAG/Core/RAG - Ingestion and Indexing Pipeline.md`
- update [[02 AI Systems/RAG/Core/02 - Chunking Strategies]]
- update [[02 AI Systems/RAG/Retrieval/03 - Embeddings and Vector Databases]]
- update [[06 Engineering/RAG/Recipe - Build a RAG Pipeline]]

Expected outputs:
- pipeline: source -> parse -> clean -> chunk -> enrich metadata -> embed -> index -> refresh -> retrieve
- indexing failure modes: stale index, duplicate chunks, bad metadata, embedding mismatch, reindex gap
- lifecycle: add, update, delete, expiration, reindex

---

## Recommended Ingest Order

1. Microsoft Agentic Retrieval + Microsoft RAG Overview
2. OpenAI Retrieval + File Search
3. Google Grounding + Check Grounding
4. AWS Bedrock Knowledge Bases retrieval + metadata filtering
5. Azure Hybrid Search + Semantic Ranker
6. Neo4j GraphRAG + Pinecone/Qdrant Hybrid Search
7. LlamaIndex Agentic Strategies + LangGraph Adaptive/Corrective RAG
8. LangChain retriever patterns for parent-child / self-query / retriever interface

เหตุผล:
- เริ่มจาก vendor docs ที่นิยาม architecture ก่อน
- เติม grounding/eval/security ก่อนลง framework patterns
- ใช้ framework docs เป็น implementation pattern ไม่ใช่ source ของ core theory ทั้งหมด

---

## Planned Wiki Notes

ควรสร้างเพิ่มใน `02 AI Systems/RAG`:

- `Retrieval/RAG - Multi-Source Retrieval.md`
- `Retrieval/RAG - Query Routing and Retrieval Strategy.md`
- `Retrieval/RAG - Metadata Filtering and Permission-Aware Retrieval.md`
- `Retrieval/RAG - Hierarchical and Parent-Child Retrieval.md`
- `Core/RAG - Ingestion and Indexing Pipeline.md`
- `Core/RAG - Security and Source Trust.md`
- `Core/Agentic RAG - Planning and Retrieval Loop.md`
- `Evaluation/Agentic RAG - Evaluation and Failure Modes.md`

ควรอัปเดต:
- [[02 AI Systems/RAG/RAG - MOC]]
- [[05 Use Cases/Application/Use Cases - Design a RAG System]]
- [[06 Engineering/RAG/RAG - MOC]]
- [[06 Engineering/RAG/Recipe - Build a RAG Pipeline]]
- [[06 Engineering/RAG/Decision - Choose a Retrieval Strategy]]
- [[04 Synthesis/Bridge/Synthesis - Memory vs RAG vs Context]]
- [[04 Synthesis/Decision/Synthesis - Agent vs Workflow vs RAG]]

---

## Ingest Checklist Per Source

ใช้ checklist นี้ทุกครั้งที่หยิบ source เข้า:

1. ระบุ source family และ URL
2. แยก fact จาก architectural inference
3. ระบุ target note หลัก 1 หน้า ก่อนแตก note เพิ่ม
4. อัปเดต `source:` หรือ `Official References` ใน note ที่แตะ
5. เพิ่ม cross-links กลับไปยัง `RAG - MOC`, `Evals - MOC`, `Guardrails - MOC`, `Agent Frameworks - MOC`, หรือ `Engineering - MOC` ตามจริง
6. ถ้าสร้าง note ใหม่ ให้เพิ่มเข้า `RAG - MOC`, `index.md`, และ `Knowledge Topic Registry.md` เมื่อเป็น canonical topic
7. ตรวจ broken links หลังจบ batch

---

## Done Criteria

ถือว่า ingest รอบนี้เสร็จเมื่อ:

- Advanced RAG แยกออกจาก core RAG ชัด
- Agentic RAG มี loop, planning, tool/source routing, budget, trace, และ eval
- มี note สำหรับ ingestion/indexing side ไม่ใช่มีแต่ retrieval side
- มี note สำหรับ metadata filtering / permission-aware retrieval / source trust
- RAG MOC มี learning path ที่อ่านจาก core -> advanced -> agentic ได้
- ทุก note ใหม่มี official references ชัด
- broken wikilinks เป็น `0`
