---
tags:
  - mcp
  - sampling
  - roots
  - elicitation
  - clientfeatures
type: note
status: evergreen
source: "MCP/MCP_Knowledge_Base.md"
parent_note: "[[02 AI Systems/MCP/MCP - MOC|MCP - MOC]]"
---

# Client Features: Sampling, Roots, Elicitation



---

## Overview

Client features คือ capabilities ที่ **server เรียกใช้ผ่าน client** — host/client ยังเป็นผู้ควบคุม

---

## Sampling

เปิดทางให้ server ขอให้ client/host ไปเรียก LLM ให้แทนได้ โดย host ยังควบคุม model access และ permissions

**กรณีใช้:**
- Multi-step reasoning
- Recursive agent behavior
- Server ต้องการให้ host เป็นคนคุยกับ model โดยตรง

> นี่คือกลไกที่ทำให้ MCP server ทำ agentic behavior ได้โดยไม่ต้องถือ API key ของโมเดลเอง

---

## Roots

เปิดทางให้ client expose ขอบเขต filesystem หรือ workspace ที่ server ใช้งานได้

**กรณีใช้:**
- Coding assistant ที่ต้องรู้ว่าโปรเจกต์อยู่ที่ไหน
- Repo-aware tools
- Workspace-bounded automation

> Roots ช่วยจำกัด blast radius — server รู้เฉพาะ path ที่ host อนุญาต

---

## Elicitation

เปิดทางให้ server ขอข้อมูลเพิ่มเติมจาก user ผ่าน client

**2 โหมด:**
- **Form mode** — ขอ structured input จากผู้ใช้
- **URL mode** — ให้ผู้ใช้ไปทำ interaction ที่ sensitive นอก MCP client เช่น auth flow, OAuth

**กรณีใช้:**
- ขอข้อมูลที่ยังไม่พอสำหรับ task
- ขอ secrets/consent ผ่าน flow ที่ปลอดภัยกว่า
- Interactive workflow ที่ต้องการ human input

---

## Logging

Server ส่ง structured log messages กลับไปยัง client

**กรณีใช้:**
- Debugging ระหว่าง tool execution
- Observability และ monitoring
- Long-running workflow tracking

---

## ดูต่อ

- [[03 - Core Primitives: Tools, Resources, Prompts]] — ความสามารถฝั่ง server
- [[05 - Security, Consent และ Authorization]] — user consent สำหรับ sampling และ tools
- [[02 AI Systems/MCP/MCP - MOC|MCP - MOC]]
