---
tags:
  - engineering
  - recipes
  - framework
type: note
status: evergreen
source: ""
parent_note: "[[06 Engineering/Recipes/Recipes - MOC]]"
---

# Recipe - Add a New Framework Note

recipe สั้น ๆ สำหรับสร้าง note ของ framework ใหม่ใน vault นี้

---

## Steps

1. ดูว่า framework นั้นเป็น concept กลางหรือ ecosystem-specific
2. ถ้าเป็น ecosystem-specific ให้เก็บไว้ใน `06 Engineering/Frameworks/`
3. ตั้งชื่อไฟล์เป็น `Framework - <Name>.md`
4. ใส่ `source:` ที่อ้าง official docs ของ framework นั้น
5. เพิ่ม `parent_note:` ให้ชี้ไป `Frameworks - MOC`
6. ถ้าความรู้ยังเป็น high-level ให้เก็บเป็น summary + scope + related notes
7. ถ้าข้อมูลเปลี่ยนตาม release ให้ระบุว่าเป็น version-sensitive

## Checklist

- มี MOC parent แล้ว
- ลิงก์กลับไป note concept ที่เกี่ยวข้อง
- ไม่ปนกับ architecture กลางถ้าเนื้อหาเป็น vendor-specific

