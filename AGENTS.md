---
tags:
  - agents
  - schema
  - workflow
type: guide
status: evergreen
source: ""
parent_note: "[[Home]]"
---

# AGENTS

เอกสารนี้คือ schema กลางสำหรับ agent ที่จะทำงานกับ vault นี้  
เป้าหมายคือทำให้ agent ทำหน้าที่เป็นผู้ดูแล wiki อย่างมีวินัย ไม่ใช่แค่ตอบแชตทั่วไป

---

## Mission

agent ต้องช่วยดูแล vault นี้ให้เป็น **persistent knowledge base** สำหรับ AI systems

งานหลักของ agent:
- ingest แหล่งข้อมูลใหม่เข้าสู่ wiki
- สรุปและสังเคราะห์ความรู้จากหลายแหล่ง
- อัปเดต cross-links และ MOC
- รักษาความสม่ำเสมอของ style, metadata, และโครงสร้าง
- ยกระดับสิ่งที่ค้นพบจาก chat ให้กลายเป็น wiki pages เมื่อมีคุณค่าเชิงความรู้

สิ่งที่ agent ไม่ควรทำ:
- เขียนทับหรือดัดแปลง raw source ต้นฉบับ
- เพิ่มเนื้อหาโดยไม่มีหลักฐานรองรับเมื่อผู้ใช้ต้องการความน่าเชื่อถือสูง
- สร้างโครงสร้างใหม่แบบรื้อของเดิมโดยไม่จำเป็น

---

## Vault Layers

vault นี้มี 5 ชั้นหลัก:

1. `00 Raw Sources/`
   - เก็บแหล่งข้อมูลต้นฉบับ
   - เป็น source of truth
   - agent อ่านได้ แต่ไม่ควรแก้ไขต้นฉบับ

2. `01 Foundations/` ถึง `02 AI Systems/`
   - คือชั้น concept และ architecture
   - agent สามารถสร้าง, แก้, สรุป, cross-link, และปรับปรุงได้

3. `03 Tools/`
   - คือชั้น tool-specific knowledge ที่เปลี่ยนตาม release, config, terminal mode, หรือ behavior ได้
   - ถ้าเป็น Claude Code ให้แยก concept ที่นิ่งออกจาก notes ที่ `version-sensitive`

4. `04 Synthesis/` ถึง `06 Engineering/`
   - คือชั้น implementation และ framework-specific engineering notes
   - agent สามารถสร้าง, แก้, สรุป, cross-link, และปรับปรุงได้

5. Schema และ workflow docs
   - เช่น `AGENTS.md`, `Home.md`, `index.md`, `Vault Standards - *.md`
   - ใช้เป็นกติกากลางสำหรับการดูแล vault

---

## Entry Points

เมื่อ agent เริ่มทำงาน ให้ใช้ไฟล์ต่อไปนี้เป็น entry points:

- [[Home]] — ภาพรวมและ reading paths
- [[index]] — catalog กลางของทั้ง vault
- [[00 Raw Sources/Raw Sources - MOC|Raw Sources - MOC]] — ชั้น raw sources
- [[00 Raw Sources/Articles/Source Manifests - MOC|Source Manifests - MOC]] — entry points สำหรับ source families ที่ active
- [[03 Tools/Claude Code/Claude Code - Multi-Agent MOC|Claude Code - Multi-Agent MOC]] — entry point สำหรับ Claude Code notes ที่แบ่ง stable / version-sensitive
- [[04 Synthesis/Synthesis - MOC|Synthesis - MOC]] — ชั้นสังเคราะห์ข้ามหมวด
- [[05 Use Cases/Use Cases - MOC|Use Cases - MOC]] — reading paths แบบใช้งานจริง
- [[06 Engineering/Engineering - MOC|Engineering - MOC]] — ชั้น implementation และ framework-specific notes
- [[Vault Standards - Properties]] — มาตรฐาน metadata
- [[Vault Workflow - Capture to Evergreen]] — workflow ของ note lifecycle

---

## Canonical Rules

### 1. Raw Sources vs Wiki

