---
tags:
  - refactor
  - folder-structure
  - maintenance
type: guide
status: evergreen
source: "vault-local folder structure plan"
parent_note: "[[Knowledge Refactor - Task Board]]"
---

# Knowledge Folder Structure Plan v2

แผนนี้ใช้สำหรับจัดโครง folder ของ vault ให้ใช้รูปแบบเดียวกันมากขึ้นในส่วนที่เป็น knowledge ทั้งหมด

เป้าหมาย:
- ให้เห็นบทบาทของ folder ทันที
- ลดความรู้สึกว่า `01 Foundations` กับ `02 AI Systems` ใช้ตรรกะคนละแบบ
- แยก `core`, `bridge`, `application`, `reference`, และ `implementation` ให้คงเส้นคงวา
- ไม่แตะความหมายของเนื้อหาเดิม ถ้าไม่จำเป็นต้องย้ายจริง
- ปรับ folder architecture โดยไม่ทำให้เนื้อหาเดิมหาย ย่อ หรือเปลี่ยนความหมาย

---

## Hard Rules: No Content Loss

ทุก phase ของการปรับ folder architecture ต้องถือกติกานี้เป็นข้อบังคับ:

1. ห้ามลบเนื้อหาเดิม
2. ห้ามย่อหรือ rewrite เนื้อหาหลักในระหว่างงานย้าย folder
3. คงชื่อไฟล์เดิมให้มากที่สุด เพื่อลด link churn
4. ย้าย MOC ให้อยู่ root ของ topic เสมอ ไม่ย้ายเข้า role folder
5. ทุก phase ต้องตรวจ:
   - จำนวนไฟล์ `.md` ไม่ลดลงโดยไม่ตั้งใจ
   - broken wikilinks ต้องเป็น `MISSING 0`
   - `git diff --check` ต้องผ่าน
6. Commit แยกตาม phase เพื่อ rollback ได้ง่าย

งานนี้เป็น folder architecture refactor ไม่ใช่งานปรับเนื้อหาเชิงความรู้

---

## หลักการออกแบบ

1. ใช้คำเรียก role เดียวกันทั้ง vault
   - `Core` = เนื้อหาหลักของหัวข้อนั้น
   - `Bridge` = หน้าเชื่อมข้าม topic
   - `Application` = ตัวอย่างใช้งาน / decision path
   - `Reference` = โน้ตอ้างอิงหรือ volatile support
   - `Implementation` = code-level / workflow-level / runtime-level detail

2. หนึ่ง topic มี canonical home เดียว
   - ถ้า topic เดียวมีหลายมุม ให้คงหน้า bridge ไว้ แต่ไม่ให้แย่งบทบาท owner

3. ให้ folder บอก role ก่อนบอก content
   - อ่านชื่อ folder แล้วควรรู้ทันทีว่าไฟล์ข้างในเป็นอะไร

4. ถ้าหมวดไหนไม่ต้องการ role ทุกแบบ ไม่ต้องฝืนใส่
   - ไม่จำเป็นต้องมี `Reference` ถ้าไม่มีของที่ควรแยก
   - ไม่จำเป็นต้องมี `Application` ถ้าเป็นหมวด theory ล้วน

---

## โครง folder ที่อยากได้

```text
Knowledge/
├── 00 Raw Sources/
├── 01 Foundations/
├── 02 AI Systems/
├── 03 Tools/
├── 04 Synthesis/
├── 05 Use Cases/
├── 06 Engineering/
├── _Templates/
├── Home.md
├── index.md
├── AGENTS.md
└── README.md
```

### แผน role ของแต่ละ folder

- `01 Foundations`
  - `Core` = LLM / prompt / context / tokenizer / evaluation primitives
  - `Bridge` = notes ที่ต้องเชื่อมไป `02 AI Systems`

- `02 AI Systems`
  - `Core` = agent runtime, framework selection, memory, retrieval, control, evaluation, protocol
  - `Bridge` = notes ที่ต้องเชื่อมไป `01 Foundations`, `04 Synthesis`, หรือ `06 Engineering`
  - `Application` = notes ที่สอนการใช้งานเชิงระบบ

- `03 Tools`
  - `Core` = tool-specific knowledge
  - `Bridge` = notes ที่เชื่อมไป core concepts
  - `Reference` = volatile workflow / release-sensitive notes

