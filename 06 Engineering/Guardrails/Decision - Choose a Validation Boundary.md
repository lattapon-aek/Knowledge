---
tags:
  - engineering
  - guardrails
  - decision
type: note
status: evergreen
source: "vault-local engineering"
parent_note: "[[06 Engineering/Guardrails/Guardrails - MOC]]"
---

# Decision - Choose a Validation Boundary

decision note สำหรับกำหนดว่าจะ validate อะไร ที่ชั้นไหน ก่อนหรือหลัง action

---

## Validation Boundary Decision Flow

```mermaid
flowchart TD
    A["Output or Action"] --> B{"Can invalid output cause side effects?"}
    B -->|yes| C["Validate before action"]
    B -->|no| D{"Is output structured?"}

    C --> E{"Can rule be expressed as schema?"}
    E -->|yes| F["Schema validation"]
    E -->|no| G["Policy / semantic validation"]

    D -->|yes| F
    D -->|no| H{"Risk requires review?"}
    H -->|yes| I["Human review gate"]
    H -->|no| J["Prompt-level constraint + monitoring"]

    F --> K["Retry / repair on failure"]
    G --> L["Reject / fallback on policy failure"]
    I --> M["Approve / reject"]
    J --> N["Log and sample failures"]
```

boundary ที่สำคัญที่สุดคือก่อน side effect ถ้าการกระทำเปลี่ยนข้อมูล เรียก tool สำคัญ หรือส่งข้อมูลออกนอก scope ต้อง validate ก่อน action เสมอ ไม่ใช่หลังจากเกิดผลแล้ว.

---

## Context

- output มีโครงสร้างชัดแค่ไหน
- invalid output เสียหายระดับใด
- validation ควรเกิดก่อน side effects หรือหลัง

## Options

- prompt-level validation
- schema validation
- policy validation
- human review gate

## Criteria

- safety
- reliability
- friction
- automation level

## Decision

บันทึก boundary ที่เลือก

## Consequences

- latency
- failure handling
- user experience
