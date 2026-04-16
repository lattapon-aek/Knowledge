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

memory ใน agent ไม่ได้มีแบบเดียว ควรแยกให้ออกระหว่างสิ่งที่อยู่ใน context ตอนนี้ กับสิ่งที่เก็บไว้นอกโมเดลแล้วเรียกกลับมาใช้

---

## Types of Memory

- Working memory: ข้อมูลที่อยู่ใน context window ของรอบนั้น
- Episodic memory: บันทึกเหตุการณ์หรือผลลัพธ์จากรอบก่อน
- Semantic memory: ข้อเท็จจริงหรือ knowledge base ที่ค้นคืนได้
- Procedural memory: กฎ วิธีทำงาน หรือ system instructions ที่ใช้ซ้ำ

---

## Practical View

- ถ้าข้อมูลต้องใช้ทันทีในรอบนี้: อยู่ใน context
- ถ้าต้องเก็บไว้ข้ามรอบ: external memory store
- ถ้าต้องคุมพฤติกรรม agent: prompt, policy, หรือ reusable workflow

---

## Cross Links

- [[01 Foundations/Context Windows/Context Windows - MOC]]
- [[02 AI Systems/AI Agent Fundamentals/05 - วงจร Perceive-Think-Act-Check]]
- [[02 AI Systems/AI Agent Fundamentals/14 - Tools: การออกแบบและทำงาน]]
- [[02 AI Systems/MCP/MCP - MOC]]
- [[Home]]
