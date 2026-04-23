---
tags:
  - mcp
  - client
  - sampling
  - elicitation
type: note
status: evergreen
source: "MCP Official Docs - modelcontextprotocol.io"
parent_note: "[[02 AI Systems/MCP/MCP - MOC|MCP - MOC]]"
created: "2026-04-23"
updated: ""
---

# Client Features: Sampling, Roots, Elicitation

> recreated จาก MCP official docs (ชื่อไฟล์เดิมมี colon ซึ่ง Windows ไม่รองรับ)

---

## Client Primitives

นอกจาก server primitives (tools, resources, prompts) MCP ยังกำหนด primitives ที่ **clients expose ให้ servers** ใช้:

| Primitive | หน้าที่ | ใช้เมื่อ |
|---|---|---|
| **Sampling** | server ขอให้ client เรียก LLM completion | server ต้องการ LLM แต่ไม่อยากมี API key เอง |
| **Elicitation** | server ขอข้อมูลเพิ่มจาก user | ต้องการ confirmation หรือ input จากคน |
| **Logging** | server ส่ง log messages ไป client | debugging และ monitoring |

---

## Sampling

ให้ server request LLM completion จาก host ผ่าน client โดยไม่ต้องมี model SDK ใน server:

- server ส่ง `sampling/createMessage` พร้อม messages, model preferences, system prompt
- client เลือก model ที่เหมาะสมตาม preferences (cost, speed, intelligence priorities)
- client ส่ง completion กลับ

### Model Preferences

server ไม่ระบุ model ตรง ๆ แต่ใช้ preference system:

| Field | หน้าที่ |
|---|---|
| `hints` | แนะนำ model/family (เช่น "claude-3-sonnet") — advisory ไม่บังคับ |
| `costPriority` | 0-1, สูง = ต้องการถูก |
| `speedPriority` | 0-1, สูง = ต้องการเร็ว |
| `intelligencePriority` | 0-1, สูง = ต้องการ capable |

client map hints ไป model ที่มี — เช่น ถ้าไม่มี Claude อาจ map "sonnet" ไป Gemini ที่ capability ใกล้เคียง

---

## Elicitation

ให้ server ขอข้อมูลเพิ่มจาก user ผ่าน client:

- server ส่ง `elicitation/request` พร้อมคำถาม
- client แสดง UI ให้ user ตอบ
- client ส่งคำตอบกลับ server

เหมาะสำหรับ:
- ขอ confirmation ก่อนทำ action ที่มีผลกระทบ
- ขอข้อมูลเพิ่มที่ server ต้องการ
- human-in-the-loop decisions

---

## Logging

ให้ server ส่ง log messages ไป client:

- ใช้สำหรับ debugging และ monitoring
- client ตัดสินใจว่าจะแสดงหรือเก็บ logs อย่างไร

---

## ความสัมพันธ์กับโน้ตอื่น

- [[02 AI Systems/MCP/Core/02 - Architecture_ Host, Client, Server|Architecture]] — client อยู่ตรงไหนใน architecture
- [[02 AI Systems/MCP/Core/03 - Core Primitives_ Tools, Resources, Prompts|Core Primitives]] — server-side primitives
- [[02 AI Systems/MCP/Security/05 - Security, Consent และ Authorization|Security]] — consent สำหรับ sampling และ elicitation
- [[02 AI Systems/MCP/MCP - MOC|MCP - MOC]]

---

## Official References

- MCP Sampling: https://modelcontextprotocol.io/docs/concepts/sampling
- MCP Elicitation: https://modelcontextprotocol.io/docs/concepts/elicitation
