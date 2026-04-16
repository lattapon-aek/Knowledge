---
tags:
  - engineering
  - mcp
  - decision
type: note
status: evergreen
source: "vault-local engineering"
parent_note: "[[06 Engineering/MCP/MCP - MOC]]"
---

# Decision - Choose MCP Integration Boundary

decision note สำหรับเลือกขอบเขตการเชื่อม MCP ระหว่าง app, client, และ server

---

## Context

- capability อยู่ฝั่งไหน
- logic ไหนควรอยู่ใน app
- logic ไหนควร expose เป็น server capability

## Options

- app-only integration
- client-side wrapper
- dedicated MCP server
- hybrid boundary

## Criteria

- reuse
- security
- operational complexity
- ownership

## Decision

บันทึก boundary ที่เลือก

## Consequences

- maintainability
- consent flow
- deployment complexity
