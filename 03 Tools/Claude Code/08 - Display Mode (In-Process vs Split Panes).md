---
tags:
  - claude-code
  - agent-teams
  - terminal
  - tmux
  - iterm2
type: note
status: draft
created: "2026-04-09"
source: "https://code.claude.com/docs/en/agent-teams"
parent_note: "[[Claude Code - Multi-Agent MOC]]"
---

# Display Mode ของ Agent Teams

Agent Teams รองรับ **2 display mode**

---

## Mode 1: In-Process (default)

ทุก Teammate รันใน terminal เดียวกัน — ไม่ต้องติดตั้งอะไรเพิ่ม

| Shortcut | ทำอะไร |
|---|---|
| `Shift+Down` | สลับไปยัง Teammate ถัดไป (วนกลับมา Lead) |
| `Enter` | เข้าดู session ของ Teammate |
| `Esc` | interrupt turn ที่กำลังรัน |
| `Ctrl+T` | toggle task list |

> ✅ ทำงานได้ทุก terminal

---

## Mode 2: Split Panes

แต่ละ Teammate ได้ pane ของตัวเอง — เห็นทุกคนพร้อมกัน

```
┌─────────────────┬─────────────────┐
│   Team Lead     │ security-agent  │
├─────────────────┼─────────────────┤
│ frontend-agent  │   qa-agent      │
└─────────────────┴─────────────────┘
```

ต้องการ **อย่างใดอย่างหนึ่ง**:

| ตัวเลือก | เหมาะกับ | วิธีติดตั้ง |
|---|---|---|
| **tmux** | Server, SSH, Linux, macOS | `brew install tmux` |
| **iTerm2 + `it2` CLI** | macOS เครื่องตัวเอง | ติดตั้ง `it2` CLI + เปิด Python API ใน iTerm2 Settings → General → Magic |

> ❌ **ไม่รองรับ** Split Pane: VS Code terminal, Windows Terminal, Ghostty

---

## ตั้งค่า Display Mode

ใน `~/.claude.json` (global config):

```json
{
  "teammateMode": "auto"
}
```

| ค่า | ผล |
|---|---|
| `"auto"` | split panes ถ้าอยู่ใน tmux, in-process ถ้าไม่ (default) |
| `"in-process"` | รันใน terminal เดียว |
| `"tmux"` | แยก pane อัตโนมัติ |

หรือใช้ flag ชั่วคราว: `claude --teammate-mode in-process`

---

## tmux คำสั่งพื้นฐาน

```bash
tmux new -s agents        # สร้าง session
Ctrl+B แล้ว %             # แบ่งแนวตั้ง
Ctrl+B แล้ว "             # แบ่งแนวนอน
Ctrl+B แล้ว D             # detach (session ยังทำงานต่อ)
tmux attach -t agents     # กลับเข้า session
tmux ls                   # ดู sessions ทั้งหมด
```

> **จุดแข็ง tmux:** session ยังทำงานอยู่แม้ SSH หลุด

---

## เลือกอะไรดี?

### เปรียบเทียบ tmux vs iTerm2

| | **tmux** | **iTerm2 + it2 CLI** |
|---|---|---|
| **OS** | macOS, Linux, WSL, Server | macOS เท่านั้น |
| **SSH / Remote** | ✅ ทำงานได้ session ไม่หลุดแม้ connection ตัด | ❌ เป็น GUI app — ติดตั้งได้เฉพาะ Mac ตัวเอง ใช้บน remote server ไม่ได้ |
| **ติดตั้ง** | `brew install tmux` | ติดตั้ง iTerm2 + `it2` CLI + เปิด Python API |
| **Visual** | pane แบบ terminal ดิบ | GUI สวยงาม มีสี scroll ง่าย |
| **Keyboard** | ต้องจำ shortcut (`Ctrl+B`) | คลิกเข้า pane ได้เลย |
| **Stability** | สูง — battle-tested | ขึ้นกับ iTerm2 version |
| **ข้อจำกัด official** | known limitations บาง OS | ต้องเปิด Python API ก่อนใช้ |

### คำแนะนำตามสถานการณ์

```
ไม่อยากติดตั้งอะไรเพิ่ม      → In-Process (default) — ใช้ได้ทุก terminal
ทำงานบน Server / SSH          → tmux — session อยู่แม้ connection หลุด
macOS + ต้องการ GUI สวย       → iTerm2 + it2 CLI
macOS + ต้องการ best of both  → tmux -CC ใน iTerm2 (official recommend)
Linux / WSL                   → tmux เท่านั้น
```

> ℹ️ Official docs แนะนำ `tmux -CC` ใน iTerm2 เป็น "suggested entrypoint" สำหรับผู้ใช้ macOS ที่ต้องการ split panes
