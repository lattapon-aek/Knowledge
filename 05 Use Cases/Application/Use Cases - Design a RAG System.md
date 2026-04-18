---
tags:
  - usecase
  - rag
  - retrieval
type: usecase
status: evergreen
source: ""
parent_note: "[[05 Use Cases/Use Cases - MOC]]"
---

# Use Cases - Design a RAG System

## Summary

ใช้ note นี้เมื่อกำลังออกแบบระบบ RAG ตั้งแต่การเลือก retrieval pipeline ไปจนถึง grounding, evaluation, และ trade-offs ด้าน cost/latency

รายละเอียดเชิงลึกของ retrieval, chunking, reranking, context assembly, และ eval ให้อยู่ใน canonical notes ของ `RAG` แล้ว ใช้ note นี้เป็น decision path เพื่อเลือกชั้นที่ต้องประกอบเท่านั้น

## Canonical Notes

- [[02 AI Systems/RAG/RAG - MOC]]
- [[04 Synthesis/Bridge/Synthesis - Memory vs RAG vs Context]]
- [[04 Synthesis/Decision/Synthesis - Prompting vs Fine-tuning vs RAG]]

---

## ใช้เมื่อไร

ใช้ note นี้เมื่อ:
- ต้องออกแบบ knowledge retrieval สำหรับ chatbot หรือ agent
- ต้องตัดสินใจระหว่าง long context, RAG, hybrid retrieval, หรือ agentic retrieval
- ต้องคุยกับ agent ให้ชัดว่า RAG system นี้ควรมีชั้นอะไรบ้าง

---

## Step 1: นิยาม retrieval problem ก่อน

ตอบคำถามเหล่านี้ก่อน:
- แหล่งข้อมูลเป็น structured, semi-structured, หรือ unstructured
- query ของผู้ใช้สั้น ตรง หรือซับซ้อน
- ต้องการ freshness แค่ไหน
- ต้องมี citation หรือ grounding ระดับไหน
- latency budget เท่าไร

ถ้ายังตอบไม่ได้ การออกแบบ RAG จะกว้างเกินไป

---

## Step 2: ออกแบบ retrieval pipeline

ลำดับที่ควรถาม:
1. chunk documents อย่างไร
2. จะใช้ lexical, vector, หรือ hybrid retrieval
3. ต้องมี query transformation หรือไม่
4. ต้องมี reranking หรือไม่
5. จะประกอบ context ก่อนส่งเข้า model อย่างไร

---

## Step 3: ตัดสินใจเรื่อง grounding

ถามให้ชัดว่า:
- คำตอบต้องอ้างแหล่งที่มาไหม
- citation ต้องละเอียดระดับ document หรือ passage
- ถ้า retrieval ไม่พอ จะตอบแบบไม่มั่นใจ, ขอข้อมูลเพิ่ม, หรือ fallback

---

## Step 4: ใส่ evaluation ตั้งแต่ต้น

ควรวัดอย่างน้อย 3 ชั้น:
- retrieval quality
- grounding / citation quality
- answer quality

ถ้าข้ามขั้นนี้ไป จะวินิจฉัยไม่ได้ว่าปัญหาอยู่ที่ retrieval หรือ generation

---

## Heuristic แบบเร็ว

| สถานการณ์ | แนวทางที่มักเหมาะ |
|---|---|
| ข้อมูลเป็นเอกสารทั่วไป, query ตรง | basic vector หรือ hybrid RAG |
| query หลากหลายและ lexical signal สำคัญ | hybrid retrieval |
| query ซับซ้อนหลายเงื่อนไข | query transformation + reranking |
| ข้อมูลเป็น entities และ relationships ชัด | knowledge graph RAG |
| ต้องค้นหลายรอบหรือวางแผน query | agentic RAG |

---

## Anti-Patterns

- เริ่มจาก vector DB ก่อนโดยยังไม่เข้าใจ retrieval problem
- chunk เล็กหรือใหญ่เกินไปโดยไม่ดู answer task
- วัดแค่ answer quality แล้วสรุปว่า retrieval ดี
- ไม่มี citation policy แต่คาดหวัง grounded answers
- ใช้ agentic RAG ทั้งที่ use case ยังเป็น retrieval ตรงไปตรงมา

---

## Recommended Reading

1. [[02 AI Systems/RAG/Core/01 - Retrieval Basics]]
2. [[02 AI Systems/RAG/Core/02 - Chunking Strategies]]
3. [[02 AI Systems/RAG/Retrieval/03 - Embeddings and Vector Databases]]
4. [[02 AI Systems/RAG/Core/04 - Query Transformation]]
5. [[02 AI Systems/RAG/Retrieval/05 - Reranking]]
6. [[02 AI Systems/RAG/Core/06 - Context Assembly]]
7. [[02 AI Systems/RAG/Core/07 - Grounding and Citation]]
8. [[02 AI Systems/RAG/Evaluation/08 - Evaluation]]
9. [[02 AI Systems/RAG/Core/09 - Cost and Latency Tradeoffs]]

---

## Cross Links

- [[02 AI Systems/RAG/RAG - MOC]]
- [[04 Synthesis/Decision/Synthesis - Agent vs Workflow vs RAG]]
- [[04 Synthesis/Bridge/Synthesis - Memory vs RAG vs Context]]
- [[Home]]
