---
tags:
  - claude-code
  - memory
  - configuration
  - CLAUDE-md
type: note
status: draft
created: "2026-04-09"
source: "https://code.claude.com/docs/en/memory"
parent_note: "[[Claude Code - Multi-Agent MOC]]"
---

# CLAUDE.md: ความจำร่วมของทีม

Claude Code มี **2 ระบบความจำ** ที่ทำงานควบคู่กัน และโหลดขึ้นมาทุก session:

| | **CLAUDE.md files** | **Auto memory** |
|---|---|---|
| **ใครเขียน** | คุณ | Claude |
| **เนื้อหา** | Instructions และ rules | Learnings ที่ Claude สังเกต |
| **Scope** | Project, user, หรือ org | Per working tree |
| **โหลดเมื่อ** | ทุก session | ทุก session (200 บรรทัดแรก หรือ 25KB) |
| **ใช้สำหรับ** | Coding standards, workflows, architecture | Build commands, debugging insights, preferences |

---

## CLAUDE.md files

### ตำแหน่งและ Scope

| Scope | ตำแหน่ง | ใช้สำหรับ | Shared กับ |
|---|---|---|---|
| **Managed policy** | macOS: `/Library/Application Support/ClaudeCode/CLAUDE.md`<br>Linux: `/etc/claude-code/CLAUDE.md`<br>Windows: `C:\Program Files\ClaudeCode\CLAUDE.md` | Company-wide standards (deploy โดย IT) | ทุกคนในองค์กร |
| **Project** | `./CLAUDE.md` หรือ `./.claude/CLAUDE.md` | Team-shared standards ของโปรเจกต์ | ทีม (via git) |
| **User** | `~/.claude/CLAUDE.md` | Personal preferences ทุกโปรเจกต์ | เฉพาะตัวเอง |
| **Local** | `./CLAUDE.local.md` | Personal project-specific (เพิ่มใน .gitignore) | เฉพาะตัวเอง |

> ℹ️ CLAUDE.md files ถูกโหลดโดยเดิน up directory tree — ถ้ารัน Claude ใน `foo/bar/` จะโหลด `foo/bar/CLAUDE.md`, `foo/CLAUDE.md` และ `CLAUDE.local.md` ที่พบระหว่างทาง

---

## สร้าง CLAUDE.md

**วิธีที่ 1: ใช้ `/init` (แนะนำ)**

```
> /init
```

Claude สแกนโปรเจกต์ทั้งหมดแล้วสร้าง CLAUDE.md ให้เอง พร้อม tech stack, โครงสร้าง และ conventions

> ℹ️ ถ้า CLAUDE.md มีอยู่แล้ว `/init` จะ suggest improvements แทนการ overwrite

**วิธีที่ 2: สั่งเขียนเอง**

```
> อ่านโปรเจกต์ทั้งหมดแล้วสร้าง CLAUDE.md
> ให้มี: tech stack, โครงสร้างโฟลเดอร์, coding conventions และ API endpoints สำคัญ
```

---

## ตัวอย่างเนื้อหา

```markdown
# โปรเจกต์: dohome E-commerce Platform
## Tech Stack
- Frontend: Next.js 14, TypeScript, Tailwind CSS
- Backend: Node.js, PostgreSQL, Redis
## รูปแบบการเขียนโค้ด
- ใช้ TypeScript strict mode เสมอ
## API Endpoints สำคัญ
- /api/products, /api/orders, /api/auth
```

> **เคล็ดลับ:** เขียนเหมือน README แต่เพื่อให้ AI อ่าน — ยิ่งละเอียดยิ่งดี แต่รักษาให้อยู่ภายใน **200 บรรทัด** ต่อไฟล์เพื่อให้ Claude ตามได้ดี

---

## จัดระเบียบด้วย `.claude/rules/`

สำหรับโปรเจกต์ขนาดใหญ่ — แยก instructions เป็นไฟล์ย่อยใน `.claude/rules/`

```
.claude/
├── CLAUDE.md        # คำสั่งหลัก
└── rules/
    ├── code-style.md   # Style guidelines
    ├── testing.md      # Testing conventions
    └── security.md     # Security requirements
```

สามารถ scope rules ให้ match ไฟล์บางประเภทด้วย frontmatter:

```markdown
---
paths:
  - "src/api/**/*.ts"
---
# API Rules
- ทุก endpoint ต้องมี input validation
```

Rules ที่ไม่มี `paths` จะโหลดทุก session เหมือน CLAUDE.md ปกติ

---

## อัพเดต CLAUDE.md

```
> /memory
```

คำสั่ง `/memory` แสดงไฟล์ CLAUDE.md, CLAUDE.local.md, และ rules ทั้งหมดที่ session นี้โหลด — เลือกไฟล์เพื่อเปิดใน editor

---

## Auto Memory

> ℹ️ ต้องใช้ Claude Code **v2.1.59+**

Claude บันทึก notes ให้ตัวเองอัตโนมัติ — build commands, debugging insights, code style, workflow habits

**ที่เก็บ:** `~/.claude/projects/<project>/memory/`

```
memory/
├── MEMORY.md          # Index โหลดทุก session (200 บรรทัดแรก)
├── debugging.md       # Debugging patterns
└── api-conventions.md # API design decisions
```

- เปิด/ปิดได้ผ่าน `/memory` หรือตั้ง `"autoMemoryEnabled": false` ใน settings
- ไฟล์ทั้งหมดเป็น markdown ธรรมดา — แก้หรือลบได้ตลอดเวลา
