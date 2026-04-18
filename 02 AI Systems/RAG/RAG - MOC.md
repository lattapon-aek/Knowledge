---
tags:
  - rag
  - moc
  - retrieval
type: moc
status: evergreen
source: ""
parent_note: "[[Home]]"
---

# RAG - MOC

> โครงความรู้สำหรับ Retrieval-Augmented Generation ในเชิงระบบและสถาปัตยกรรม

---

## Scope

RAG คือการดึงข้อมูลภายนอกที่เกี่ยวข้องเข้ามาใน runtime context ก่อนให้โมเดลตอบ เพื่อลด knowledge gap และเพิ่ม grounding

หมวดนี้เป็น canonical home ของ retrieval pipeline, chunking, reranking, context assembly, grounding, และ RAG evaluation  
ถ้าพูดถึง memory continuity หรือ personalization ให้ไป `Memory Systems` แทน
ถ้าเป็น read/write policy, memory taxonomy, session persistence, หรือ long-term recall ให้ไป `Memory Systems` แทน ไม่เล่าซ้ำในหมวด RAG

กติกาการอ่าน:
- ไฟล์ที่มีเลข `01, 02, 03...` คือ core learning path
- ไฟล์ที่ไม่มีเลขคือหัวข้อ advanced หรือ pattern เฉพาะทาง

---

## Notes Map

- [[02 AI Systems/RAG/Core/01 - Retrieval Basics|Retrieval basics]]
- [[02 AI Systems/RAG/Core/02 - Chunking Strategies|Chunking strategies]]
- [[02 AI Systems/RAG/Retrieval/03 - Embeddings and Vector Databases|Embeddings and vector search]]
- [[02 AI Systems/RAG/Core/04 - Query Transformation|Query transformation]]
- [[02 AI Systems/RAG/Retrieval/05 - Reranking|Reranking]]
- [[02 AI Systems/RAG/Core/06 - Context Assembly|Context assembly]]
- [[02 AI Systems/RAG/Core/07 - Grounding and Citation|Grounding and citation]]
- [[02 AI Systems/RAG/Evaluation/08 - Evaluation|RAG evaluation]]
- [[02 AI Systems/RAG/Core/09 - Cost and Latency Tradeoffs|Cost and latency tradeoffs]]
- [[02 AI Systems/RAG/Retrieval/RAG - Hybrid Retrieval|Hybrid retrieval]]
- [[02 AI Systems/RAG/Retrieval/RAG - Knowledge Graph RAG|Knowledge Graph RAG]]
- [[02 AI Systems/RAG/Core/RAG - Agentic RAG|Agentic RAG]]

---

## Related Notes

- [[01 Foundations/LLM Foundations/Core/04 - Inference, Context และ RAG]]
- [[01 Foundations/Context Windows/Context Windows - MOC]]
- [[01 Foundations/Prompt Engineering/Prompt Engineering - MOC]]
- [[01 Foundations/LLM Foundations/Core/10 - Embeddings และ Semantic Similarity]]
- [[01 Foundations/LLM Foundations/Core/14 - Vector Representations และ Similarity Search]]
- [[04 Synthesis/Synthesis - Weights, Context, Retrieval และ Tools]]
- [[02 AI Systems/Memory Systems/Memory Systems - MOC]]
- [[02 AI Systems/Memory Systems/Core/06 - Memory Retrieval vs RAG]]
- [[04 Synthesis/Synthesis - Memory vs RAG vs Context]]
- [[02 AI Systems/AI Agent Fundamentals/07 - รูปแบบ Agent Architectures]]
- [[02 AI Systems/Agent Frameworks/Agent Frameworks - MOC]]
- [[02 AI Systems/MCP/14 - Tools: การออกแบบและทำงาน]]
- [[02 AI Systems/Evals/Evals - MOC]]
- [[04 Synthesis/Synthesis - Agent vs Workflow vs RAG]]
- [[04 Synthesis/Synthesis - Prompting vs Fine-tuning vs RAG]]

---

## Learning Path

### 1. Foundations Before RAG

1. [[01 Foundations/LLM Foundations/Core/04 - Inference, Context และ RAG]]
2. [[01 Foundations/Context Windows/Core/01 - Context Window คืออะไร]]
3. [[01 Foundations/LLM Foundations/Core/10 - Embeddings และ Semantic Similarity]]
4. [[01 Foundations/LLM Foundations/Core/14 - Vector Representations และ Similarity Search]]
5. [[04 Synthesis/Synthesis - Weights, Context, Retrieval และ Tools]]

### 2. Core RAG Pipeline

1. [[02 AI Systems/RAG/Core/01 - Retrieval Basics]]
2. [[02 AI Systems/RAG/Core/02 - Chunking Strategies]]
3. [[02 AI Systems/RAG/Retrieval/03 - Embeddings and Vector Databases]]
4. [[02 AI Systems/RAG/Core/04 - Query Transformation]]
5. [[02 AI Systems/RAG/Retrieval/05 - Reranking]]
6. [[02 AI Systems/RAG/Core/06 - Context Assembly]]
7. [[02 AI Systems/RAG/Core/07 - Grounding and Citation]]

### 3. Quality and Operations

1. [[02 AI Systems/RAG/Evaluation/08 - Evaluation]]
2. [[02 AI Systems/RAG/Core/09 - Cost and Latency Tradeoffs]]

### 4. Advanced RAG Patterns

1. [[02 AI Systems/RAG/Retrieval/RAG - Hybrid Retrieval]]
2. [[02 AI Systems/RAG/Retrieval/RAG - Knowledge Graph RAG]]
3. [[02 AI Systems/RAG/Core/RAG - Agentic RAG]]

### 5. Synthesis

1. [[04 Synthesis/Synthesis - Agent vs Workflow vs RAG]]
2. [[04 Synthesis/Synthesis - Prompting vs Fine-tuning vs RAG]]
3. [[04 Synthesis/Synthesis - Memory vs RAG vs Context]]

---

## Next Notes To Create

- RAG - Multi-Source Retrieval

## Implementation Bridge

- [[06 Engineering/README]]
- [[06 Engineering/RAG/RAG - MOC]]
- [[Knowledge Topic Registry]]
