---
tags:
  - mcp
  - tools
  - resources
  - prompts
  - primitives
type: note
status: draft
source: "MCP/MCP_Knowledge_Base.md"
parent_note: "[[MCP - MOC]]"
---

# Core Primitives: Tools, Resources, Prompts



---

## Overview

Server features หลัก 3 อย่าง:

| Primitive | ใครคุม | ใช้ทำอะไร | Risk level |
|---|---|---|---|
| **Tools** | Model/host | Action, API call, computation | สูง (side effects) |
| **Resources** | Host/app | Read-only context | ต่ำ |
| **Prompts** | User | Workflow/template | — |

---

## Tools

ใช้สำหรับ action หรือ computation ที่ model เรียกได้

ตัวอย่างการใช้งาน:
- เรียก API
- query database
- สร้าง ticket
- trigger workflow
- คำนวณผลลัพธ์

**ลักษณะสำคัญ:**
- Model-controlled
- มีโอกาสเกิด **side effects**
- ควรมี user approval
- มี schema สำหรับ input/output

> เหมาะกับ: execute action, call external service, run automation

---

## Resources

ใช้สำหรับส่ง context/data แบบ **อ่านอย่างเดียว**

ตัวอย่างข้อมูล:
- file contents, docs, config
- database schema
- app-specific data

**ลักษณะสำคัญ:**
- Application-driven
- Read-only → lower risk กว่า tools
- ระบุด้วย URI

> เหมาะกับ: เติม context, ให้ model อ่านข้อมูล, host เลือก include resource เข้า prompt

---

## Prompts

ใช้สำหรับ template หรือ workflow ที่ server ส่งให้ host/client

ตัวอย่าง:
- code review prompt
- summarization workflow
- domain-specific assistant mode

**ลักษณะสำคัญ:**
- User-controlled
- มักถูก expose เป็นคำสั่งหรือ UI action
- รับ arguments ได้

> เหมาะกับ: standard workflow, reusable template, guided interaction

---

## ฟีเจอร์เสริมที่สำคัญในงานจริง

นอกจาก primitives หลัก MCP ยังมี:
- **Progress tracking** — สำหรับงานที่ใช้เวลานาน
- **Pagination** — สำหรับ list responses
- **Cancellation notifications** — ยกเลิก operation
- **Ping** — ตรวจ connection
- **Completion support** — ช่วย autocomplete argument values

> สำหรับ production-grade implementation ส่วนนี้สำคัญพอ ๆ กับ primitives หลัก

---

## Capability Matrix (ภาพรวม)

| Capability | ฝั่ง | ใครคุมหลัก | ใช้ทำอะไร |
|---|---|---|---|
| Tools | Server feature | Model/host | Action, API, computation |
| Resources | Server feature | Host/app | Read-only context |
| Prompts | Server feature | User | Workflow/template |
| Sampling | Client feature | Host/client | Server ขอให้ host เรียก LLM |
| Roots | Client feature | Host/client | เปิดขอบเขต filesystem |
| Elicitation | Client feature | Host/client | ขอข้อมูลเพิ่มจากผู้ใช้ |
| Logging | Server/Client | Server/client | Structured log messages |
| Tasks | Client/Server | ทั้งสองฝั่ง | Task-augmented interactions |

---

## ดูต่อ

- [[04 - Client Features: Sampling, Roots, Elicitation]] — ความสามารถฝั่ง client
- [[05 - Security, Consent และ Authorization]] — หลักการ security สำหรับ tools
- [[MCP - MOC]]