- `04 Synthesis`
  - `Bridge` = comparison / decision / tradeoff notes
  - `Core` = bridge notes ที่ถูกยอมรับเป็น canonical synthesis

- `05 Use Cases`
  - `Application` = decision paths, entry points, practical examples
  - `Decision` = when to use / when not to use / choose between options

- `06 Engineering`
  - `Core` = implementation architecture
  - `Implementation` = recipes, framework notes, code/runtime details
  - `Reference` = project notes / derived guides / maintenance notes

---

## Target Architecture

โครงปลายทางที่ต้องการสำหรับรอบนี้:

```text
01 Foundations/
├── LLM Foundations/
│   ├── LLM Foundations - MOC.md
│   ├── Core/
│   └── Bridge/
├── Prompt Engineering/
│   ├── Prompt Engineering - MOC.md
│   ├── Core/
│   └── Bridge/
├── Context Windows/
│   ├── Context Windows - MOC.md
│   └── Core/
└── Tokenizer in AI/
    ├── Tokenizer in AI - MOC.md
    └── Core/

02 AI Systems/
├── AI Agent Fundamentals/
│   ├── AI Agent Fundamentals - MOC.md
│   ├── Core/
│   └── Reference/
├── Agent Frameworks/
│   ├── Agent Frameworks - MOC.md
│   └── Core/
├── Memory Systems/
│   ├── Memory Systems - MOC.md
│   ├── Core/
│   └── Application/
├── RAG/
│   ├── RAG - MOC.md
│   ├── Core/
│   ├── Retrieval/
│   └── Evaluation/
├── Guardrails/
│   ├── Guardrails - MOC.md
│   ├── Core/
│   └── Operations/
├── Evals/
│   ├── Evals - MOC.md
│   ├── Core/
│   └── Application/
└── MCP/
    ├── MCP - MOC.md
    ├── Core/
    ├── Client/
    ├── Security/
    └── Bridge/

03 Tools/Claude Code/
├── Claude Code - Multi-Agent MOC.md
├── Core/
├── Workflow/
└── Reference/

04 Synthesis/
├── Synthesis - MOC.md
├── Bridge/
└── Decision/

05 Use Cases/
├── Use Cases - MOC.md
├── Application/
└── Decision/
```

`06 Engineering` มีโครง implementation-specific อยู่แล้ว จึงไม่ต้องรื้อใหญ่ในรอบนี้

---

## โครงย่อยที่อยากให้สม่ำเสมอ

### 01 Foundations

- `LLM Foundations`
- `Prompt Engineering`
- `Context Windows`
- `Tokenizer in AI`

### 02 AI Systems

- `AI Agent Fundamentals`
- `Agent Frameworks`
- `Memory Systems`
- `RAG`
- `Guardrails`
- `Evals`
- `MCP`

### 03 Tools

- `Claude Code`

### 04 Synthesis

- single-topic bridge notes
- comparison notes
- decision synthesis notes

### 05 Use Cases

- one use case = one decision path
- one topic = one practical entry point

### 06 Engineering

- `Frameworks`
- `Architecture to Code`
- `Patterns`
- `Recipes`
- `Decisions`
- `Project Notes`

---

## กติกาย้ายหมวด

- ถ้าหน้าไหนเป็น owner หลักของ topic นั้น ให้คงไว้
- ถ้าหน้าไหนเป็น comparison ระหว่างหลาย topic ให้ย้ายหรือคงไว้ใน `04 Synthesis`
- ถ้าหน้าไหนเป็น decision path ให้ย้ายหรือคงไว้ใน `05 Use Cases`
- ถ้าหน้าไหนเป็น implementation detail ให้ย้ายหรือคงไว้ใน `06 Engineering`
- ถ้าหน้าไหนเป็น volatile tool reference ให้คงไว้ใน `03 Tools`

---

## สิ่งที่ต้องระวัง

- อย่าใช้ folder เดียวแบกทั้ง core และ bridge ถ้าแยกได้
- อย่า rename topics โดยไม่อัปเดต registry
- อย่าเปลี่ยนเนื้อหา ถ้ายังแค่จัดวางโครง
- ถ้าต้องย้าย note ให้ย้ายพร้อม link map และ audit log

---

## ใช้ร่วมกับ

- [[Knowledge Topic Registry]]
- [[Knowledge Topic Audit]]
- [[Knowledge Refactor - Task Board]]
