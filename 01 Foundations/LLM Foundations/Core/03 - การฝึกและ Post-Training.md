---
tags:
  - llm
  - training
  - rlhf
  - alignment
  - pretraining
type: note
status: evergreen
source: "OpenAI, Google Research, Google DeepMind, Anthropic"
parent_note: "[[LLM Foundations - MOC]]"
---

# การฝึกและ Post-Training

---

## ขอบเขตของโน้ตนี้

โน้ตนี้ตอบคำถามว่า:
- โมเดลถูกฝึกตั้งแต่ต้นอย่างไร
- ทำไม **base model** ถึงยังไม่ใช่ assistant ที่ทำตามคำสั่งได้ดี
- **post-training** เปลี่ยนพฤติกรรมโมเดลอย่างไร

โน้ตนี้จะเน้น **training lifecycle** เป็นหลัก  
ส่วนเรื่องความต่างระหว่าง **base model / instruction model / chat model** จะไปลงลึกต่อใน [[08 - Data, Pretraining และ Model Modes]]

---

## ภาพรวมวงจรชีวิตของ LLM

```mermaid
flowchart LR
    A["Raw data"] --> B["Cleaning / filtering / deduplication"]
    B --> C["Tokenizer + data pipeline"]
    C --> D["Pretraining"]
    D --> E["Supervised fine-tuning / instruction tuning"]
    E --> F["Preference alignment<br/>RLHF / RLAIF"]
    F --> G["Evaluation + red teaming"]
    G --> H["Deployment"]
    H --> I["Feedback / iteration"]
    I --> E
```

แนวคิดหลัก:
- **Pretraining** สร้างความสามารถทั่วไปของโมเดล
- **Post-training** ปรับพฤติกรรมให้ตอบในรูปแบบที่ผู้ใช้ต้องการมากขึ้น
- หลัง deploy แล้วระบบจริงยังต้องวนกลับมาเก็บ feedback, eval, และปรับ pipeline ต่อ

---

## Pretraining คืออะไร

Pretraining คือการฝึกโมเดลจากค่าน้ำหนักเริ่มต้นบนข้อมูลมหาศาล เพื่อให้โมเดลเรียนรู้ pattern ของภาษาและข้อมูลที่พบใน training distribution

สำหรับโมเดลตระกูล GPT แนวคิดหลักคือ:
- รับลำดับ token ก่อนหน้า
- ทำนาย token ถัดไป
- ปรับ weights เพื่อลด prediction error

```mermaid
flowchart LR
    A["Text corpus"] --> B["Tokenization"]
    B --> C["Token sequence"]
    C --> D["Predict next token"]
    D --> E["Loss"]
    E --> F["Update weights"]
```

สิ่งที่ pretraining มักให้:
- pattern completion
- syntax และ semantic regularities
- ความสามารถ general-purpose บางส่วน
- พื้นฐานสำหรับ few-shot / in-context behavior ในภายหลัง

สิ่งที่ pretraining ไม่ได้รับประกัน:
- การทำตาม intent ของผู้ใช้
- การปฏิเสธอย่างเหมาะสม
- factuality
- safety behavior

---

## อย่าสับสน: Pretraining กับ Fine-tuning

| แนวคิด | จุดประสงค์ |
|---|---|
| **Pretraining** | ฝึกบนข้อมูลปริมาณมากเพื่อสร้าง general language model |
| **Fine-tuning** | ปรับโมเดลต่อบนข้อมูลเฉพาะงานหรือเฉพาะพฤติกรรม |

Transfer learning สำคัญตรงที่:
- ไม่ต้องฝึกจากศูนย์ทุกครั้ง
- ใช้ data และ compute น้อยกว่าการ pretrain มาก
- ทำให้ pretrained checkpoint กลายเป็นฐานสำคัญของงาน downstream

---

## Instruction Tuning คืออะไร

Google Research อธิบายว่า **instruction tuning** คือการ fine-tune โมเดลบนชุดข้อมูลที่งานต่าง ๆ ถูกเขียนให้อยู่ในรูปคำสั่งธรรมชาติ ทำให้โมเดล generalize ไปยัง instructions ใหม่ได้ดีขึ้น

สรุปสั้นที่สุด:

