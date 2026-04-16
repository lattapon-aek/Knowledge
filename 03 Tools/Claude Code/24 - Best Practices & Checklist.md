---
tags:
  - claude-code
  - best-practices
  - checklist
  - quick-start
type: note
status: evergreen
created: "2026-04-09"
source: "https://code.claude.com/docs/en/agent-teams · https://code.claude.com/docs/en/hooks-guide"
parent_note: "[[Claude Code - Multi-Agent MOC]]"
---

# Best Practices & Checklist

---

## ✅ สิ่งที่ควรทำ

- **ใช้ CLAUDE.md** — เขียนบริบทโปรเจกต์ กฎ naming convention และสิ่งที่ห้ามทำไว้ที่นี่ ตาม docs ไฟล์นี้ถูกโหลดเข้าสู่ context ตอนเริ่ม session
- **กำหนด scope ชัดเจนให้แต่ละ agent** — ระบุโฟลเดอร์ที่รับผิดชอบและห้ามแตะ
- **บอก fallback ใน prompt** — "ถ้าเจอ error ให้ข้ามและบันทึกไว้"
- **เติม context ล่าสุดตอนเริ่ม session** — ใช้ `SessionStart` hook กับ `compact` matcher เพื่อ inject สิ่งที่เพิ่งเกิดขึ้น เช่น `git log --oneline -5`
- **จำกัดจำนวน Teammates** — ใช้เท่าที่งานต้องการจริง ๆ
- **เลือก model ให้เหมาะกับงาน** — Claude Code รองรับ `sonnet`, `opus`, และ `haiku` aliases
- **ตรวจสอบผลลัพธ์จริงเสมอ** — อย่าเชื่อแค่คำว่า "เสร็จแล้ว"
- **ใช้ git worktree** — เมื่อหลาย agent แก้ไฟล์ในโปรเจกต์เดียวกัน
- **เปิด Agent Teams ผ่าน config** — ต้องตั้งค่า `CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS=1` ก่อนใช้
- **ระบุ retry limit** — "ลองใหม่ได้สูงสุด 2 รอบ" เพื่อป้องกัน infinite loop

---

## ❌ สิ่งที่ควรหลีกเลี่ยง

- **อย่าใส่งานเยอะเกินไปใน session เดียว** — ถ้าต้องการแยก context ให้ใช้ Subagent หรือ Agent Teams
- **อย่าใช้ Agent Teams กับงานที่ไม่จำเป็น** — overhead สูง ใช้เฉพาะงาน complex จริงๆ
- **อย่าปล่อยให้ agent เข้าถึง irreversible commands** — ใส่ `deny` ใน permissions เช่น `rm -rf`, `git push --force`
- **อย่า hardcode API key ใน CLAUDE.md** — ใช้ environment variable แทน
- **อย่า nest teams** — Teammate ไม่สามารถ spawn team อื่นได้ (ทำได้แค่ Lead)
- **อย่าพึ่ง `/resume` กับ in-process teammates** — ไม่ stable ตาม official docs

---

## ตัวอย่าง Quick Start

1. ตั้งค่า `CLAUDE.md` ให้มีบริบทโปรเจกต์ที่จำเป็น
2. ถ้าจะใช้ Agent Teams ให้เปิด `CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS=1`
3. สร้าง subagent หรือ teammate จากงานที่แยกขอบเขตได้ชัด
4. ทดสอบกับงานเล็กก่อน แล้วค่อยขยายไปงานจริง

**ผล: ได้โครงเริ่มต้นที่ใช้งานต่อได้**

---

## Checklist ก่อน Deploy Multi-Agent System

- [ ] CLAUDE.md มีบริบทโปรเจกต์ครบ
- [ ] แต่ละ agent มีขอบเขตความรับผิดชอบชัดเจน (ระบุโฟลเดอร์)
- [ ] `permissions.deny` ครอบคลุม irreversible actions
- [ ] ทดสอบ agent แยกก่อนรวม team
- [ ] ตั้ง model ให้เหมาะกับงาน (Haiku/Sonnet/Opus)
- [ ] มีการ review ผลลัพธ์จากคนจริงก่อน merge
- [ ] เปิดใช้ git worktree ถ้ามีหลาย agent แก้ไฟล์เดียวกัน
- [ ] รู้วิธีหยุด agent ฉุกเฉินด้วย `Esc`

---

## ดูเพิ่มเติม
- [[01 - Claude Code คืออะไร]]
- [[09 - Permissions และ Settings]]
- [[12 - CLAUDE File|CLAUDE.md]]
- [[23 - ข้อจำกัด Agent Teams]]

## พื้นฐานทฤษฎีที่เกี่ยวข้อง

- [[02 AI Systems/AI Agent Fundamentals/10 - Risks และ Best Practices|Best Practices ทฤษฎี]] — Privacy-by-Design, Guardrails, Monitoring, Incident Response ในทฤษฎี ตรงกับ checklist นี้
- [[02 AI Systems/AI Agent Fundamentals/09 - เมื่อไรควรและไม่ควรใช้ Agent|Decision Framework]] — เกณฑ์ตัดสินใจว่าเมื่อไรควรใช้ Agent ระดับใด ก่อนใช้ checklist นี้
- [[02 AI Systems/Guardrails/Guardrails - MOC|Guardrails - MOC]] — รวมข้อจำกัด, validation, fallback, permissions, และ monitoring ที่เกี่ยวกับ production agents
- [[02 AI Systems/Evals/Evals - MOC|Evals - MOC]] — ใช้ตรวจว่าระบบ multi-agent ใช้งานได้จริงและไม่ regress เมื่อปรับ prompt หรือ model
