---
tags:
  - claude-code
  - commands
  - workflow
  - automation
  - version-sensitive
type: note
status: evergreen
created: "2026-04-09"
source: "https://code.claude.com/docs/en/skills"
parent_note: "[[Claude Code - Multi-Agent MOC]]"
---

# Custom Commands (.claude/commands/)

สร้างคำสั่งเองได้ — นำกลับมาใช้ซ้ำได้ไม่ต้องพิมพ์ยาวซ้ำๆ

---

## สร้าง Custom Command

```
> สร้างไฟล์ .claude/commands/review.md สำหรับ /review command
> ให้ตรวจสอบโค้ด 3 ด้าน: Security (OWASP Top 10), Performance และ Style
> output เป็น JSON format
```

**ผลลัพธ์ — `.claude/commands/review.md`:**

```markdown
ตรวจสอบโค้ดในไฟล์ที่ระบุโดย:
1. Security: หาช่องโหว่ตาม OWASP Top 10
2. Performance: หาจุดที่ทำให้ช้า
3. Style: ตรวจ coding convention
Output เป็น JSON: { "security": [], "performance": [], "style": [] }
```

---

## วิธีเรียกใช้

```bash
claude /review src/api/auth.ts
claude /deploy-check
claude /update-memory
```
