---
tags:
  - synthesis
  - derived
  - memory
  - rag
  - context
type: synthesis
status: evergreen
source: "vault-local synthesis"
parent_note: "[[Home]]"
---

# Synthesis - Memory vs RAG vs Context

## Summary

สามชั้นนี้แก้คนละปัญหา:

- `context` คือสิ่งที่ model เห็นตอนนี้
- `memory` คือสิ่งที่ระบบจำข้ามรอบ
- `RAG` คือการดึง knowledge ภายนอกมา grounding คำตอบในรอบนั้น

## Quick Decision

- ข้อมูลต้องใช้ตอนนี้ → context
- ต้องจำข้ามรอบ → memory
- ต้องอิงเอกสาร/แหล่งข้อมูล → RAG
- ต้องการทั้ง continuity และ grounding → ใช้ memory + RAG ร่วมกัน

## Canonical Notes To Read Instead

| ต้องการ | ไปอ่าน |
|---|---|
| working memory vs long-term memory | [[02 AI Systems/Memory Systems/Core/01 - Working Memory vs Long-Term Memory]] |
| memory taxonomy | [[02 AI Systems/Memory Systems/Core/02 - Episodic vs Semantic vs Procedural Memory]] |
| read/write policies | [[02 AI Systems/Memory Systems/Core/03 - Memory Read and Write Policies]] |
| retrieval vs RAG | [[02 AI Systems/Memory Systems/Core/06 - Memory Retrieval vs RAG]] |
| RAG pipeline | [[02 AI Systems/RAG/RAG - MOC]] |

## Cross Links

- [[02 AI Systems/Memory Systems/Memory Systems - MOC]]
- [[02 AI Systems/RAG/RAG - MOC]]
- [[04 Synthesis/Synthesis - Agent vs Workflow vs RAG]]
- [[01 Foundations/Context Windows/Context Windows - MOC]]
- [[Home]]
