---
tags:
  - claude-code
  - agent-teams
  - limitations
  - experimental
type: note
status: draft
created: "2026-04-09"
source: "https://code.claude.com/docs/en/agent-teams"
parent_note: "[[Claude Code - Multi-Agent MOC]]"
---

# ข้อจำกัดของ Agent Teams

> ⚠️ Agent Teams ยังอยู่ในสถานะ **Experimental** — ใช้อย่างระมัดระวัง
> ℹ️ ต้องใช้ Claude Code **v2.1.32 ขึ้นไป** — ตรวจสอบด้วย `claude --version`

---

## ข้อจำกัดที่ทราบจาก Official Docs

| ข้อจำกัด | รายละเอียด | วิธีรับมือ |
|---|---|---|
| **ไม่รองรับ `/resume` และ `/rewind`** | หลัง resume/rewind Lead อาจส่งข้อความหา Teammate ที่ไม่มีแล้ว | Spawn Teammate ใหม่หลัง resume |
| **Task status lag** | Teammate บางครั้งไม่ mark task ว่าเสร็จ ทำให้ task ถัดไป block | ตรวจสอบและอัพเดต task status ด้วยตนเอง |
| **Shutdown ช้า** | Teammate ต้องรอ request/tool call ปัจจุบันเสร็จก่อน | รอหรือ interrupt ด้วย `Esc` |
| **1 team ต่อ 1 session** | Lead manage ได้แค่ 1 team ต่อครั้ง | Clean up team เก่าก่อนสร้างใหม่ |
| **ไม่มี nested teams** | Teammate ไม่สามารถ spawn team หรือ Teammate เพิ่มได้ | Lead เท่านั้นที่ manage team ได้ |
| **Lead เปลี่ยนไม่ได้** | session ที่สร้าง team คือ Lead ตลอดชีพ ย้าย/เลื่อนตำแหน่ง Teammate เป็น Lead ไม่ได้ | วางแผน Lead ให้ถูกตั้งแต่ต้น |
| **Permission ตั้งตอน spawn** | Teammate เริ่มต้นด้วย permission ของ Lead เสมอ แก้รายตัวได้ภายหลัง แต่ตั้งล่วงหน้าตอน spawn ไม่ได้ | เซ็ต permission ของ Lead ให้ถูกก่อน spawn |
| **Split pane ใช้ได้แค่บาง terminal** | ไม่รองรับ VS Code terminal, Windows Terminal, Ghostty | ใช้ in-process mode แทน |
| **ต้นทุนสูง** | แต่ละ Teammate = Claude instance แยก = token แยก | ใช้ 3-5 Teammates เท่าที่จำเป็น, ใช้ Haiku ที่ทำได้ |
| **Hallucination** | Claude อาจคิดเองว่าทำเสร็จแล้ว | ตรวจสอบผลลัพธ์จริงเสมอ |
| **Irreversible Actions** | คำสั่งลบ/deploy ไม่มีการย้อนกลับ | ใส่ใน `deny` list ใน permissions |

---

## ข้อจำกัดของ Subagents (Agent Tool)

- **ทำงาน sequential** — ไม่ parallel (ต่างจาก Agent Teams)
- **รายงานกลับ main เท่านั้น** — Subagent คุยกับ Subagent อื่นโดยตรงไม่ได้
- **ไม่มี mailbox** — ต่างจาก Agent Teams ที่ Teammate คุยกันเองได้

---

## ข้อจำกัดทั่วไปของ Multi-Agent

- **Context window ของแต่ละ agent มีจำกัด** — 200K tokens (Claude Sonnet)
- **ไม่มี cross-provider agent communication** — Claude คุยกับ GPT-4 หรือ Gemini โดยตรงไม่ได้
- **Experimental = อาจเปลี่ยนแปลงได้** — behavior ยังไม่ stable 100%

---

## ดูเพิ่มเติม
- [[19 - วิธีเริ่ม Agent Team]]
- [[22 - Error Handling]]
- [[06 - การควบคุมต้นทุน]]

## พื้นฐานทฤษฎีที่เกี่ยวข้อง

- [[02 AI Systems/AI Agent Fundamentals/09 - เมื่อไรควรและไม่ควรใช้ Agent|Tradeoffs ของการใช้ Agent]] — Latency / Cost / Complexity tradeoffs ในทฤษฎี ตรงกับข้อจำกัดจริงของ Agent Teams
- [[02 AI Systems/AI Agent Fundamentals/10 - Risks และ Best Practices|Scalability Challenges]] — Context window limit, Hallucination, Oversight issues ที่พบใน production
