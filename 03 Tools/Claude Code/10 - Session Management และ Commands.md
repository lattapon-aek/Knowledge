---
tags:
  - claude-code
  - commands
  - session
  - reference
type: note
status: draft
created: "2026-04-09"
source: "https://code.claude.com/docs/en/cli-reference"
parent_note: "[[Claude Code - Multi-Agent MOC]]"
---

# Session Management และ Built-in Commands

---

## จัดการ Session

| คำสั่ง | ความหมาย |
|---|---|
| `/compact` | บีบอัด context (ใช้เมื่อ session ยาวนาน) |
| `claude -r` / `--resume` | ต่อ session เดิม |
| `claude -c` / `--continue` | ต่อจาก message ล่าสุด |
| `Esc` | หยุด agent กลางคัน (ปลอดภัย) |

> **แนวทางที่ดี:** ใช้ `/compact` ทุก 30-40 นาที หรือเมื่อ context เกิน 50%

---

## Built-in Commands สำคัญ

| คำสั่ง | ใช้ทำอะไร |
|---|---|
| `/agents` | **สร้าง/แก้ไข/ลบ/ดู Subagent** (หัวใจของ Multi-Agent) |
| `/init` | สร้าง CLAUDE.md อัตโนมัติจากการสแกนโปรเจกต์ |
| `/memory` | แก้ไข memory system ทั้งหมด (CLAUDE.md + auto memory files) |
| `/permissions` | จัดการ allow/deny tools แบบ interactive |
| `/context` | ดูการใช้ context window ปัจจุบัน (visual grid) |
| `/cost` | ดูต้นทุน token ที่ใช้ไปใน session นี้ |
| `/compact` | บีบอัด context เมื่อ session ยาว |
| `/config` | เปิด Settings interface เพื่อแก้ไขการตั้งค่า |