```text
pretraining         -> โมเดลเรียนรู้ continuation ของภาษา
instruction tuning  -> โมเดลเรียนรู้รูปแบบ "ผู้ใช้ขออะไร -> ควรตอบอย่างไร"
```

```mermaid
flowchart TD
    A["Pretrained model"] --> B["Instruction datasets"]
    B --> C["Input: natural-language instruction"]
    C --> D["Target: desired response"]
    D --> E["Instruction-tuned model"]
```

ผลที่มักเห็น:
- zero-shot performance ดีขึ้น
- few-shot prompting ใช้ง่ายขึ้น
- พฤติกรรมใกล้ assistant มากขึ้น

ข้อสำคัญ:
- instruction tuning ไม่ได้แปลว่าโมเดล "รู้จริง" มากขึ้นโดยอัตโนมัติ
- มันเปลี่ยนรูปแบบการตอบและการตีความงาน มากกว่าการใส่ knowledge ใหม่แบบตรง ๆ

---

## RLHF คืออะไร

OpenAI อธิบาย **RLHF (Reinforcement Learning from Human Feedback)** เป็นกระบวนการใช้ feedback ของมนุษย์เพื่อปรับโมเดลให้ตอบได้ helpful, truthful, และ less toxic มากขึ้น

ลำดับงานระดับสูง:
1. เก็บตัวอย่างคำตอบที่มนุษย์อยากได้
2. ทำ **Supervised Fine-Tuning (SFT)** ให้โมเดลตอบตามตัวอย่าง
3. สร้างคำตอบหลายแบบจากโมเดล
4. ให้มนุษย์จัดอันดับหรือเปรียบเทียบคำตอบ
5. ฝึก **reward model** จาก preference data
6. ใช้ reinforcement learning ปรับ policy ให้ได้ reward สูงขึ้น

```mermaid
flowchart TD
    A["Pretrained model"] --> B["Human demonstrations"]
    B --> C["Supervised fine-tuning"]
    C --> D["Candidate outputs"]
    D --> E["Human preference comparisons"]
    E --> F["Reward model"]
    F --> G["RL optimization"]
    G --> H["Aligned assistant"]
```

สิ่งที่ RLHF ทำได้ดี:
- ปรับพฤติกรรมให้ตอบตาม user intent มากขึ้น
- ลดคำตอบที่ไม่ helpful หรือไม่ปลอดภัยบางแบบ
- ทำให้ output style เสถียรกว่า base model

สิ่งที่ RLHF ไม่ได้รับประกัน:
- factual correctness
- elimination ของ hallucination
- alignment ที่สมบูรณ์

---

## RLAIF และ Constitutional AI

Anthropic เสนออีกแนวทางคือ **Constitutional AI** ซึ่งใช้ชุดหลักการหรือ constitution มากำกับการ critique และ revise คำตอบของโมเดล แล้วจึงใช้ preference optimization ต่อ

แนวคิดหลักมี 2 ช่วง:
- **Supervised phase**: โมเดลวิจารณ์และแก้คำตอบของตัวเองตามหลักการ
- **Preference / RL phase**: ใช้ AI feedback เป็นส่วนหนึ่งของ preference signal แทนการพึ่งมนุษย์ทุกขั้น

สิ่งที่ควรเข้าใจ:
- RLHF = preference signal มาจากมนุษย์เป็นหลัก
- RLAIF / Constitutional AI = preference signal บางส่วนมาจาก AI ที่ถูกกำกับด้วยหลักการ

---

## คุณภาพข้อมูลฝึกสำคัญอย่างไร

ทั้ง OpenAI, Google, DeepMind, และ Hugging Face ล้วนสอดคล้องกันว่า model quality ไม่ได้ขึ้นกับ parameter count อย่างเดียว แต่ขึ้นกับ data pipeline อย่างมาก

ตัวแปรสำคัญ:
- **data quality**
- **deduplication**
- **mixture of domains**
- **language coverage**
- **filtering and safety processing**
- **contamination risk**

สรุปง่าย ๆ:
- ข้อมูลมากแต่สกปรก อาจทำให้โมเดลจำ pattern ที่ไม่ต้องการ
- ข้อมูลสะอาดแต่แคบเกินไป อาจทำให้ generalization แย่
- data mixture มีผลต่อ behavior พอ ๆ กับ architecture ในหลายกรณี

