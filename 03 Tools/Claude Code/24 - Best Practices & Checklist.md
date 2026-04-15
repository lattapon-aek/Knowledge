---
tags:
  - claude-code
  - best-practices
  - checklist
  - quick-start
type: note
status: evergreen
created: "2026-04-09"
source: "https://code.claude.com/docs/en/agent-teams"
parent_note: "[[Claude Code - Multi-Agent MOC]]"
---

# Best Practices & Checklist

---

## ✅ สิ่งที่ควรทำ

- **ใช้ CLAUDE.md** — เขียนบริบทโปรเจกต์ กฎ naming convention และสิ่งที่ห้ามทำไว้ที่นี่ ทุก agent อ่านอัตโนมัติ
- **กำหนด scope ชัดเจนให้แต่ละ agent** — ระบุโฟลเดอร์ที่รับผิดชอบและห้ามแตะ
- **บอก fallback ใน prompt** — "ถ้าเจอ error ให้ข้ามและบันทึกไว้"
- **จำกัดจำนวน Teammates** — 3–5 ตัวต่อ team เพื่อควบคุมต้นทุน
- **ใช้ Haiku สำหรับงานง่าย** — ประหยัดกว่า Sonnet มาก
- **ตรวจสอบผลลัพธ์จริงเสมอ** — อย่าเชื่อแค่คำว่า "เสร็จแล้ว"
- **ใช้ git worktree** — เมื่อหลาย agent แก้ไฟล์ในโปรเจกต์เดียวกัน
- **เปิด Agent Teams ผ่าน settings.json** — ต้องตั้งค่า `CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS=1` ก่อนใช้
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

## Quick Start: เห็นผลใน 10 นาที

```bash
# 1. ติดตั้ง Claude Code (2 นาที)
curl -fsSL https://claude.ai/install.sh | bash
export ANTHROPIC_API_KEY='sk-ant-...'

# 2. สร้างโครงสร้างโฟลเดอร์ (1 นาที)
mkdir -p .claude/agents .claude/commands

# 3. สร้าง CLAUDE.md อัตโนมัติ (2 นาที)
claude
> /init

# 4. เปิด Agent Teams ใน settings.json (1 นาที)
# เพิ่มใน .claude/settings.json:
# { "env": { "CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS": "1" } }

# 5. สร้าง agent แรก (2 นาที)
# พิมพ์ใน Claude:
> /agents
# เลือก "สร้าง agent ใหม่" แล้วบอก Claude ว่าต้องการ agent แบบไหน

# 6. ทดลองใช้ custom command (2 นาที)
claude /review src/
```

**ผล: เห็น agent ทำงานจริงใน 10 นาที!**

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
