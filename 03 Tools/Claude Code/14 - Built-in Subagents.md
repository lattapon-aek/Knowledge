---
tags:
  - claude-code
  - subagents
  - built-in
type: note
status: draft
created: "2026-04-09"
source: "https://code.claude.com/docs/en/sub-agents"
parent_note: "[[Claude Code - Multi-Agent MOC]]"
---

# Built-in Subagents ที่มีมาในตัว

Claude Code มี subagents ในตัวที่ Claude ใช้โดยอัตโนมัติ — **ไม่ต้องสร้างเอง**

| Agent | Model | Tools | เหมาะกับ |
|---|---|---|---|
| **Explore** | Haiku (เร็ว) | Read-only เท่านั้น | ค้นหาและวิเคราะห์ codebase โดยไม่แก้ไขอะไร |
| **Plan** | รับจาก main session | Read-only เท่านั้น | ใช้ใน plan mode เพื่อวิจัยโค้ดก่อนวางแผน |
| **general-purpose** | รับจาก main session | ทุก tool | งานซับซ้อนที่ต้องทั้ง explore และ implement |
| **statusline-setup** | Sonnet | — | เรียกอัตโนมัติเมื่อรัน `/statusline` |
| **Claude Code Guide** | Haiku | — | เรียกอัตโนมัติเมื่อถามเกี่ยวกับ feature ของ Claude Code |

---

## ข้อสำคัญ

> **Subagent ไม่สามารถ spawn subagent ซ้อนกันได้** — มีแค่ main agent เท่านั้นที่ spawn subagents ได้

---

## ดูเพิ่มเติม
- [[15 - สร้าง Subagent ด้วย agents]]
