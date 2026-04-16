---
tags:
  - synthesis
  - derived
  - agent
  - workflow
  - rag
type: synthesis
status: evergreen
created: "2026-04-12"
source: "vault-local synthesis"
parent_note: "[[Home]]"
---

# Agent vs Workflow vs RAG

## Summary

สามอย่างนี้แก้คนละปัญหา:

- `Workflow` ใช้เมื่อขั้นตอนชัดและ deterministic
- `RAG` ใช้เมื่อปัญหาคือข้อมูลไม่พอหรืออยากลด hallucination
- `Agent` ใช้เมื่อระบบต้องตัดสินใจเลือก step หรือ tool เองระหว่างทาง

---

## Quick Decision

- งานเป็นลำดับแน่นอน: ใช้ workflow
- งานต้องดึงความรู้ภายนอกแบบแม่น: ใช้ RAG
- งานต้องวางแผน ปรับตัว หรือเลือกเครื่องมือเอง: ใช้ agent

---

## Cross Links

- [[02 AI Systems/AI Agent Fundamentals/08 - Workflow vs AI Agent]]
- [[02 AI Systems/AI Agent Fundamentals/09 - เมื่อไรควรและไม่ควรใช้ Agent]]
- [[01 Foundations/LLM Foundations/04 - Inference, Context และ RAG]]
- [[Home]]