---

## Compute-Optimal Training และ Chinchilla

DeepMind แสดงว่า ภายใต้ compute budget เดียวกัน โมเดลจำนวนมากในยุคก่อนหน้านั้นมีแนวโน้ม **undertrained** คือมีพารามิเตอร์เยอะ แต่ใช้ training tokens น้อยเกินไป

ข้อสรุปสำคัญของ Chinchilla:
- การเพิ่ม model size อย่างเดียวไม่พอ
- จำนวน training tokens ต้องขยายตามอย่างเหมาะสม
- บางกรณีโมเดลที่เล็กลง แต่ฝึกบนข้อมูลมากขึ้น จะดีกว่าโมเดลที่ใหญ่กว่าแต่ข้อมูลน้อยกว่า

```mermaid
flowchart TD
    A["Compute budget"] --> B["Model size"]
    A --> C["Training tokens"]
    A --> D["Training steps"]
    B --> E["Final capability"]
    C --> E
    D --> E
```

Mental model:
- อย่าดูแค่ `parameters`
- ต้องมอง `parameters + data + compute` เป็นชุดเดียว

---

## ข้อจำกัดของ Post-Training

Post-training ช่วยมาก แต่มี trade-off จริง:
- โมเดลอาจ helpful ขึ้น แต่ยัง hallucinate ได้
- โมเดลอาจปลอดภัยขึ้น แต่ตอบแคบลง
- reward model อาจถูก optimize เกินจนเกิด reward hacking
- การทำตามคำสั่งได้ดี ไม่ได้แปลว่าโมเดลมี grounded knowledge ดีขึ้นเสมอไป

---

## อย่าสับสนกับ 3 คู่หลัก

### 1. Pretraining vs Post-training
- **Pretraining** สร้างความสามารถกว้าง
- **Post-training** ปรับพฤติกรรมการตอบ

### 2. SFT vs Instruction Tuning
- **SFT** เป็นคำกว้างสำหรับ supervised fine-tuning
- **Instruction tuning** คือ SFT แบบหนึ่งที่ใช้ instruction-response pairs หลายงาน

### 3. Alignment vs Factuality
- **Alignment** = ตอบตาม intent และ policy ได้ดีขึ้น
- **Factuality** = ข้อเท็จจริงถูกต้อง
- สองอย่างนี้เกี่ยวข้องกัน แต่ไม่ใช่เรื่องเดียวกัน

---

## Mental Model

```text
Pretraining   = สร้าง engine ของภาษา
Instruction tuning = สอนให้รับงานในรูปคำสั่ง
Preference alignment = ปรับพฤติกรรมให้ตอบแบบ assistant มากขึ้น
```

---

## Official References

- OpenAI, Language models are few-shot learners  
  https://openai.com/index/language-models-are-few-shot-learners/
- OpenAI, Aligning language models to follow instructions  
  https://openai.com/index/instruction-following/
- OpenAI paper, Training language models to follow instructions with human feedback  
  https://cdn.openai.com/papers/Training_language_models_to_follow_instructions_with_human_feedback.pdf
- Google Research, Introducing FLAN  
  https://research.google/blog/introducing-flan-more-generalizable-language-models-with-instruction-fine-tuning/
- Google Research, The Flan Collection  
  https://research.google/pubs/the-flan-collection-designing-data-and-methods-for-effective-instruction-tuning/
- Google DeepMind, An empirical analysis of compute-optimal large language model training  
  https://deepmind.google/en/blog/an-empirical-analysis-of-compute-optimal-large-language-model-training/
- Anthropic, Constitutional AI  
  https://www.anthropic.com/news/constitutional-ai-harmlessness-from-ai-feedback

---

## ดูต่อ

- [[08 - Data, Pretraining และ Model Modes]] — ความต่างระหว่าง base model, instruction model, chat model
- [[04 - Inference, Context และ RAG]] — หลังฝึกเสร็จแล้ว runtime ทำงานอย่างไร
- [[05 - ข้อจำกัดและการประเมินผล LLM]]
- [[04 Synthesis/Synthesis - Prompting vs Fine-tuning vs RAG]] — เปรียบเทียบว่าเมื่อไรควรแก้ที่ prompt, RAG, หรือ fine-tuning
- [[LLM Foundations - MOC]]
