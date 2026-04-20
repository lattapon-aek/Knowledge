---
tags:
  - claude-code
  - comparison
  - ai-tools
type: note
status: evergreen
created: "2026-04-09"
source: "https://code.claude.com/docs/en/overview"
parent_note: "[[Claude Code - Multi-Agent MOC]]"
---

# เปรียบเทียบ Agentic Coding Tools

เครื่องมือ AI สำหรับ coding ในปัจจุบันแบ่งได้เป็น **5 กลุ่มตามรูปแบบการทำงาน**

|                 | **Chat**           | **AI Copilot**   | **Agentic IDE**  | **Agentic CLI**   | **No-code**   |
| --------------- | ------------------ | ---------------- | ---------------- | ----------------- | ------------- |
| **ตัวอย่าง**    | claude.ai, ChatGPT | GitHub Copilot   | Cursor, Windsurf | Claude Code       | Lovable, Bolt |
| **เข้าถึงไฟล์** | ไม่ได้             | เฉพาะไฟล์ที่เปิด | ทั้ง codebase    | ทั้ง codebase     | —             |
| **รันโค้ด**     | ไม่ได้             | ไม่ได้           | ได้ (ผ่าน IDE)   | ได้ (bash โดยตรง) | —             |
| **Headless/CI** | ❌                  | ❌                | ❌                | ✅                 | ❌             |
| **Multi-Agent** | ❌                  | ❌                | ❌                | ✅                 | ❌             |

---

## เลือกตามงาน

| ถ้าต้องการ...                            | ใช้...              |
| ---------------------------------------- | ------------------- |
| autocomplete เร็วขณะพิมพ์โค้ด            | GitHub Copilot      |
| งาน agentic แต่ยังอยากเห็น UI / diff     | Cursor              |
| automation, CI/CD, headless, Multi-Agent | **Claude Code CLI** |
| Prototype เร็ว ไม่เขียนโค้ด              | Lovable / Bolt      |

> **สรุป:** Cursor เหมาะกับ developer ที่ต้องการ visual feedback ส่วน Claude Code CLI เหมาะกับ automation และงานที่ไม่ต้องการ GUI

## ดูเพิ่มเติม

- [[Claude Code - Multi-Agent MOC]]
- [[02 AI Systems/Agent Frameworks/Agent Frameworks - MOC|Agent Frameworks - MOC]] — เปรียบเทียบ Claude Code กับ framework ที่ใช้สร้าง agents โดยตรง
