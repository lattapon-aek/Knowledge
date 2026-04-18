---
tags:
  - claude-code
  - error-handling
  - troubleshooting
  - agents
  - version-sensitive
type: note
status: evergreen
created: "2026-04-09"
source: "https://code.claude.com/docs/en/agent-teams"
parent_note: "[[Claude Code - Multi-Agent MOC]]"
---

# Error Handling: เมื่อ Agent ทำงานผิดพลาด

---

## ความจริงเรื่อง Error Handling

Claude Code ใช้การสั่งงานแบบ prompt, hooks, และการตอบกลับจาก subagent/teammate เป็นหลัก ดังนั้น workflow ที่ robust ควรกำหนด fallback และ retry policy ไว้ล่วงหน้า

**Flow เมื่อ agent ล้มเหลว:**

```
Orchestrator spawn
    → subagent ทำงาน
    → subagent รายงานว่า "ไม่สามารถอ่านไฟล์ X ได้ เพราะไม่มีสิทธิ์"
    → Orchestrator รับรายงาน
    → Orchestrator ตัดสินใจขั้นต่อไป
```

---

## วิธีทำให้ Orchestrator จัดการ Error ได้ดี

**หลักการ:** แทนที่จะคาดหวังให้ agent "จัดการ error เอง" ควร **บอกใน prompt ตั้งแต่ต้น** ว่าถ้าเจออุปสรรคแบบนี้ให้ทำอะไร

**ตัวอย่าง prompt ที่ดี:**

```text
ตรวจสอบ security ในโฟลเดอร์ src/ และ:
- ถ้าเจอไฟล์ที่อ่านไม่ได้ ให้ข้ามและบันทึกชื่อไฟล์นั้นไว้
- ถ้ารัน lint แล้ว error ให้ลองแก้แล้วรันใหม่ได้สูงสุด 2 รอบ
- สรุปผลท้ายสุดว่าทำสำเร็จกี่ไฟล์ ข้ามกี่ไฟล์ และเหตุผล
```

---

## สัญญาณเตือนที่ Agent มีปัญหา

| อาการ | ความหมาย | วิธีรับมือ |
|---|---|---|
| ตอบว่า "เสร็จแล้ว" แต่ไม่มีผลลัพธ์จริง | Hallucination — agent คิดเองว่าเสร็จ | ถามต่อ: "แสดงไฟล์ที่แก้ให้ดูหน่อย" |
| วนซ้ำขั้นตอนเดิมหลายรอบโดยไม่คืบหน้า | ติด loop หาทางออกไม่เจอ | หยุดด้วย `Esc` แล้วปรับ prompt |
| รายงานบางส่วนแต่หายไปกลางทาง | context หมด หรือ timeout | ถาม Orchestrator: "สรุปสิ่งที่ทำได้และที่ยังค้างอยู่" |
| Task สถานะ "in progress" นานผิดปกติ | agent ค้าง | ใช้ `Esc` interrupt แล้ว spawn ใหม่ |

---

## สิ่งที่ Agent Teams จัดการได้เอง (บางส่วน)

สำหรับ **Agent Teams**:
- docs ระบุว่า teammates ส่งข้อความหากันได้โดยตรง, มี shared task list, และมี `TeammateIdle` / `TaskCompleted` hooks สำหรับประกบ workflow
- ถ้าทีมหลุดจังหวะ ให้ใช้สถานะ task, ข้อความโดยตรง, หรือสร้าง teammate ใหม่ตามสถานการณ์

---

## Best Practice สำหรับ Error-Resilient Agents

1. **ระบุ fallback ในทุก prompt** — "ถ้าทำไม่ได้ให้ทำแทนด้วย..."
2. **ให้ agent รายงานเสมอ** — "สรุปผลและสิ่งที่ยังทำไม่ได้ก่อนหยุด"
3. **จำกัดจำนวนครั้ง retry** — "ลองใหม่ได้สูงสุด 2 รอบ"
4. **ตรวจสอบผลลัพธ์จริงเสมอ** — อย่าเชื่อแค่คำว่า "เสร็จแล้ว"
5. **ใช้ permissions.deny** — ป้องกัน irreversible actions เช่น `rm -rf`, `git push --force`

---

## พื้นฐานทฤษฎีที่เกี่ยวข้อง

- [[02 AI Systems/AI Agent Fundamentals/Reference/10 - Risks และ Best Practices|Risks & Best Practices]] — Hallucination, Overreliance, Failure Handling และ Guardrails ในทฤษฎี ตรงกับปัญหาที่พบใน Claude Code จริง
- [[05 Use Cases/Application/Use Cases - Evaluate an AI Agent]]
