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

### 1. Agents ≠ Chatbots
Agent คือระบบ autonomous ที่ perceive → reason → act — ไม่ใช่แค่ระบบสนทนา

### 2. Architecture matters
ความสามารถของ agent ไม่ได้เกิดจาก prompt เก่งอย่างเดียว แต่เกิดจาก model + tools + orchestration ที่ทำงานร่วมกัน

### 3. Tools คือ superpowers
ถ้าไม่มี tools แม้ model จะฉลาด ก็ยังแตะโลกจริงไม่ได้

### 4. Not everything needs an agent
หลายปัญหาเหมาะกับ script, workflow automation, direct API, retrieval, หรือ chatbot ธรรมดามากกว่า

### 5. Autonomy คือแก่นของคำว่า Agent
ตัวแบ่งสำคัญที่สุดระหว่าง agent กับระบบประเภทอื่น คือความสามารถในการทำงานเพื่อเป้าหมายโดยอัตโนมัติและต่อเนื่อง

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

1. แยกความแตกต่างระหว่าง LLM, function calling, และ agent ได้ชัด
2. อธิบายการทำงานร่วมกันของ 3 components ภายใน agent loop ได้
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
- **Intro to AI Agents** — นิยาม capability, use cases, และ architecture ของ agents
- **Workflows versus agents** — เปรียบเทียบ agentic workflows กับ traditional workflows
- **The Agent Factory – Episode 1: Agents** — อธิบาย true AI agent และการเริ่มสร้างด้วย Agent Developer Kit
- **Conversational versus non-conversational AI Agents** — เปรียบเทียบ multi-turn conversational agents กับ single-turn patterns

### จาก Community
- **From gen AI to agentic AI: Everything you need to know – Part 1 and Part 2** — ว่าด้วยความสามารถของ agentic AI และความต่างจาก AI แบบเดิม

---

## ดูต่อ

- [[AI Agent Fundamentals - MOC]]
- [[09 - เมื่อไรควรและไม่ควรใช้ Agent]]
- [[10 - Risks และ Best Practices]]
