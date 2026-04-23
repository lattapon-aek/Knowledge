---
tags:
  - mcp
  - protocol
  - integration
  - agent
type: note
status: evergreen
source: "MCP/MCP_Knowledge_Base.md"
parent_note: "[[02 AI Systems/MCP/MCP - MOC|MCP - MOC]]"
---

# MCP คืออะไรและแก้ปัญหาอะไร



---

## MCP คืออะไร

**Model Context Protocol (MCP)** คือ open protocol สำหรับเชื่อม AI application เข้ากับ external tools, data sources, prompts และ workflow components ด้วยมาตรฐานเดียวกัน

แทนการเขียน integration แบบ custom ระหว่างแอปกับ tool ทีละคู่ MCP กำหนดมาตรฐานกลางที่ทุก implementation ใช้ร่วมกันได้

---

## ปัญหาที่ MCP แก้: M × N Integrations

**ก่อนมี MCP:**
- AI application แต่ละตัว ต้องรองรับ API/interface ของ integration แต่ละตัว
- Tool แต่ละตัว ต้องรองรับ host/client หลายรูปแบบ
- ผลคือ M × N integration paths, maintenance cost สูง, ecosystem แตก fragment

**หลังมี MCP:**
- AI application implement ฝั่ง client ตาม MCP มาตรฐานครั้งเดียว
- Tool/data provider implement ฝั่ง server ตาม MCP มาตรฐานครั้งเดียว
- M × N → M + N

---

## สิ่งที่ MCP ครอบคลุมและไม่ครอบคลุม

**MCP ครอบคลุม:**
- Protocol สำหรับ context exchange
- Message schema และ lifecycle
- Capability negotiation
- Standard features, utilities, transports

**MCP ไม่ได้บังคับ:**
- ว่า host ต้องใช้ LLM รุ่นไหน
- Prompt orchestration ภายใน host ต้องเป็นแบบไหน
- UX ของ approval/consent
- Business logic ของแต่ละ server

> MCP = มาตรฐานการคุยกัน ไม่ใช่ framework ที่กำหนดทุกอย่างของ agent runtime

---

## จำให้สั้นที่สุด

| Entity | คืออะไร |
|---|---|
| **Host** | แอป AI ที่ผู้ใช้ใช้งานจริง (AI desktop app, IDE, coding assistant) |
| **Client** | connector ภายใน host ที่คุยกับ MCP server แต่ละตัว |
| **Server** | บริการที่ expose capabilities ผ่าน MCP |
| **Tools** | ใช้ทำ action (execute, compute, call API) |
| **Resources** | ใช้ให้ context แบบอ่านข้อมูล |
| **Prompts** | ใช้เป็น template/workflow |

---

## ดูต่อ

- [[02 - Architecture_ Host, Client, Server]] — โครงสร้างและ layering
- [[03 - Core Primitives_ Tools, Resources, Prompts]] — capabilities ฝั่ง server
- [[02 AI Systems/MCP/MCP - MOC|MCP - MOC]]
