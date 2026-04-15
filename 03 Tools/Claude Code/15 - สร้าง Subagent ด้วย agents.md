---
tags:
  - claude-code
  - subagents
  - agents-command
  - frontmatter
type: note
status: draft
created: "2026-04-09"
source: "https://code.claude.com/docs/en/sub-agents"
parent_note: "[[Claude Code - Multi-Agent MOC]]"
---

# สร้าง Subagent ด้วย /agents

---

## วิธีที่ 1: ใช้ `/agents` (แนะนำ)

```
> /agents
```

เปิด interactive interface: View / Create / Edit / Delete agents

---

## วิธีที่ 2: สร้างไฟล์ .md โดยตรง

ไฟล์ subagent คือ markdown พร้อม YAML frontmatter:

```markdown
---
name: security-agent
description: ตรวจ security issues โดยเฉพาะ
model: claude-haiku-4-5
tools: Read, Grep
---

คุณคือวิศวกร Security ที่เชี่ยวชาญ OWASP Top 10

ทำงานเฉพาะ: ค้นหา security issues เท่านั้น
ห้าม: แก้ไขโค้ด, เขียน test, ทำสิ่งอื่นที่ไม่เกี่ยวกับ security
Output: JSON { issue, severity, file, line, recommendation }
```

---

## Frontmatter Fields ทั้งหมด

| Field | Required | ความหมาย |
|---|---|---|
| `name` | ✅ | ชื่อ identifier (lowercase, hyphen) |
| `description` | ✅ | บอก Claude ว่าเมื่อไหร่ควร delegate งานนี้ |
| `model` | — | `sonnet`, `opus`, `haiku` หรือ full model ID |
| `tools` | — | allowlist เครื่องมือที่ใช้ได้ |
| `disallowedTools` | — | denylist เครื่องมือที่ห้ามใช้ |
| `isolation` | — | `worktree` = รันใน git worktree อัตโนมัติ |
| `permissionMode` | — | `default`, `acceptEdits`, `auto`, `dontAsk`, `bypassPermissions`, `plan` |
| `memory` | — | `user`, `project`, หรือ `local` = จำข้ามการสนทนาได้ |
| `maxTurns` | — | จำกัดจำนวน turn สูงสุด |
| `skills` | — | inject เนื้อหา skill เข้า context ของ subagent ตั้งแต่เริ่ม |
| `mcpServers` | — | MCP servers ที่ใช้ได้เฉพาะใน subagent นี้ |
| `hooks` | — | lifecycle hooks สำหรับ subagent นี้โดยเฉพาะ |
| `background` | — | `true` = รันเป็น background task เสมอ |
| `effort` | — | `low`, `medium`, `high`, `max` (Opus 4.6 เท่านั้น) |
| `initialPrompt` | — | prompt แรกที่ถูก auto-submit เมื่อ agent รันเป็น main session |
| `color` | — | `red`, `blue`, `green`, `yellow`, `purple`, `orange`, `pink`, `cyan` |

> **Tip:** `tools` (allowlist) กับ `disallowedTools` (denylist) ใช้ร่วมกันได้ — ถ้าใช้ทั้งคู่ `disallowedTools` ถูกนำออกก่อน แล้ว `tools` กรองจากที่เหลือ
> **Tip:** ใช้ `isolation: worktree` เพื่อให้ agent ได้ branch แยกอัตโนมัติ

---

## ดูเพิ่มเติม
- [[14 - Built-in Subagents]]
- [[16 - บทบาท Frontend, Backend, QA]]
- [[18 - Git Worktree]]
