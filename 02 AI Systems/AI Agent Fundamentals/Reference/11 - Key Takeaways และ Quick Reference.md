---
tags:
  - agent
  - summary
  - reference
type: note
status: evergreen
source: "Google Skills — Agent Fundamentals (Module 4) · ทั้งคอร์ส"
parent_note: "[[AI Agent Fundamentals - MOC]]"
---

# Key Takeaways และ Quick Reference



---

## สรุปสุดท้ายในประโยคเดียว

> **Agent คือระบบที่ใช้ model เพื่อคิด ใช้ tools เพื่อทำ และใช้ orchestration เพื่อวนทำงานจน goal สำเร็จ**

---

## Key Takeaways รวมทั้งคอร์ส

- **Agents ≠ Chatbots** — agent คือระบบที่ perceive → reason → act ไม่ใช่แค่ระบบสนทนา
- **Architecture matters** — ความสามารถเกิดจาก model + tools + orchestration ที่ทำงานร่วมกัน
- **Tools คือ superpowers** — ถ้าไม่มี tools model ยังแตะโลกจริงไม่ได้
- **Not everything needs an agent** — บางงานควรใช้ script, workflow automation, direct API, retrieval, หรือ chatbot ธรรมดา
- **Autonomy คือแก่น** — ตัวแบ่งสำคัญคือการทำงานเพื่อ goal ได้ต่อเนื่องโดยไม่ต้องสั่งทุก step

---

## Quick Reference Card

| หัวข้อ | สาระ |
|---|---|
| Agent คืออะไร | ระบบอัตโนมัติที่พยายามบรรลุเป้าหมายโดยการสังเกตและลงมือทำใน environment |
| สามองค์ประกอบหลัก | Model · Tools · Orchestration |
| Agent loop | Perceive → Think → Act → Check → Repeat until done |
| ควรใช้ agent เมื่อ | Multi-step · Need adaptation · Need reasoning · Need external actions |
| ไม่ควรใช้ agent เมื่อ | Simple single ops · Deterministic workflows · Real-time requirements · FAQ |
| ประเภท tools | Pre-built integrations · Custom functions · Information retrieval |

---

## สิ่งที่ควรทำได้หลังเรียนจบ

1. แยก LLM, function calling, และ agent ออกจากกันได้
2. อธิบายการทำงานร่วมกันของ model, tools, และ orchestration ได้
3. ประเมินได้ว่า use case ไหนควรใช้ agent หรือ solution ที่ง่ายกว่า
4. ออกแบบ high-level architecture ของ agent สำหรับ use case ต่าง ๆ ได้
5. หลีกเลี่ยง anti-pattern และ over-engineering ได้

---

## Reflection Questions

ใช้คำถามเหล่านี้เพื่อแปลงทฤษฎีเป็นการออกแบบจริง:

1. งานซ้ำ ๆ ในงานประจำของคุณมีงานไหนที่เป็น multi-step, adaptive, และ reasoning-intensive บ้าง?
2. ถ้าจะสร้าง customer service agent สำหรับ order cancellation — ควรใช้ pre-built integration หรือ custom function และเพราะอะไร?
3. ระบบ recommendation สำหรับ e-commerce ควรเป็น single agent หรือหลาย specialized agents?
4. ถ้าเลือก 3 งานที่ทำเป็นประจำ งานไหนควรใช้ agent และงานไหนควรใช้ script หรือ automation ธรรมดา?

---

## Resource List (จาก Google Skills)

### จาก Google
- Intro to AI Agents
- Workflows versus agents
- The Agent Factory – Episode 1: Agents
- Conversational versus non-conversational AI Agents

### จาก Community
- From gen AI to agentic AI: Everything you need to know – Part 1 and Part 2

---

## ดูต่อ

- [[AI Agent Fundamentals - MOC]]
- [[05 Use Cases/Decision/Use Cases - When to Use an Agent|When to Use an Agent]]
- [[10 - Risks และ Best Practices]]
