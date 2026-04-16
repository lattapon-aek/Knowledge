---
tags:
  - claude-code
  - agent-tool
  - subagents
  - version-sensitive
type: note
status: draft
created: "2026-04-09"
source: "https://code.claude.com/docs/en/sub-agents"
parent_note: "[[Claude Code - Multi-Agent MOC]]"
---

# Agent Tool (เดิมชื่อ Task Tool)

> ℹ️ ตั้งแต่ Claude Code **v2.1.63** เป็นต้นมา "Task tool" เปลี่ยนชื่อเป็น **"Agent tool"** (ชื่อเก่ายังใช้ได้เป็น alias)

**Agent Tool** = เครื่องมือ internal ที่ Claude ใช้ **โดยอัตโนมัติ** เพื่อ spawn Subagent จากภายใน session

ผู้ใช้ไม่ต้องเรียกเองโดยตรง — แค่บอก Claude ว่าต้องการ delegate งาน:

```text
ช่วย delegate งานตรวจ security ใน /api ให้ security-agent
แล้ว qa-agent เขียน unit test สำหรับ auth.ts ด้วย
```

---

## Agent Tool vs Agent Teams

| | Agent Tool (Subagent) | Agent Teams |
|---|---|---|
| ทำงานใน | session เดียวกัน | Claude Code instances แยก |
| Teammate คุยกันได้ | ❌ (รายงานกลับ main เท่านั้น) | ✅ โดยตรง |
| เหมาะกับ | งาน focused ต้องการแค่ผลลัพธ์ | งานซับซ้อนที่ต้อง collaborate |

---

## พื้นฐานทฤษฎีที่เกี่ยวข้อง

- [[02 AI Systems/AI Agent Fundamentals/14 - Tools: การออกแบบและทำงาน|Tools: การออกแบบและทำงาน]] — Agent Tool คือ Tool ชนิดพิเศษ: แทนที่จะ return data กลับมา มัน spawn agent อีกตัวเป็น output
- [[02 AI Systems/AI Agent Fundamentals/04 - สถาปัตยกรรม Agent: Model + Tools + Orchestration|Orchestration Component]] — การ spawn subagent ผ่าน Agent Tool คือ Orchestration ที่ทำงานจริง
