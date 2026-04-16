---
tags:
  - engineering
  - guardrails
  - moc
type: moc
status: evergreen
source: ""
parent_note: "[[06 Engineering/Engineering - MOC]]"
---

# Guardrails - MOC

implementation layer สำหรับ validation, review gates, fallback behavior, tool safety, และ policy enforcement

---

## Notes Map

- [[06 Engineering/Guardrails/Recipe - Add Output Validation|Add Output Validation]]
- [[06 Engineering/Guardrails/Decision - Choose a Validation Boundary|Choose a Validation Boundary]]

---

## Related Hubs

- [[02 AI Systems/Guardrails/Guardrails - MOC|Guardrails - MOC]]
- [[02 AI Systems/MCP/MCP - MOC|MCP - MOC]]
- [[03 Tools/Claude Code/22 - Error Handling|Claude Code Error Handling]]
- [[06 Engineering/README|Engineering - README]]

---

## Use This Layer When

- ต้องเอา policy ไปบังคับใน runtime
- ต้อง validate output ก่อนใช้งานต่อ
- ต้องตั้ง human review gate
- ต้องเชื่อม fallback กับ failure handling
