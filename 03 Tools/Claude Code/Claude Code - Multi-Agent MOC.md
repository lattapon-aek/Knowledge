---
tags:
  - claude-code
  - multi-agent
  - ai-tools
  - anthropic
  - moc
type: moc
status: evergreen
created: "2026-04-09"
source: "https://code.claude.com/docs/en/overview · https://code.claude.com/docs/en/agent-teams · https://code.claude.com/docs/en/sub-agents"
parent_note: "[[Home]]"
---

# Claude Code - Multi-Agent MOC

---

## 📌 ภาพรวม

Claude Code คือ **CLI tool** จาก Anthropic สำหรับ agentic coding และ multi-agent workflows ตามเอกสารทางการของ Claude Code

---

## 🗂️ Notes ในชุดนี้

### พื้นฐาน
- [[01 - Claude Code คืออะไร]]
- [[02 - เปรียบเทียบ Agentic Coding Tools]]
- [[03 - Orchestrator Pattern]]

### สถาปัตยกรรม Agent
- [[04 - 1 Session vs Subagents vs Agent Teams]]
- [[05 - รูปแบบการใช้งาน Multi-Agent]]
- [[06 - การควบคุมต้นทุน]]

### การติดตั้งและตั้งค่า
- [[07 - การติดตั้งและเริ่มใช้งาน]]
- [[08 - Display Mode (In-Process vs Split Panes)]]
- [[09 - Permissions และ Settings]]
- [[10 - Session Management และ Commands]]

### การสร้าง Agent
- [[11 - โครงสร้างโฟลเดอร์ .claude]]
- [[12 - CLAUDE File|CLAUDE.md]]
- [[13 - Custom Commands]]
- [[14 - Built-in Subagents]]
- [[15 - สร้าง Subagent ด้วย agents]]
- [[16 - บทบาท Frontend, Backend, QA]]

### ลงมือทำ
- [[17 - Agent Tool]]
- [[18 - Git Worktree]]
- [[19 - วิธีเริ่ม Agent Team]]
- [[20 - Multi-Provider AI]]
- [[21 - กรณีศึกษา]]
- [[22 - Error Handling]]
- [[23 - ข้อจำกัด Agent Teams|ข้อจำกัด]]

### Quick Reference
- [[24 - Best Practices & Checklist]]

---

## Related Hubs

- [[04 Synthesis/Synthesis - MOC|Synthesis - MOC]]
- [[05 Use Cases/Use Cases - MOC|Use Cases - MOC]]
- [[02 AI Systems/AI Agent Fundamentals/AI Agent Fundamentals - MOC|AI Agent Fundamentals - MOC]]
- [[02 AI Systems/Agent Frameworks/Agent Frameworks - MOC|Agent Frameworks - MOC]]
- [[02 AI Systems/Guardrails/Guardrails - MOC|Guardrails - MOC]]
- [[02 AI Systems/Evals/Evals - MOC|Evals - MOC]]
- [[06 Engineering/Engineering - MOC|Engineering - MOC]]
- [[Knowledge Topic Registry]]

---

## Stable Concepts

หมวดนี้ควรอ่านเป็นแนวคิดและ workflow ที่ค่อนข้างนิ่ง

- [[01 - Claude Code คืออะไร]]
- [[02 - เปรียบเทียบ Agentic Coding Tools]]
- [[03 - Orchestrator Pattern]]
- [[05 - รูปแบบการใช้งาน Multi-Agent]]
- [[06 - การควบคุมต้นทุน]]
- [[16 - บทบาท Frontend, Backend, QA]]
- [[21 - กรณีศึกษา]]
- [[20 - Multi-Provider AI]]
 
ถ้าต้องการอ่านกรอบคิดเรื่อง agent / workflow / decision ก่อน ให้ไป `AI Agent Fundamentals`
ถ้าต้องการอ่าน decision path ว่าควรใช้ agent เมื่อไรหรือควรขยายเป็น multi-agent เมื่อไร ให้ไป `05 Use Cases`
ถ้า topic เป็นเรื่อง Claude Code ที่ทับกับ core concepts ให้เลือก canonical home ของ topic นั้นก่อน แล้วค่อยใช้หมวดนี้เป็น volatile tool reference

---

## Version Sensitive Notes

หมายเหตุ: กลุ่มนี้ผูกกับ release, settings, terminal mode, หรือ behavior ที่เปลี่ยนได้

- [[04 - 1 Session vs Subagents vs Agent Teams]]
- [[07 - การติดตั้งและเริ่มใช้งาน]]
- [[08 - Display Mode (In-Process vs Split Panes)]]
- [[09 - Permissions และ Settings]]
- [[10 - Session Management และ Commands]]
- [[11 - โครงสร้างโฟลเดอร์ .claude]]
- [[12 - CLAUDE File|CLAUDE.md]]
- [[13 - Custom Commands]]
- [[14 - Built-in Subagents]]
- [[15 - สร้าง Subagent ด้วย agents]]
- [[17 - Agent Tool]]
- [[18 - Git Worktree]]
- [[19 - วิธีเริ่ม Agent Team]]
- [[20 - Multi-Provider AI]]
- [[22 - Error Handling]]
- [[23 - ข้อจำกัด Agent Teams|ข้อจำกัด]]
- [[24 - Best Practices & Checklist]]

### Boundary Reminder

- ถ้าเป็น concept หลักเรื่อง agent, prompt, context, memory, RAG, guardrails, evals ให้ไป canonical topic ที่ registry ระบุไว้ก่อน
- ถ้าเป็น implementation-level recipe ให้ไป `06 Engineering`
- ถ้าเป็น decision path ว่าควรใช้เครื่องมือ / workflow แบบไหน ให้ไป `05 Use Cases`

---

## ⚡ Quick Decision

```
worker ต้องคุยกันไหม?
├── ใช่ → Agent Teams (parallel, แต่ token สูง)
└── ไม่ → Subagents (sequential, context สะอาด, ถูกกว่า)

งานง่าย ไฟล์น้อย → 1 Session
งานมี workflow A→B→C → Subagents
งานใหญ่ หลาย domain พร้อมกัน → Agent Teams
```

---

## 🔗 Official Docs
[code.claude.com](https://code.claude.com/docs/en/overview)
