---
tags:
  - engineering
  - memory
  - decision
type: note
status: evergreen
source: "vault-local engineering"
parent_note: "[[06 Engineering/Memory/Memory - MOC]]"
---

# Decision - Choose a Memory Policy

decision note สำหรับเลือกว่าจะเก็บอะไรเป็น memory และเก็บอย่างไร

---

## Context

- ข้อมูลนี้ต้องจำข้าม turn หรือไม่
- transient state พอไหม
- privacy หรือ retention constraint มีไหม

## Options

- no memory
- session memory
- profile memory
- long-term memory

## Criteria

- usefulness
- freshness
- privacy
- retrieval quality

## Decision

บันทึก policy ที่เลือก

## Consequences

- personalization
- stale memory risk
- storage and governance overhead
