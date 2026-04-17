---
tags:
  - memory
  - rag
  - retrieval
  - comparison
type: note
status: draft
source: "Google ADK, Microsoft Learn, OpenAI Docs"
parent_note: "[[Memory Systems - MOC]]"
---

# Memory Retrieval vs RAG

> Bridge note สำหรับแยก memory retrieval กับ RAG retrieval แบบสั้น ๆ

---

## Summary

memory retrieval กับ RAG retrieval ใช้ primitive คล้ายกัน แต่ intent ต่างกัน

- memory retrieval → continuity, personalization, prior interactions
- RAG retrieval → external knowledge, grounding, evidence

## Canonical Notes To Read Instead

| ต้องการ | ไปอ่าน |
|---|---|
| memory continuity / personalization | [[02 AI Systems/Memory Systems/Core/01 - Working Memory vs Long-Term Memory]] |
| memory taxonomy | [[02 AI Systems/Memory Systems/Core/02 - Episodic vs Semantic vs Procedural Memory]] |
| read/write policies | [[02 AI Systems/Memory Systems/Core/03 - Memory Read and Write Policies]] |
| retrieval grounding / document evidence | [[02 AI Systems/RAG/RAG - MOC]] |
| RAG pipeline | [[02 AI Systems/RAG/RAG - MOC]] |

## Quick Decision

- ต้องการจำผู้ใช้ / งาน / ความต่อเนื่อง → memory
- ต้องการตอบจากเอกสารหรือ knowledge base → RAG
- ต้องการทั้งสองอย่าง → memory + RAG ร่วมกัน

## Cross Links

- [[02 AI Systems/Memory Systems/Memory Systems - MOC]]
- [[02 AI Systems/RAG/RAG - MOC]]
- [[04 Synthesis/Synthesis - Memory vs RAG vs Context]]
