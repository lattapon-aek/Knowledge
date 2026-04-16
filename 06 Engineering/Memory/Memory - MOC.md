---
tags:
  - engineering
  - memory
  - moc
type: moc
status: evergreen
source: ""
parent_note: "[[06 Engineering/Engineering - MOC]]"
---

# Memory - MOC

implementation layer สำหรับ memory stores, retrieval policies, personalization hooks, และ persistence decisions

---

## Notes Map

- [[06 Engineering/Memory/Recipe - Add a Memory Layer|Add a Memory Layer]]

---

## Related Hubs

- [[02 AI Systems/Memory Systems/Memory Systems - MOC|Memory Systems - MOC]]
- [[02 AI Systems/Agent Frameworks/Core/03 - State and Memory|Agent Frameworks - State and Memory]]
- [[04 Synthesis/Synthesis - Memory in Agents|Synthesis - Memory in Agents]]
- [[06 Engineering/README|Engineering - README]]

---

## Use This Layer When

- ต้องเก็บข้อมูลข้าม session หรือข้าม workflow
- ต้องแยก transient state ออกจาก persistent memory
- ต้องออกแบบ read/write policy สำหรับ memory