- raw sources อยู่ใน `00 Raw Sources/`
- note สรุปหรือ synthesis ต้องไม่ไปอยู่ใน raw sources
- ถ้าสร้างความรู้ใหม่จาก source ให้ไปสร้างในหมวด wiki ที่เหมาะแทน

### 2. Metadata

ทุก note ใหม่ควรใช้ properties มาตรฐาน:

- `tags`
- `type`
- `status`
- `source`
- `parent_note`
- `created`
- `updated`

กติกา:
- ใช้ `source` เป็น plain string
- ใช้ `parent_note` แทน `up`
- ถ้าไม่มีค่า ใช้ `""`

### 3. Naming

- note แบบลำดับใช้ `NN - หัวข้อ.md`
- หน้าแม่ใช้ `Topic - MOC.md`
- โน้ตสังเคราะห์ใช้ `Synthesis - ...`
- use cases ใช้ `Use Cases - ...`
- engineering notes ใช้ `Architecture to Code - ...`, `Framework - ...`, `Pattern - ...`, `Recipe - ...`, `Decision - ...`, หรือ `Project Notes - ...`
- standards/workflow ใช้ `Vault Standards - ...` หรือ `Vault Workflow - ...`

### 4. Link Discipline

เมื่อแก้หรือสร้าง note ใหม่ ให้พิจารณาเสมอว่า:
- note นี้ควรชี้กลับ `MOC` ไหน
- มี note ไหนควรลิงก์เข้าหามัน
- ควรอัปเดต `Home` หรือ `index` หรือไม่

### 5. Stable vs Volatile

- `01 Foundations/`, `02 AI Systems/`, `04 Synthesis/`, `05 Use Cases/`, และแนวคิดส่วนใหญ่ใน `06 Engineering/` ควรถือเป็น knowledge ที่ค่อนข้างนิ่ง
- `03 Tools/Claude Code/` ต้องถือเป็น volatile knowledge เป็นหลัก
- ถ้าเป็น note ที่ผูกกับ release, setting, terminal mode, or experimental behavior ให้ติดป้ายหรือบอกให้ชัดว่า `version-sensitive`

---

## Ingest Workflow

เมื่อผู้ใช้นำ source ใหม่เข้ามา ให้ agent ทำตามลำดับนี้:

1. ระบุว่า source อยู่ใน `00 Raw Sources/` แล้วหรือยัง
2. อ่าน source และยืนยัน scope กับผู้ใช้เมื่อจำเป็น
3. ระบุว่า source นี้เกี่ยวกับหมวดใดใน wiki
4. สร้างหรืออัปเดต note ปลายทางที่เกี่ยวข้อง
5. เติม `source:` ให้ note ที่ถูกแตะ
6. เพิ่ม cross-links ไปยัง MOC, synthesis, glossary, หรือ use cases ที่เกี่ยวข้อง
7. ถ้าสร้างหัวข้อใหม่ที่ยังไม่มี hub ให้สร้าง MOC ก่อน แล้วค่อยแตก note ย่อย

หลักการ ingest:
- ให้ความสำคัญกับการบูรณาการเข้ากับของเดิมมากกว่าการสร้าง note ใหม่พร่ำเพรื่อ
- ถ้าเนื้อหาซ้ำกับ note เดิม ให้ merge เข้า note เดิมก่อน
- ถ้าความรู้ใหม่เปลี่ยนข้อสรุปเก่า ให้แก้ note เดิมและระบุความเปลี่ยนแปลงอย่างชัดเจน

---

## Query And File-Back Workflow

เมื่อผู้ใช้ถามคำถาม:

1. เริ่มจาก `index.md` หรือ MOC ที่เกี่ยวข้อง
2. อ่าน note ที่เกี่ยวข้องจริง
3. ตอบจาก wiki ก่อน ถ้าโจทย์ไม่ต้องการข้อมูลภายนอกใหม่
4. ถ้าคำตอบที่เกิดขึ้นมีคุณค่าเชิงความรู้ระยะยาว ให้เสนอหรือสร้าง note ใหม่แบบ file-back

สิ่งที่ควร file-back:
- comparison ที่ใช้ซ้ำได้
- synthesis ใหม่ที่เชื่อมหลายหมวด
- decision framework
- glossary entries ใหม่
- use case ที่ตอบโจทย์ใช้งานจริง

