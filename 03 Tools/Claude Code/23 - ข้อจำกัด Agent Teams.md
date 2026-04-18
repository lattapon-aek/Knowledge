---
tags:
  - claude-code
  - agent-teams
  - limitations
  - experimental
type: note
status: evergreen
created: "2026-04-09"
source: "https://code.claude.com/docs/en/agent-teams"
parent_note: "[[Claude Code - Multi-Agent MOC]]"
---

# ข้อจำกัดของ Agent Teams

> ⚠️ Agent Teams ยังอยู่ในสถานะ **Experimental** — ใช้อย่างระมัดระวัง
> ℹ️ ต้องใช้ Claude Code **v2.1.32 ขึ้นไป** — ตรวจสอบด้วย `claude --version`

---

## ข้อจำกัดที่ official ระบุ

| ข้อจำกัด | รายละเอียด | วิธีรับมือ |
|---|---|---|
| **ไม่รองรับ `/resume` และ `/rewind` กับ in-process teammates** | หลัง resume/rewind Lead อาจส่งข้อความหา Teammate ที่ไม่มีแล้ว | Spawn Teammate ใหม่หลัง resume |
| **1 team ต่อ 1 session** | Lead manage ได้แค่ 1 team ต่อครั้ง | Clean up team เก่าก่อนสร้างใหม่ |
| **ไม่มี nested teams** | Teammate ไม่สามารถ spawn team หรือ Teammate เพิ่มได้ | Lead เท่านั้นที่ manage team ได้ |
| **Split pane ต้องพึ่ง tmux หรือ iTerm2** | ต้องตั้งค่า tmux หรือ iTerm2 + it2 CLI ก่อนใช้ split pane | ใช้ in-process mode แทน |
| **ต้นทุนสูง** | Agent Teams ใช้ token มากกว่าสession เดียว | จำกัดจำนวน teammate ให้พอดีกับงาน |

---

## ข้อจำกัดของ Subagents (Agent Tool)

- **รายงานกลับ main เท่านั้น** — Subagent คุยกับ Subagent อื่นโดยตรงไม่ได้
- **ไม่มี mailbox** — ต่างจาก Agent Teams ที่ Teammate คุยกันเองได้
- **สามารถทำงาน parallel หรือ sequential ได้** แต่การประสานยังผ่าน main conversation

---

## ข้อจำกัดทั่วไปของ Multi-Agent

- **Experimental = อาจเปลี่ยนแปลงได้** — behavior ยังไม่ stable 100%
- **การกำหนด scope และ permissions สำคัญมาก** — ถ้าไม่ชัดจะเกิด conflict หรือ permission friction ได้ง่าย

---

## ดูเพิ่มเติม
- [[19 - วิธีเริ่ม Agent Team]]
- [[22 - Error Handling]]
- [[06 - การควบคุมต้นทุน]]

## พื้นฐานทฤษฎีที่เกี่ยวข้อง

- [[05 Use Cases/Use Cases - When to Use an Agent|When to Use an Agent]] — Latency / Cost / Complexity tradeoffs ในทฤษฎี ตรงกับข้อจำกัดจริงของ Agent Teams
- [[02 AI Systems/AI Agent Fundamentals/Reference/10 - Risks และ Best Practices|Scalability Challenges]] — Context window limit, Hallucination, Oversight issues ที่พบใน production
