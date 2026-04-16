---
tags:
  - engineering
  - rag
  - decision
type: note
status: evergreen
source: ""
parent_note: "[[06 Engineering/RAG/RAG - MOC]]"
---

# Decision - Choose a Retrieval Strategy

decision note สำหรับเลือกว่า RAG ควรใช้ retrieval แบบไหนในระบบนี้

---

## Context

- ข้อมูลอยู่ที่ไหน
- query มีลักษณะแน่นอนหรือกว้าง
- ต้องการ recall หรือ precision มากกว่า
- token budget จำกัดแค่ไหน

## Options

- lexical retrieval
- dense retrieval
- hybrid retrieval
- reranking

## Criteria

- accuracy
- latency
- cost
- maintainability
- integration complexity

## Decision

บันทึกทางเลือกที่เลือกและเหตุผล

## Consequences

- ได้อะไร
- เสียอะไร
- สิ่งที่ต้อง monitor
