---
tags:
  - context
  - moc
  - llm
type: moc
status: evergreen
source: ""
parent_note: "[[Home]]"
---
# Context Windows — Map of Content

> แหล่งความรู้รวมทุกหัวข้อเกี่ยวกับ `context windows` ในการใช้งาน LLM จริง
> 
> **Sources**: Anthropic Docs · Google Caching API · RoPE Paper · Position Interpolation Paper · Model Cards

หมวดนี้เป็น canonical home ของ context budget, context rot, prompt caching, long-context trade-offs, และ context engineering  
โน้ต `01 Foundations/Prompt Engineering/13 - Messages, System Prompt และ Chat Templates` ใช้เป็น runtime bridge เท่านั้น ไม่ใช่ที่อธิบาย context management หลัก

---

## Notes

| # | Note | เนื้อหาหลัก |
|---|---|---|
| 01 | [[01 - Context Window คืออะไร]] | นิยาม, การนับ tokens, context budget, context rot, model sizes, attention cost |
| 02 | [[02 - การบริหารและ Context Engineering]] | การจัด prompt, การนับ token, การจัดการเมื่อข้อมูลเกิน, การเลือก RAG vs long context, testing และ monitoring |
| 03 | [[03 - Prompt Caching]] | วิธีทำงานของ prompt caching, ราคาของ Anthropic, การคำนวณต้นทุนและ ROI, code examples, แนวปฏิบัติที่ดี |

---

## ความสัมพันธ์กับ Topic อื่น

- [[01 Foundations/Tokenizer in AI/Tokenizer in AI - MOC|Tokenizer in AI]] — token counting ผูกกับ tokenizer โดยตรง
- [[01 Foundations/LLM Foundations/LLM Foundations - MOC|LLM Foundations]] — context window × attention mechanism = ข้อจำกัดเชิงคำนวณ
- [[01 Foundations/LLM Foundations/08 - Data, Pretraining และ Model Modes|Data, Pretraining และ Model Modes]] — weights vs context vs external memory
- [[01 Foundations/LLM Foundations/04 - Inference, Context และ RAG|Inference, Context และ RAG]] — RAG เป็นทางเลือกเมื่อ context เริ่มตึงหรือไม่อยากใส่ข้อมูลทั้งหมด
- [[01 Foundations/LLM Foundations/09 - Serving Metrics และระบบ Production LLM|Serving Metrics และระบบ Production LLM]] — caching, latency, และ trade-offs ของ context length
- [[02 AI Systems/RAG/RAG - MOC|RAG]] — chunking strategy มีผลต่อปริมาณข้อมูลที่เอาเข้า context ได้จริง
- [[01 Foundations/Prompt Engineering/13 - Messages, System Prompt และ Chat Templates|13 - Messages, System Prompt และ Chat Templates]] — bridge note สำหรับ runtime context/message layer
- [[02 AI Systems/AI Agent Fundamentals/AI Agent Fundamentals - MOC|AI Agent Fundamentals]] — multi-turn agents ทำให้ปัญหาการสะสมของ context ชัดขึ้น
- [[06 Engineering/README]] — implementation layer สำหรับ cache, prompt shaping, retrieval recipes, และ runtime decisions
- [[Knowledge Topic Registry]]

---

## หลักคิดสรุป

```
context window  = working memory ระหว่างการตอบ
input + output  = ใช้งบ context ร่วมกัน
context rot     = context ยาวมาก → recall ลดลง
prompt caching  = reuse prefix computation เพื่อลด cost/latency
RAG             = เลือกเฉพาะข้อมูลที่เกี่ยวข้องมาป้อน
```

---

## เส้นทางอ่านต่อที่แนะนำ

- ถ้ายังสับสนว่า context window ต่างจากความรู้ในโมเดลอย่างไร -> [[01 Foundations/LLM Foundations/08 - Data, Pretraining และ Model Modes|Data, Pretraining และ Model Modes]]
- ถ้าอยากเข้าใจ runtime ของ request -> [[01 Foundations/LLM Foundations/04 - Inference, Context และ RAG|Inference, Context และ RAG]]
- ถ้าอยากเข้าใจผลกระทบต่อ latency และ cost -> [[01 Foundations/LLM Foundations/09 - Serving Metrics และระบบ Production LLM|Serving Metrics และระบบ Production LLM]]
