---
tags:
  - engineering
  - patterns
  - multi-agent
  - messaging
  - communication
  - version-sensitive
  - derived
type: note
status: evergreen
source: "https://www.digitalocean.com/community/tutorials/single-to-multi-agent-infrastructure · https://microsoft.github.io/autogen/stable/user-guide/core-user-guide/design-patterns/group-chat.html · https://docs.crewai.com/en/concepts/flows"
parent_note: "[[06 Engineering/Patterns/Patterns - MOC]]"
---

# Pattern - Sync vs Async Agent Communication

## ภาพรวม

การสื่อสารระหว่าง agent เป็นเรื่องของ design choice ไม่ใช่รายละเอียดปลายทางของการ implement ใช้ synchronous communication เมื่ออยากได้ ordering ที่เข้มและ control flow ที่ง่ายกว่า ใช้ asynchronous communication เมื่ออยากได้ decoupling, retries, และ throughput ที่ดีกว่า

---

## การสื่อสารแบบ Synchronous

ใช้เมื่อ:
- caller ต้องรอคำตอบก่อนเดินต่อ
- ordering สำคัญ
- flow สั้นและ debug ง่าย
- อยากได้ ownership และ failure visibility ที่ง่ายกว่า

ลักษณะ:
- request/response
- coupling แน่นกว่า
- conceptual overhead ต่ำกว่า
- reason ได้ง่ายกว่าใน pipeline ขนาดเล็ก

---

## การสื่อสารแบบ Asynchronous

ใช้เมื่อ:
- agent ทำงานอิสระกันได้
- ระบบต้องการ decoupling
- retries และ buffering สำคัญ
- คาดว่ามี burst หรือ task ที่รันนาน

ลักษณะ:
- queue / pub-sub / topic-based
- แยก producer กับ consumer ได้ดีกว่า
- ต้องมีวินัยด้าน infrastructure มากกว่า
- ต้องมี retry, backpressure, และ dead-letter handling

---

## เมื่อควรเลือก Sync

- orchestrator เรียก helper agent
- handoff ต้องการ latency ต่ำ
- sequencing เข้ม
- มีจำนวน agent ไม่มาก

## เมื่อควรเลือก Async

- เก็บข้อมูลก่อนแล้วค่อยวิเคราะห์ทีหลัง
- specialist agent ทำงานอิสระกัน
- workflow ที่รันนาน
- ต้องการ throughput สูงหรือรับ burst ได้

---

## หลักออกแบบ

- กำหนด semantics ของ message ก่อนเลือก transport
- ถ้าเป็น async ให้กำหนด idempotency และ retry policy ไว้ตั้งแต่ต้น
- ถ้ามีหลาย agent แชร์ topic เดียวกัน ให้กำหนด ownership และ namespace ให้ชัด
- ทำ payload ให้เล็กพอเพื่อไม่ให้ context บวม
- อย่าเลือก async แค่เพราะฟังดู scale ได้กว่า

---

## Failure Modes ที่พบบ่อย

- มอง queue เป็นยาวิเศษสำหรับ orchestration ที่ไม่ดี
- ปล่อยให้ synchronous call chain block ทั้งที่ควรเป็น async
- trace หายว่าใครส่งอะไรและทำไม
- งานซ้ำเพราะยังไม่ได้กำหนด idempotency

---

## ลิงก์ที่เกี่ยวข้อง

- [[04 Synthesis/Bridge/Synthesis - Single to Multi-Agent Infrastructure]]
- [[06 Engineering/Architecture to Code/Architecture - Multi-Agent Infrastructure]]
- [[06 Engineering/Patterns/Pattern - Retry and Backoff]]
- [[02 AI Systems/Agent Frameworks/Core/04 - Tool Orchestration]]
- [[02 AI Systems/Agent Frameworks/Core/07 - Checkpointing and Resumability]]
