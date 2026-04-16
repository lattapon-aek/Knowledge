---
tags:
  - engineering
  - mcp
  - moc
type: moc
status: evergreen
source: ""
parent_note: "[[06 Engineering/Engineering - MOC]]"
---

# MCP - MOC

implementation layer สำหรับ integrating MCP servers, client wiring, consent flow, และ tool exposure

---

## Notes Map

- [[06 Engineering/MCP/Recipe - Add MCP Server Integration|Add MCP Server Integration]]
- [[06 Engineering/MCP/Decision - Choose MCP Integration Boundary|Choose MCP Integration Boundary]]

---

## Related Hubs

- [[02 AI Systems/MCP/MCP - MOC|MCP - MOC]]
- [[02 AI Systems/AI Agent Fundamentals/14 - Tools: การออกแบบและทำงาน|AI Agent Fundamentals - Tools]]
- [[06 Engineering/README|Engineering - README]]

---

## Use This Layer When

- ต้อง wire MCP เข้า application/runtime จริง
- ต้องแยก server capabilities ออกจาก app logic
- ต้องคิดเรื่อง consent และ boundaries ใน implementation
