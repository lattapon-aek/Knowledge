---
tags:
  - synthesis
  - derived
  - agents
  - memory
type: synthesis
status: evergreen
created: "2026-04-12"
source: "vault-local synthesis"
parent_note: "[[Home]]"
---

# Memory in Agents

## Summary

memory ใน agent คือการจัดการข้อมูลข้ามรอบให้เหมาะกับงานนั้น ๆ โดยมักประกอบด้วย context ตอนนี้, session-scoped state, และ long-term memory ที่เรียกกลับมาใช้ได้

## Use the Canonical Notes For

- working memory vs long-term memory → [[02 AI Systems/Memory Systems/Core/01 - Working Memory vs Long-Term Memory]]
- episodic / semantic / procedural taxonomy → [[02 AI Systems/Memory Systems/Core/02 - Episodic vs Semantic vs Procedural Memory]]
- read/write policies → [[02 AI Systems/Memory Systems/Core/03 - Memory Read and Write Policies]]
- memory retrieval vs RAG → [[02 AI Systems/Memory Systems/Core/06 - Memory Retrieval vs RAG]]

## Practical View

- ถ้าข้อมูลต้องใช้ทันทีในรอบนี้: อยู่ใน context
- ถ้าต้องเก็บไว้ข้ามรอบ: external memory store
- ถ้าต้องคุมพฤติกรรม agent: prompt, policy, หรือ reusable workflow

## Cross Links

- [[01 Foundations/Context Windows/Context Windows - MOC]]
- [[02 AI Systems/Memory Systems/Memory Systems - MOC]]
- [[02 AI Systems/RAG/RAG - MOC]]
- [[04 Synthesis/Synthesis - Memory vs RAG vs Context]]
- [[Home]]
