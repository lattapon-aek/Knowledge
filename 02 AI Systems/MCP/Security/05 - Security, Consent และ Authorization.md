---
tags:
  - mcp
  - security
  - consent
  - authorization
  - safety
type: note
status: evergreen
source: "MCP/MCP_Knowledge_Base.md"
parent_note: "[[02 AI Systems/MCP/MCP - MOC|MCP - MOC]]"
---

# Security, Consent และ Authorization



---

## ทำไม Security จึงสำคัญใน MCP

MCP เปิดทางไปถึง data access และ code execution ได้โดยตรง ดังนั้น trust & safety จึงเป็นส่วนที่ protocol ให้ความสำคัญอย่างมาก

---

## หลักการสำคัญ

- ผู้ใช้ต้องมี **explicit consent** ต่อ data access และ tool execution
- **Host ต้องคุม** ว่าจะ expose data อะไรให้ server
- Tool metadata และ description ไม่ควรถูกเชื่อแบบไม่มีเงื่อนไข — treat as **untrusted input** ถ้า server ไม่น่าเชื่อถือ
- Sampling ต้องอยู่ภายใต้ **user approval** และ host control

---

## Authorization

Official spec ระบุ authorization สำหรับ HTTP-based transports:
- Authorization อยู่ระดับ transport
- เหมาะกับ restricted remote MCP servers
- ต้องออกแบบ token handling, scope, redirect flow, communication security ให้ดี
- Local stdio server หลายกรณีไม่ต้องมี OAuth-style flow

---

## Security Checklist

- ขอ **consent ก่อนเรียก tools** ที่มี side effects
- จำกัด scope ของ tool ให้แคบที่สุด
- ใช้ **Roots** เพื่อจำกัด filesystem boundary
- แยก secrets ออกจาก prompt/resource เมื่อทำได้
- Log เฉพาะเท่าที่จำเป็น
- Validate input schema ทุกครั้ง
- Treat server descriptions และ annotations เป็น **untrusted input** ถ้า server ไม่น่าเชื่อถือ

---

## ความเสี่ยงที่พบบ่อย

- Prompt injection ผ่าน tool output หรือ resource content
- Tool ที่มี side effects โดยไม่มี user confirmation
- Server ที่ expose capabilities เกินขอบเขตที่ควร
- Secrets ที่รั่วผ่าน logging หรือ error messages

---

## ดูต่อ

- [[03 - Core Primitives_ Tools, Resources, Prompts]] — ความเสี่ยงของ tools
- [[04 - Client Features_ Sampling, Roots, Elicitation]] — Roots สำหรับจำกัดขอบเขต filesystem
- [[02 AI Systems/MCP/MCP - MOC|MCP - MOC]]
