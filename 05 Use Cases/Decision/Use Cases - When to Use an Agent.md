---
tags:
  - agent
  - decision-framework
  - use-cases
type: usecase
status: evergreen
source: "Google Skills — Agent Fundamentals (Module 4)"
parent_note: "[[05 Use Cases/Use Cases - MOC]]"
---

# เมื่อไรควรและไม่ควรใช้ Agent



---

## Use Cases ที่ Agent เด่นมาก

### 1. Complex multi-step workflows
**ตัวอย่าง:** การจัดการ expense report

Agent ทำได้ในคำสั่งเดียว:
- ดึง receipt จากอีเมล
- จัดหมวดหมู่ค่าใช้จ่าย
- ตรวจ policy
- ส่งขออนุมัติ
- อัปเดต accounting system

### 2. Dynamic problem solving
**ตัวอย่าง:** การจองทริปในโลกจริงที่มีความไม่แน่นอน:
- เที่ยวบินเต็ม, ราคาเปลี่ยน, ตารางชนกัน
- Agent ปรับแผนตามข้อมูลใหม่ที่ค้นพบได้

### 3. Ongoing task management
**ตัวอย่าง:** "ติดตามราคาตั๋วไป Tokyo จองทันทีเมื่อราคาต่ำกว่า $800"
- ไม่ใช่ one-shot query แต่เป็น responsibility ต่อเนื่อง

### 4. Integrated experiences
**ตัวอย่าง:** วางแผนอีเวนต์ ต้องประสานหลายระบบ:
- calendar + venue database + catering + invitation platform
- Agent orchestrate ข้ามระบบได้แบบไร้รอยต่อ

---

## Use Cases เฉพาะที่ Agent เหมาะมาก

### Automated incident response (Event-triggered)
เมื่อ production error เกิด:
- วิเคราะห์ error logs และ stack traces
- เช็ก recent deployments
- ประเมิน severity
- สร้าง incident ticket
- route ไป on-call team
- rollback ถ้าเข้าเกณฑ์
- อัปเดต stakeholders

### Research & analysis (Chat-triggered)
`Prepare a competitive analysis of our top three competitors`
- หา competitor → ดึงข่าว → ดึงข้อมูลการเงิน → วิเคราะห์ product → สร้าง comparison matrix → รายงานพร้อม citation

### Daily business intelligence (Time-triggered)
ทุกเช้าเวลา 8 โมง:
- ดึง metrics จากระบบ sales, support, product
- เทียบกับ target และ historical trends
- หา anomaly
- ส่ง briefing แบบ personalized

---

## เมื่อ "ไม่ควร" ใช้ Agent

| กรณี | ทางเลือกที่ดีกว่า |
|---|---|
| Simple Q&A — เวลาทำการ, วิธีรีเซ็ตรหัสผ่าน | FAQ page, retrieval system, simple chatbot |
| Single API call — อากาศวันนี้, ราคาหุ้น | Direct API call หรือ function calling |
| High-volume, low-complexity — ส่ง notification, resize images | Traditional automation |
| Deterministic workflows — ถ้า order > $100 ให้ free shipping | Workflow engine, rules engine |
| Real-time, latency-sensitive — microsecond trading, game actions | Agent มี reasoning loop ทำให้ latency สูงขึ้น |

---

## Decision Framework

คำถาม 4 ข้อก่อนตัดสินใจ:

1. ต้องมีหลายขั้นตอนที่พึ่งพากันหรือไม่?
2. ต้องปรับตัวตามสิ่งที่ค้นพบระหว่างทางหรือไม่?
3. ต้องใช้ reasoning เพื่อเลือกแนวทางที่ดีที่สุดหรือไม่?
4. ต้องลงมือทำใน external systems หรือไม่?

**ถ้าคำตอบเป็น "ใช่" ส่วนใหญ่ → นี่คือ agent-shaped problem**

```
Start
  └─ Multiple steps?
       ├─ No → Complex reasoning?
       │          ├─ No → Use Simple API
       │          └─ Yes → External actions?
       │                    ├─ No → Use LLM
       │                    └─ Yes → Use Agent ✓
       └─ Yes → Needs adaptation?
                  ├─ No → Use Workflow Automation
                  └─ Yes → Use Agent ✓
```

---

## Tradeoffs ของการใช้ Agent

| ด้าน | ผลกระทบ |
|---|---|
| Latency | สูงขึ้น เพราะมี reasoning loop |
| Cost | สูงขึ้น เพราะ reasoning + tool orchestration ซับซ้อน |
| Complexity | สูงขึ้น ทั้ง architecture, monitoring, failure handling |

**หลักคิด:** เริ่มจาก solution ที่ง่ายที่สุดก่อน เพิ่ม agent capabilities เฉพาะจุดที่สร้าง value ชัดเจน

---

## ดูต่อ

- [[04 Synthesis/Decision/Synthesis - Workflow vs AI Agent|Workflow vs AI Agent]]
- [[02 AI Systems/AI Agent Fundamentals/Reference/10 - Risks และ Best Practices]]
- [[05 Use Cases/Application/Use Cases - Build an AI Agent]]
- [[05 Use Cases/Decision/Use Cases - Move from Single to Multi-Agent]]

## ตัวอย่าง Implementation จริง

- [[03 Tools/Claude Code/Workflow/23 - ข้อจำกัด Agent Teams|ข้อจำกัด Agent Teams]] — Tradeoffs ของ Multi-Agent ใน Claude Code: latency, cost, context limit, experimental status
- [[03 Tools/Claude Code/Workflow/24 - Best Practices & Checklist|Best Practices & Checklist]] — Checklist ก่อน deploy และ decision guide ว่าควรใช้ 1 Session / Subagents / Agent Teams
