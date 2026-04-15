---
tags:
  - standards
  - properties
  - metadata
type: guide
status: evergreen
source: ""
parent_note: "[[Home]]"
---

# Vault Standards - Properties

## Canonical Properties

vault นี้ใช้ properties หลักชุดเดียว:

- `tags` = หัวข้อหรือคำค้นหลักของโน้ต
- `type` = ประเภทของโน้ต
- `status` = ระดับความสมบูรณ์ของโน้ต
- `source` = แหล่งที่มาของเนื้อหา
- `parent_note` = หน้าแม่หรือ MOC ที่โน้ตนี้สังกัด
- `created` = วันที่สร้างโน้ต
- `updated` = วันที่แก้ล่าสุด

---

## Allowed Values

### `type`

- `home`
- `moc`
- `note`
- `synthesis`
- `guide`
- `glossary`
- `template`

### `status`

- `seed`
- `draft`
- `evergreen`

---

## Usage Rules

- ใช้ `parent_note` แทน `up`
- `source` เก็บเป็น plain string ไม่ใช้ markdown formatting
- ถ้าไม่มีค่า ให้ใช้ `""`
- `tags` ใช้เป็น YAML list
- note ใหม่ทั่วไปเริ่มที่ `type: note` และ `status: draft`
- quick capture ใช้ `status: seed`

---

## Example

```yaml
---
tags:
  - rag
  - retrieval
type: note
status: draft
source: "Article X, section 2"
parent_note: "Parent MOC"
created: "2026-04-12"
updated: ""
---
```

---

## Cross Links

- [[Home]]
- [[Vault Standards - Note Lifecycle]]
- [[_Templates/Standard Note Template|Standard Note Template]]
- [[_Templates/Quick Capture Template|Quick Capture Template]]
