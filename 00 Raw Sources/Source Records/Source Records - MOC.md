---
tags:
  - rawsources
  - sourcerecords
  - registry
type: moc
status: evergreen
source: ""
parent_note: "[[Raw Sources - MOC]]"
---

# Source Records - MOC

หมวดนี้ใช้เก็บ **reconstructed source records** ที่สร้างจาก `source:` fields ของโน้ตที่มีอยู่แล้วใน vault

หมายเหตุสำคัญ:
- ไฟล์ในหมวดนี้ **ไม่ใช่ raw source ต้นฉบับ**
- ไฟล์เหล่านี้เป็นทะเบียนแหล่งอ้างอิงที่ช่วยให้เห็นว่า wiki ปัจจุบันอิงกับแหล่งใดบ้าง
- ถ้าภายหลังได้ต้นฉบับจริง ควรเก็บไว้ใน `Articles`, `Papers`, หรือ `Assets` แล้วใช้ source records เป็นตัวเชื่อมแทน

---

## Records

- [[00 Raw Sources/Source Records/Legacy Knowledge Bases - Source Record|Legacy Knowledge Bases]] — knowledge base ภายในที่เคยใช้เป็นฐานเขียนโน้ต
- [[00 Raw Sources/Source Records/Official Documentation Bundles - Source Record|Official Documentation Bundles]] — bundle ของ official docs หลายเจ้า
- [[00 Raw Sources/Source Records/Agent Courses And Guides - Source Record|Agent Courses And Guides]] — คอร์สและคู่มือที่เกี่ยวกับ agents
- [[00 Raw Sources/Source Records/Claude Code Official Docs - Source Record|Claude Code Official Docs]] — เอกสารทางการของ Claude Code
- [[00 Raw Sources/Source Records/External Articles - Source Record|External Articles]] — บทความภายนอกที่ถูกอ้างในโน้ตปัจจุบัน
- [[00 Raw Sources/Source Records/Dive into Claude Code Paper - Source Record|Dive into Claude Code Paper]] — arxiv 2604.14228, source code analysis ของ Claude Code architecture
- [[00 Raw Sources/Source Records/RAG-Anything - Source Record|RAG-Anything]] — arxiv 2510.12323, multimodal RAG framework
- [[00 Raw Sources/Source Records/LLM Engineer Toolkit - Source Record|LLM Engineer Toolkit]] — curated list ของ 120+ LLM libraries
- [[00 Raw Sources/Source Records/AI Engineering From Scratch - Source Record|AI Engineering From Scratch]] — curriculum/course (reference only)
- [[00 Raw Sources/Source Records/Harness Engineering Sources - Source Record|Harness Engineering Sources]] — 9 sources เรื่อง harness engineering (Anthropic, OpenAI, Martin Fowler, LangChain ฯลฯ)

---

## ใช้ทำอะไร

- ตรวจว่าโน้ตแต่ละชุดมาจากแหล่งไหน
- มองเห็น coverage ของ sources โดยไม่ต้องเปิดทีละไฟล์
- ช่วย migration จาก wiki-only ไปสู่ raw-sources-aware vault
- เป็นฐานสำหรับสร้าง `log.md` หรือ ingestion records ในอนาคต
