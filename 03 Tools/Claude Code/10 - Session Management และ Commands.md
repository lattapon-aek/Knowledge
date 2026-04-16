---
tags:
  - claude-code
  - commands
  - session
  - reference
type: note
status: draft
created: "2026-04-09"
source: "https://code.claude.com/docs/en/cli-reference · https://code.claude.com/docs/en/hooks-guide"
parent_note: "[[Claude Code - Multi-Agent MOC]]"
---

# Session Management และ Built-in Commands

---

## จัดการ Session

| คำสั่ง | ความหมาย |
|---|---|
| `/compact` | บีบอัด context |
| `claude -r` / `--resume` | ต่อ session เดิม |
| `claude -c` / `--continue` | ต่อจาก message ล่าสุด |
| `Esc` | หยุด agent กลางคัน (ปลอดภัย) |

> **แนวทางที่ดี:** ใช้ `/compact` เมื่อ session เริ่มยาวและต้องการลด context

---

## ใส่ Context ล่าสุดตอนเริ่ม Session

ถ้าต้องการให้ Claude เห็น "งานล่าสุด" ตั้งแต่เริ่ม session สามารถใช้ `SessionStart` hook กับ `compact` matcher เพื่อ inject context กลับเข้าไปหลังการ compact ได้

ตัวอย่างที่ official docs ยกมา คือเรียกคำสั่งที่คืน output ล่าสุดจาก git เช่น:

```bash
git log --oneline -5
```

> จุดสำคัญ: นี่ไม่ใช่ `/compact` เอง แต่เป็น hook ที่ช่วยเติม context หลัง compaction หรือเมื่อ session เริ่มใหม่

---

## Built-in Commands สำคัญ

| คำสั่ง | ใช้ทำอะไร |
|---|---|
| `/agents` | เปิด interface สำหรับจัดการ subagents |
| `/init` | สร้าง CLAUDE.md อัตโนมัติจากการสแกนโปรเจกต์ |
| `/memory` | จัดการ memory files และ rules ที่ session โหลด |
| `/permissions` | จัดการ allow/deny tools แบบ interactive |
| `/context` | ดูการใช้ context window ปัจจุบัน (visual grid) |
| `/cost` | ดูต้นทุน token ที่ใช้ไปใน session นี้ |
| `/compact` | บีบอัด context เมื่อ session ยาว |
| `/config` | เปิด Settings interface เพื่อแก้ไขการตั้งค่า |
