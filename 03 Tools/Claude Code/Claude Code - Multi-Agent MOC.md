---
tags:
  - claude-code
  - multi-agent
  - ai-tools
  - anthropic
  - MOC
type: moc
status: evergreen
created: "2026-04-09"
source: "https://code.claude.com/docs/en/overview"
parent_note: "[[Home]]"
---

# 🗺️ Claude Code — Multi-Agent (Map of Content)

> สร้าง AI Agents ที่ทำงานร่วมกันด้วย Claude Code | dohome Tech Team | ณ วันที่ 9 เมษายน 2568

---

## 📌 ภาพรวม

Claude Code คือ **CLI tool** จาก Anthropic สำหรับ Agentic Coding — ทำงานผ่าน Terminal โดยตรง อ่าน/เขียน/แก้ไขไฟล์จริง รันโค้ดได้ และรองรับ Multi-Agent

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
