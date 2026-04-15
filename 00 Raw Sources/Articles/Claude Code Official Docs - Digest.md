---
tags:
  - rawsources
  - digest
  - claudecode
  - officialdocs
type: reference
status: draft
source: "https://code.claude.com/docs/en/overview"
parent_note: "[[Claude Code Official Docs - Manifest]]"
---

# Claude Code Official Docs - Digest

## Scope

digest นี้สรุปกลุ่มเอกสาร Claude Code ที่เกี่ยวกับ:
- overview
- agent teams
- sub-agents
- memory
- settings
- skills
- CLI

---

## Key Points

- Claude Code วางตัวเป็น agentic coding environment ที่รวม chat, tools, filesystem, และ orchestration workflows
- docs ฝั่ง `agent-teams` และ `sub-agents` ชี้ไปที่รูปแบบ multi-agent orchestration โดยใช้หลาย sessions หรือ specialized agents
- docs ฝั่ง `memory`, `settings`, และ `cli-reference` เน้น operational control และ reproducible workflows

---

## Operational Implications

- หมวด `03 Tools/Claude Code` ของ vault นี้พึ่ง docs family นี้โดยตรง
- ถ้าจะ ingest เพิ่มในอนาคต ควรเน้น:
  - orchestration
  - sub-agent boundaries
  - CLI workflows
  - permissions / settings

---

## Related Notes

- [[00 Raw Sources/Articles/Claude Code Official Docs - Manifest]]
- [[03 Tools/Claude Code/Claude Code - Multi-Agent MOC]]
- [[03 Tools/Claude Code/03 - Orchestrator Pattern]]
- [[03 Tools/Claude Code/04 - 1 Session vs Subagents vs Agent Teams]]
- [[03 Tools/Claude Code/10 - Session Management และ Commands]]
- [[03 Tools/Claude Code/24 - Best Practices & Checklist]]

---

## Official References

- Overview: https://code.claude.com/docs/en/overview
- Agent Teams: https://code.claude.com/docs/en/agent-teams
- Sub-agents: https://code.claude.com/docs/en/sub-agents
