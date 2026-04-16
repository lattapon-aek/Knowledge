---
tags:
  - claude-code
  - multi-provider
  - architecture
  - limitations
  - version-sensitive
type: note
status: draft
created: "2026-04-09"
source: "https://code.claude.com/docs/en/agent-teams"
parent_note: "[[Claude Code - Multi-Agent MOC]]"
---

# Multi-Provider AI — ความจริงที่ต้องรู้

---

## ❌ สิ่งที่ต้องมีตัวกลาง

ถ้าจะให้โมเดลต่าง provider ทำงานร่วมกัน ต้องมี **โค้ดหรือ service ตัวกลาง** คอยประสานการเรียก API และรวมผลลัพธ์

---

## ✅ Multi-Provider ที่ทำได้จริง

ผ่าน **โค้ดหรือ API เป็นตัวกลาง** — orchestration อยู่ที่โค้ดที่เราสร้างเอง

```mermaid
flowchart TD
    DEV[นักพัฒนาเขียนโค้ด Orchestrator]
    DEV -->|เรียก API| CA[Claude API ผลลัพธ์ A]
    DEV -->|เรียก API| OA[OpenAI API ผลลัพธ์ B]
    DEV -->|เรียก API| GA[Gemini API ผลลัพธ์ C]
    CA & OA & GA --> RES[โค้ดรวมผลลัพธ์ output สุดท้าย]
```

---

## เปรียบเทียบ

| | Claude Code Agent Teams | Multi-Provider (ผ่านโค้ด) |
|---|---|---|
| **Agent คุยกันได้** | ✅ โดยตรง (mailbox) | ❌ ต้องผ่านโค้ดตัวกลาง |
| **Model ที่ใช้** | Claude เท่านั้น | ใช้ได้ทุกเจ้า |
| **ตั้งค่า** | Natural language | เขียนโค้ด API calls เอง |
| **Status** | Experimental | ขึ้นอยู่กับโค้ดที่เขียน |

---

## พื้นฐานทฤษฎีที่เกี่ยวข้อง

- [[02 AI Systems/AI Agent Fundamentals/12 - LLM พื้นฐาน|LLM พื้นฐาน]] — รายชื่อ LLM ต่างเจ้า (GPT-4, Llama, Gemini, Claude) และความแตกต่างด้านสถาปัตยกรรม
