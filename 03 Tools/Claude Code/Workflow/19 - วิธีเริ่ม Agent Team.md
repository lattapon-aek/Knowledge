---
tags:
  - claude-code
  - agent-teams
  - how-to
  - experimental
  - version-sensitive
type: note
status: evergreen
created: "2026-04-09"
source: "https://code.claude.com/docs/en/agent-teams"
parent_note: "[[Claude Code - Multi-Agent MOC]]"
---

# วิธีเริ่ม Agent Team

Agent Team ไม่มี command พิเศษ — แค่ **บอก Claude เป็นภาษาธรรมดา**

---

## ตัวอย่าง Prompts

```text
# Code Review แบบ parallel
Create an agent team to review PR #142.
Spawn three reviewers:
- One focused on security
- One checking performance
- One validating test coverage

# Debug แบบแข่งสมมติฐาน
สร้าง agent team มา 3 ตัว แต่ละตัวสืบสวน bug จากคนละสมมติฐาน
ให้คุยกันเองแล้วหา root cause ที่ชนะ

# Parallel refactor
Create a team with 3 teammates to refactor these modules in parallel.
Use Sonnet for each teammate.
```

---

## Keyboard Shortcuts (In-Process Mode)

| Shortcut | ทำอะไร |
|---|---|
| `Shift+Down` | สลับไปยัง Teammate ถัดไป (วนกลับมา Lead) |
| `Enter` | เปิด session ของ teammate ที่เลือก |
| `Ctrl+T` | toggle task list |
| `Esc` | interrupt turn ที่กำลังรันอยู่ |

---

## เปรียบเทียบ: ทำเองทุกอย่าง vs Agent Teams

| | แบบเดิม | Agent Teams |
|---|---|---|
| การเริ่มต้น | เปิด terminal หลายอันเอง | บอก Claude เป็นประโยคเดียว |
| การส่งข้อมูล | copy-paste ระหว่างหน้าต่าง | Teammate คุยกันเอง ผ่าน mailbox |
| การติดตาม | ติดตามสถานะเอง | shared task list อัพเดต realtime |
| **ผลลัพธ์** | ใช้เวลานาน | **ทำงาน parallel ได้พร้อมกัน** |

---

## ดูเพิ่มเติม
- [[08 - Display Mode (In-Process vs Split Panes)]]
- [[09 - Permissions และ Settings]]
- [[23 - ข้อจำกัด Agent Teams]]
- [[05 Use Cases/Decision/Use Cases - Move from Single to Multi-Agent]]
