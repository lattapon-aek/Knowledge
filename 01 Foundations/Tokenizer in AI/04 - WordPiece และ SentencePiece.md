---
tags:
  - tokenizer
  - wordpiece
  - sentencepiece
  - llm
  - nlp
type: note
status: draft
source: "Tokenizer in AI/Tokenizer-Knowledge-Base.md — ส่วนที่ 6.3–6.5, 11"
parent_note: "[[Tokenizer in AI - MOC]]"
---
# WordPiece และ SentencePiece

## WordPiece

Google ใช้ WordPiece กับ BERT และโมเดลตระกูล BERT อีกหลายตัว (Google Research, 2019)

### ลักษณะสำคัญ

- เป็น subword tokenizer ที่ **คล้าย BPE แต่มีความต่างที่สำคัญ**
- ใช้ marker `##` บอกว่า token นั้นเป็น **continuing subword** (ส่วนต่อท้ายของคำ)

```
transformer → transform + ##er
```

### ความต่างเชิงเทคนิค: WordPiece vs BPE

| | BPE | WordPiece |
|---|---|---|
| **วิธีเลือกคู่ที่ merge** | ความถี่สูงสุด (frequency-based) | Likelihood ของ training data (likelihood-based) |
| **สูตร score** | `frequency(pair)` | `frequency(pair) / (frequency(left) × frequency(right))` |
| **ตัวอย่าง** | merge ("u","g") ถ้าพบ 20 ครั้ง | merge ("g","s") ถ้า score = 0.050 สูงกว่า |

**ตัวอย่างประกอบ:**
```
Pair: ("u", "g") appears 20 times
      ("u", "n") appears 16 times
      ("h", "u") appears 15 times
      ("g", "s") appears 5 times

BPE: merge ("u", "g") ← 20 is highest
WordPiece: 
  score("u","g") = 20 / (36 × 20) = 0.028
  score("g","s") = 5 / (20 × 5) = 0.050  ← highest score
  → merge ("g", "s") ← more informative
```

### ข้อควรรู้

- Implementation ต้นฉบับจาก Google ไม่ได้ open-source ออกมาครบถ้วน
- **Hugging Face Transformers** ให้ `BertTokenizer` / `BertTokenizerFast` ที่เข้ากันได้กับ BERT

**โมเดลที่ใช้:** BERT, DistilBERT, Electra, ERNIE

---

## SentencePiece

SentencePiece เป็น tokenizer framework ของ Google ที่ออกแบบให้เป็น **language-independent**

### จุดเด่นสำคัญ

- train ได้จาก raw sentences **โดยไม่ต้อง pre-tokenize** ล่วงหน้า
- รองรับทั้ง **BPE** และ **Unigram language model**
- จัดการ whitespace เป็น "สัญลักษณ์ปกติ" ของระบบ ใช้ `▁` แทน space
- normalization แบบ NFKC
- detokenization ย้อนกลับได้แบบ lossless

```
"Hello world." → "Hello▁world."
→ segmented → IDs
→ decode: แปลง ▁ กลับเป็น space
```

> [!note]
> SentencePiece เก็บข้อมูล whitespace ไว้ ทำให้ detokenize ได้แม่นยำกว่า tokenizer ที่ทิ้งข้อมูล space ไป

### เหมาะกับภาษาที่ไม่มีช่องว่างคั่นคำ

ภาษาอย่าง Chinese, Japanese และ **ภาษาไทย** ที่ whitespace ไม่ได้ทำหน้าที่คั่นคำชัดเจน — SentencePiece มีข้อได้เปรียบมากกว่า tokenizer ที่พึ่ง whitespace เป็นหลัก

**โมเดลที่ใช้:** T5, LLaMA, ALBERT, mBART, XLNet

---

## Unigram (ใช้ร่วมกับ SentencePiece)

### หลักคิดต่างจาก BPE

| | BPE | Unigram |
|---|---|---|
| จุดเริ่มต้น | vocabulary เล็ก | vocabulary ใหญ่ |
| กระบวนการ | merge ให้ใหญ่ขึ้น | ตัดออกจนเหลือขนาดที่ต้องการ |

**โมเดลที่ใช้:** ALBERT, T5, mBART, Big Bird, XLNet

---

## สรุปเปรียบเทียบอัลกอริทึมต่าง ๆ

| Algorithm | แนวคิดหลัก | ใช้ใน | จุดแข็ง | ข้อควรระวัง |
|---|---|---|---|---|
| **BPE** | Merge คู่พบบ่อยซ้ำ ๆ | GPT-2, RoBERTa | Compact, เร็ว | Coverage ขึ้นกับ base symbols |
| **WordPiece** | subword + `##` prefix | BERT, DistilBERT | ใช้จริงกับ BERT | training details ไม่ open-source ครบ |
| **SentencePiece** | train จาก raw text | T5, LLaMA | Multilingual, ไม่ต้อง pre-tokenize | ต้องออกแบบ normalization ระวัง |
| **Unigram** | ตัด vocab จากชุดใหญ่ | ALBERT, XLNet | ยืดหยุ่น probabilistic | ช้ากว่า BPE เล็กน้อย |

## ลิงก์ที่เกี่ยวข้อง

- [[03 - อัลกอริทึม BPE และ Byte-level BPE]]
- [[07 - เปรียบเทียบ Tokenizer รายโมเดล]]
- [[06 - ทำไม Tokenization ถึงสำคัญ]]
