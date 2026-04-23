---
tags:
  - agent
  - definition
type: note
status: evergreen
source: "Google Skills — Agent Fundamentals (Module 1)"
parent_note: "[[AI Agent Fundamentals - MOC]]"
---

# AI Agent คืออะไร



---

## นิยาม

จาก Google Whitepaper:

> A generative AI agent is an application that **attempts to achieve a goal** by observing the world and acting upon it using the tools that it has at its disposal.

สรุปเชิงปฏิบัติ:
- เป็น application ที่พยายามทำเป้าหมายให้สำเร็จ
- สังเกต environment ระหว่างทาง
- ลงมือทำผ่านเครื่องมือที่มี

---

## ปัญหาที่ทำให้ Agent เกิดขึ้น

### ช่องว่างระหว่าง "รู้" กับ "ลงมือทำ"

LLM รุ่นแรกสามารถ:
- ให้คำตอบได้
- ให้ขั้นตอนได้
- ให้ตัวอย่างโค้ดได้

แต่ยัง **ไปแตะโลกภายนอกไม่ได้** — ผู้ใช้ยังต้องไปลงมือทำทุกอย่างเอง

### Function Calling ยังไม่พอ

LLM + Function Calling เรียก API ได้ แต่ผู้ใช้หรือโค้ดรอบนอกยังต้อง orchestrate ทุกขั้นตอนเอง

### สิ่งที่ผู้ใช้ต้องการจริง ๆ

ระบบที่พูดว่า:
> "ฉันหาตัวเลือกเที่ยวบินที่เข้ากับปฏิทินของคุณแล้ว จับคู่กับโรงแรมใกล้เคียงในงบแล้ว พร้อมจองตัวเลือกที่เหมาะที่สุด ต้องการให้ดำเนินการต่อหรือไม่"

นี่คือ promise ของ agent: จากระบบที่ "ตอบ" ไปสู่ระบบที่ **"พยายามทำงานให้สำเร็จ"**

---

## ตัวอย่างเปรียบเทียบ: Should I wear a jacket today?

| ระดับ | สิ่งที่ทำ | ข้อจำกัด |
|---|---|---|
| LLM | ให้คำแนะนำทั่วไป เช่น ถ้าต่ำกว่า 60°F ควรใส่ | ไม่มีข้อมูล environment จริง |
| LLM + Function Calling | เรียก weather API → ตอบว่าควรใส่ | ผู้ใช้ยังต้องควบคุม flow |
| Agent | เช็ก location → เรียก weather API → เช็ก calendar → ดูช่วงที่ผู้ใช้ต้องออกนอก → สรุปพร้อมเหตุผล | — |

ตัวอย่าง output จาก agent:
> "ตอนนี้ 55°F แต่จะลดเหลือ 48°F ตอน 6 PM และคุณมี outdoor meeting ตอนนั้น ดังนั้นควรใส่แจ็กเก็ตแน่นอน"

---

## Mental Model

```
LLMs          → Consultants — ให้คำแนะนำ แต่ไม่ลงมือทำ
LLM + Tools   → Assistants  — ใช้เครื่องมือได้เมื่อถูกสั่ง
Agents        → Trusted employees — รับเป้าหมายแล้วหาวิธีทำเอง
```

---

## นิยามอีกมุม: Brain + Body

**(จาก HuggingFace Agents Course)**

> An Agent is a system that leverages an AI model to interact with its environment in order to achieve a user-defined objective. It combines reasoning, planning, and the execution of actions (often via external tools) to fulfill tasks.

Agent มี 2 ส่วนหลัก:

| ส่วน | ความหมาย |
|---|---|
| **Brain (AI Model)** | ส่วนคิด — reasoning, planning, ตัดสินใจว่า action ไหนดีที่สุด |
| **Body (Capabilities & Tools)** | ส่วนทำ — สิ่งที่ agent ถูก equip มาให้ทำได้ |

*Agent มี agency — ความสามารถ interact กับ environment*

---

## Spectrum of Agency

Agent ไม่ได้มีแค่แบบเดียว — มีอยู่บน **continuous spectrum** ของระดับ autonomy:

| Agency Level | คำอธิบาย | ชื่อเรียก | ตัวอย่าง Pattern |
|---|---|---|---|
| ☆☆☆ | Output ไม่มีผลต่อ program flow | Simple Processor | `process_llm_output(llm_response)` |
| ★☆☆ | Output กำหนด control flow พื้นฐาน | Router | `if llm_decision(): path_a() else: path_b()` |
| ★★☆ | Output กำหนดว่าจะเรียก function ไหน | Tool Caller | `run_function(llm_chosen_tool, llm_chosen_args)` |
| ★★★ | Output ควบคุม iteration และ continuation | Multi-step Agent | `while llm_should_continue(): execute_next_step()` |
| ★★★ | Agentic workflow หนึ่งเรียก workflow อีกอัน | Multi-Agent | `if llm_trigger(): execute_agent()` |

*(จาก smolagents conceptual guide)*

---

## Use Cases ของ Agent

| Use Case | ตัวอย่าง |
|---|---|
| Personal Virtual Assistants | Siri, Alexa, Google Assistant — ตั้งเตือน, ส่ง message, ควบคุมอุปกรณ์ |
| Customer Service Chatbots | ตอบคำถาม, troubleshoot, เปิด ticket, ทำ transaction |
| AI NPC in Games | LLM-powered NPC ที่ respond contextually แทน rigid behavior tree |

ถ้าต้องการเส้นทางใช้งานจริงต่อ ให้ดู [[05 Use Cases/Application/Use Cases - Build an AI Agent]] และ [[05 Use Cases/Decision/Use Cases - Move from Single to Multi-Agent]]

---

## ดูต่อ

- [[02 - วิวัฒนาการ LLM สู่ Agent]]
- [[03 - คุณสมบัติ 5 อย่างของ Agent]]
- [[11 - Key Takeaways และ Quick Reference]]
- [[01 Foundations/LLM Foundations/Bridge/12 - LLM พื้นฐาน|12 - LLM พื้นฐาน]]
- [[02 AI Systems/AI Agent Fundamentals/Core/08 - Harness Engineering|08 - Harness Engineering]] — Agent = Model + Harness, ระบบรอบ ๆ model ที่ทำให้ agent ทำงานได้จริง

## ตัวอย่าง Implementation จริง

- [[03 Tools/Claude Code/Core/01 - Claude Code คืออะไร|Claude Code คืออะไร]] — Claude Code คือ AI Agent สำหรับ coding ที่ implement แนวคิดนี้จริง (Brain = Claude LLM, Body = Read/Write/Edit/Bash tools)