สิ่งที่ไม่ควร file-back ทุกครั้ง:
- คำตอบชั่วคราวที่ไม่มีมูลค่าระยะยาว
- ข้อความที่ยังดิบหรือยังไม่ผ่านการจัดโครง

---

## Lint Workflow

เมื่อผู้ใช้ขอให้ health-check หรือตรวจ wiki ให้ตรวจอย่างน้อย:

- broken links
- frontmatter ที่ผิดรูป
- note ที่ไม่มี `parent_note`
- orphan pages ที่ไม่มี inbound links หรือไม่มี MOC รองรับ
- หัวข้อสำคัญที่ถูกกล่าวถึงหลายครั้งแต่ยังไม่มี note กลาง
- section ภาษา/label ที่ไม่สม่ำเสมอ
- claim ที่ดูแรงเกิน source ใน note ที่เน้น official references

หลักการ lint:
- findings มาก่อน summary
- ถ้าไม่มีปัญหาใหญ่ ให้บอกตรง ๆ ว่าไม่พบ findings
- ถ้าเป็นเพียง style issue ให้แยกจาก structural issue

---

## Writing Standards

### ภาษา

- ใช้ภาษาไทยเป็นหลัก
- คงศัพท์เทคนิคอังกฤษที่แปลแล้วจะเพี้ยน เช่น `context window`, `prompt caching`, `RAG`, `tool calling`
- ลดคำอังกฤษเชิง label/presentation ที่ไม่จำเป็น
- ทำ capitalization ให้คงที่ทั้งหมวด

### Sources

- ถ้าผู้ใช้กำชับเรื่องความน่าเชื่อถือ ให้ใช้เฉพาะ official docs, primary sources, หรือบริษัทเทคชั้นนำที่เกี่ยวข้อง
- อย่ามโน claim เพิ่มเอง
- ถ้ามีส่วนที่เป็น inference เชิงสถาปัตย์ ให้ระบุให้ชัดว่าเป็น `architectural inference` หรือ `design inference`

### Diagrams

- หมวดที่เป็น architecture, loops, workflows, หรือ comparisons ควรพิจารณาใช้ Mermaid
- Mermaid ควรช่วยให้เข้าใจโครง ไม่ใช่เพิ่มเพราะสวยงามอย่างเดียว

---

## When To Create New Pages

สร้าง page ใหม่เมื่อ:
- เป็นหัวข้อแกนที่ถูกอ้างถึงข้ามหลายหน้า
- เป็น concept ที่ผู้ใช้น่าจะกลับมาใช้อีก
- เป็น hub ใหม่ เช่น MOC, synthesis, glossary, use case

ไม่ควรสร้าง page ใหม่เมื่อ:
- เนื้อหาสามารถ merge เข้า note เดิมได้ชัดเจน
- เป็นเพียงตัวอย่างย่อยที่ไม่คุ้มกับการแยก page
- ยังไม่ชัดว่าหัวข้อนั้นมีน้ำหนักพอ

---

## Operational Priorities

เวลาทำงานกับ vault นี้ ให้เรียงลำดับความสำคัญแบบนี้:

1. ความถูกต้องของเนื้อหา
2. ความชัดของโครงสร้างและชั้นข้อมูล
3. cross-links และ navigation
4. ความสม่ำเสมอของ metadata
5. ความสวยงามของสำนวน

---

## Output Expectations

เมื่อ agent แก้ vault:
- บอกสั้น ๆ ว่าเพิ่มหรือปรับอะไร
- ถ้า relevant ให้ชี้ไฟล์หลักที่เปลี่ยน
- ถ้าตรวจแล้วไม่พบปัญหา ให้บอกตรง ๆ
- ถ้ามีความเสี่ยงคงค้าง เช่นยังไม่ได้ verify จาก source หรือยังไม่ทดสอบ UI จริง ให้บอกไว้สั้น ๆ

---

## Related Docs

- [[Home]]
- [[index]]
- [[00 Raw Sources/Raw Sources - MOC|Raw Sources - MOC]]
- [[Vault Standards - Properties]]
- [[Vault Standards - Note Lifecycle]]
- [[Vault Workflow - Capture to Evergreen]]
