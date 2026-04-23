---
tags:
  - llm
  - pretraining
  - basemodel
  - instructiontuning
  - scaling
  - finetuning
  - emergence
  - chinchilla
  - scaling-laws
type: note
status: evergreen
source: "OpenAI, Google Research, Google DeepMind, Meta AI, Schaeffer et al."
parent_note: "[[LLM Foundations - MOC]]"
---

# Data, Pretraining และ Model Modes

---

## ขอบเขตของโน้ตนี้

โน้ตนี้ไม่ได้ลงลึก pipeline การฝึกทั้งหมด แต่จะตอบว่า:
- training data shape ความสามารถของโมเดลอย่างไร
- pretraining ทำให้เกิด **base model** แบบไหน
- post-training ทำให้เกิด **instruction model / chat model** อย่างไร
- **in-context learning** ต่างจากการเรียนรู้ใน weights อย่างไร

ถ้าต้องการ training lifecycle แบบเต็ม ให้ดู [[03 - การฝึกและ Post-Training]]

---

## Data สำคัญเพราะอะไร

โมเดลไม่ได้เรียน "ความจริงของโลก" แบบตรง ๆ แต่มันเรียน pattern จาก **training distribution** ที่ป้อนให้

องค์ประกอบสำคัญของ data mixture:
- **quantity** — ปริมาณข้อมูล
- **quality** — ความสะอาดและความน่าเชื่อถือ
- **deduplication** — ลดข้อมูลซ้ำที่บิด training signal
- **domain mixture** — web, books, code, math, instruction data
- **language coverage** — ภาษาไหนถูกแทนมากหรือน้อย
- **filtering** — toxicity, low-quality text, policy-violating content

ข้อสรุปเชิงปฏิบัติ:
- training data มีผลต่อความสามารถและพฤติกรรมพร้อมกัน
- โมเดลที่ architecture คล้ายกันอาจ behavior ต่างกันมากเพราะ data mixture ต่างกัน

---

## Pretraining สอนอะไรโมเดล

ในการ pretraining โมเดลจะ optimize objective ของภาษา เช่น next-token prediction สำหรับ GPT-like models

สิ่งที่ถูกเรียนรู้ไม่ใช่ fact database แบบตรงตัว แต่คือ:
- statistical regularities
- linguistic structure
- latent patterns ของข้อมูลที่เจอ
- ความสามารถบางส่วนที่โผล่มาในรูป few-shot / in-context behavior

สิ่งนี้อธิบายได้ว่าทำไม:
- โมเดลตอบได้หลายงาน
- แต่ยังตอบไม่ตรง intent ของผู้ใช้เสมอ

---

## Base Model คืออะไร

**Base model** คือโมเดลที่ผ่าน pretraining แล้ว แต่ยังไม่ได้ถูก post-train ให้ตอบในบทบาท assistant อย่างจริงจัง

ลักษณะทั่วไป:
- เก่ง continuation
- เก่งเติม pattern ให้สมบูรณ์
- อาจตอบแบบไม่ตรง task framing ของผู้ใช้
- อาจทำตาม instruction ได้บ้างจาก pretraining และ scale แต่ยังไม่เสถียร

```mermaid
flowchart LR
    A["Training data"] --> B["Pretraining"]
    B --> C["Base model"]
    C --> D["Strong continuation ability"]
    C --> E["General language patterns"]
    C --> F["Limited instruction-following reliability"]
```

OpenAI อธิบายในงาน InstructGPT ว่า GPT-3 ถูกฝึกให้ทำนาย next word บน Internet text ไม่ได้ถูกฝึกโดยตรงให้ทำสิ่งที่ผู้ใช้ต้องการอย่างปลอดภัยและ helpful

---

## Instruction Model / Chat Model คืออะไร

เมื่อเอา base model ไปผ่าน instruction tuning และ alignment ขั้นต่อมา โมเดลจะเปลี่ยน mode จากการ "เติมข้อความให้ต่อเนื่อง" ไปเป็นการ "รับคำสั่งแล้วตอบในรูปแบบผู้ช่วย"

```mermaid
flowchart LR
    A["Base model"] --> B["Instruction tuning"]
    B --> C["Preference alignment"]
    C --> D["Instruction / chat model"]
```

ผลที่เปลี่ยนชัด:
- ตีความคำสั่งได้ดีขึ้น
- รักษา format คำตอบได้ดีขึ้น
- ปฏิเสธหรือระบุข้อจำกัดได้ดีขึ้นในบางกรณี
- ใช้งานผ่าน chat interface ได้เป็นธรรมชาติมากขึ้น

อย่าสรุปเกินจริง:
- chat model ไม่ได้แปลว่าเก่งกว่า base model ทุก task
- ในบางงานเชิง completion, style transfer, หรือ decoding control บางแบบ base model อาจคาดเดาพฤติกรรมง่ายกว่า

---

## อย่าสับสน: Base Model vs Chat Model

| ประเด็น | Base model | Instruction / chat model |
|---|---|---|
| Training stage | mainly pretraining | pretraining + post-training |
| พฤติกรรมเด่น | continuation | instruction following |
| ความเสถียรต่อ user intent | ต่ำกว่า | สูงกว่า |
| การปฏิเสธ / safety policy | จำกัด | โดยทั่วไปชัดกว่า |
| เหมาะกับ | research, completion-style control, adaptation | assistant UX, API/chat use cases |

---

## Fine-tuning, Instruction Tuning, RLHF ต่างกันอย่างไร

| เทคนิค | ทำอะไร |
|---|---|
| **Fine-tuning** | ปรับโมเดลต่อบน dataset เฉพาะงาน |
| **Instruction tuning** | fine-tune บนหลายงานที่เขียนในรูป instruction |
| **RLHF / preference alignment** | ใช้ preference signal เพื่อปรับ behavior ให้ตรงสิ่งที่ต้องการมากขึ้น |

ความสัมพันธ์:
- instruction tuning เป็น fine-tuning แบบหนึ่ง
- RLHF มักเกิดหลัง SFT / instruction tuning
- ทั้งหมดนี้คือ post-training แต่หน้าที่ไม่เหมือนกัน

---

## In-Context Learning คืออะไร

OpenAI GPT-3 แสดงให้เห็นว่าโมเดลสามารถทำงานใหม่จาก prompt และ examples ได้ โดย **ไม่ต้องอัปเดต weights**

```mermaid
flowchart TD
    A["Weights from training"] --> B["Model capability prior"]
    C["Prompt + examples at runtime"] --> D["Task-specific behavior in this request"]
    B --> E["Final response"]
    D --> E
```

แยกให้ขาด:
- **In-weight learning** — สิ่งที่โมเดลเรียนจาก training
- **In-context learning** — สิ่งที่โมเดลทำได้จากข้อมูลใน prompt ตอน runtime

ข้อสำคัญ:
- in-context learning ไม่ใช่ parameter update
- พอจบ request โมเดลไม่ได้ "จำถาวร" สิ่งนั้นลงใน weights

---

## Weights vs Context vs External Memory

นี่เป็นจุดที่คนมักสับสนมากที่สุด

| สิ่งนี้ | อยู่ที่ไหน | เปลี่ยนเมื่อไร |
|---|---|---|
| **Weights** | อยู่ในพารามิเตอร์ของโมเดล | เปลี่ยนตอน training / fine-tuning |
| **Context** | อยู่ใน prompt ของ request ปัจจุบัน | เปลี่ยนทุก request |
| **External memory / RAG** | อยู่ใน database, search index, documents | ถูกดึงเข้ามาตอน runtime |

สรุป:
- โมเดล "รู้" บางอย่างเพราะอยู่ใน weights
- โมเดล "เห็น" บางอย่างเพราะอยู่ใน context
- โมเดล "เข้าถึง" บางอย่างเพราะระบบ runtime ไปดึงมาให้

---

## Scaling Laws และ Chinchilla

### Kaplan Scaling Laws (OpenAI, 2020)

OpenAI scaling laws ชี้ว่า loss มีความสัมพันธ์แบบ power law กับ:
- model size (N — จำนวน parameters)
- dataset size (D — จำนวน training tokens)
- training compute (C)

ข้อค้นพบสำคัญ:
- loss ลดลงอย่าง **smooth และ predictable** เมื่อเพิ่ม N, D, หรือ C
- ความสัมพันธ์เป็น power law: `L(x) ≈ a · x^(-α) + L∞`
- ภายใต้ compute budget คงที่ Kaplan แนะนำให้เพิ่ม model size มากกว่า data size

### Chinchilla Scaling Laws (DeepMind, 2022)

DeepMind Chinchilla เพิ่มมุมมองที่ท้าทาย Kaplan:
- การเพิ่ม parameters อย่างเดียวไม่พอ
- training tokens ต้องสมดุลกับ model size ภายใต้ compute budget
- อัตราส่วนที่เหมาะสมอยู่ที่ประมาณ **20 tokens ต่อ 1 parameter**
- โมเดลยุคก่อน Chinchilla ส่วนใหญ่ **undertrained** — parameters เยอะแต่ data น้อยเกินไป

```mermaid
flowchart TD
    A["Compute budget C"] --> B["Model size N"]
    A --> C["Training tokens D"]
    B --> D["Kaplan: เน้นเพิ่ม N"]
    C --> E["Chinchilla: N และ D ต้องสมดุล<br/>D ≈ 20 × N"]
    D --> F["Final loss"]
    E --> F
```

ดังนั้นเวลาพูดว่าโมเดล "ใหญ่กว่า":
- ไม่ได้แปลว่า "ดีกว่า" โดยอัตโนมัติ
- ต้องถามต่อว่าใช้ข้อมูลเท่าไร และฝึกนานแค่ไหน

### หลัง Chinchilla: แนวโน้มปัจจุบัน

ในทางปฏิบัติหลังปี 2023 หลายทีมเลือก **overtrain** โมเดลเล็กเกินอัตราส่วน Chinchilla:
- **Llama 2 7B** ฝึกบน 2T tokens (สูงกว่า Chinchilla optimal มาก)
- **Mistral 7B** ฝึกบน data มากกว่า Chinchilla ratio เช่นกัน
- เหตุผล: inference cost สำคัญกว่า training cost ในระยะยาว — โมเดลเล็กที่ฝึกนานกว่าจะถูกกว่าตอน deploy

สรุป: Chinchilla optimal คือ **training-compute optimal** แต่ไม่ใช่ **inference-compute optimal** เสมอไป

---

## Emergence และ Capability Thresholds

### Emergent Capabilities คืออะไร

Emergent capabilities หมายถึงความสามารถที่ **ไม่ปรากฏในโมเดลขนาดเล็ก แต่โผล่ขึ้นมาอย่างกะทันหันเมื่อโมเดลถึงขนาดหนึ่ง**

ตัวอย่างที่มักถูกอ้าง:
- **Chain-of-thought reasoning** — โมเดลเล็กไม่ได้ประโยชน์จาก CoT prompting แต่โมเดลใหญ่ได้
- **Multi-step arithmetic** — accuracy กระโดดขึ้นที่ scale หนึ่ง
- **Code generation** — ความสามารถเพิ่มขึ้นแบบไม่เป็นเส้นตรงกับ scale

```mermaid
flowchart LR
    A["Model scale"] --> B["Loss ลดลง smooth<br/>(power law)"]
    A --> C["บาง capabilities<br/>โผล่แบบ step function"]
    B --> D["Predictable"]
    C --> E["Harder to predict"]
```

### ข้อถกเถียงเรื่อง Emergence

งานวิจัยหลังปี 2023 ตั้งคำถามว่า emergence เป็น **ปรากฏการณ์จริง** หรือเป็น **artifact ของ metric ที่ใช้วัด**:

| มุมมอง | อธิบาย |
|---|---|
| **Emergence เป็นจริง** | บาง capabilities ต้องการ minimum scale จริง ๆ เพราะ task ซับซ้อนเกินกว่า small model จะ represent ได้ |
| **Emergence เป็น metric artifact** | ถ้าเปลี่ยนจาก discrete metric (exact match) เป็น continuous metric (token-level accuracy) การกระโดดจะหายไป — performance จริง ๆ อาจ smooth ตลอด |
| **มุมมองประนีประนอม** | loss ลดลง smooth แต่ downstream task performance อาจมี threshold เพราะ task ต้องการ minimum capability level |

### Capability Prediction

ผลกระทบเชิงปฏิบัติ:
- **scaling laws ทำนาย loss ได้ดี** — loss เป็น smooth power law
- **scaling laws ทำนาย specific capabilities ได้ยาก** — ไม่รู้ว่า capability X จะโผล่ที่ scale ไหน
- ทำให้การตัดสินใจว่า "ต้องโมเดลใหญ่แค่ไหนถึงจะทำ task นี้ได้" ยังเป็นเรื่องที่ต้อง empirical testing

### Signal-to-Noise Ratio (SNR) Framework

งานวิจัยล่าสุดเสนอ framework ที่ใช้ SNR อธิบาย emergence:
- เมื่อ SNR ของ capability signal ผ่าน threshold หนึ่ง capability จะ "โผล่" ขึ้นมา
- ก่อนถึง threshold โมเดลอาจมี signal อยู่แล้วแต่ถูก noise กลบ
- framework นี้ช่วยอธิบายว่าทำไม emergence ดูเหมือน step function ทั้งที่ underlying learning อาจ smooth

---

## Scaling Laws กับการตัดสินใจเชิงปฏิบัติ

| คำถาม | Scaling laws ช่วยได้ไหม |
|---|---|
| โมเดลใหญ่ขึ้นจะ loss ลดลงเท่าไร? | ได้ดี (power law prediction) |
| โมเดลใหญ่ขึ้นจะทำ task X ได้ไหม? | ไม่แน่นอน (emergence unpredictable) |
| ควรเพิ่ม data หรือ parameters? | Chinchilla ให้ guideline แต่ต้องพิจารณา inference cost ด้วย |
| ถึง ceiling แล้วหรือยัง? | ยังไม่ถึง absolute ceiling แต่ diminishing returns ชัดขึ้น |

---

## Mental Model

```text
Data mixture shapes what patterns the model can learn
Pretraining creates a base model
Post-training changes that base model into an assistant-like model
Prompting activates behavior at runtime without changing weights
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
- Google DeepMind, An empirical analysis of compute-optimal large language model training  
  https://deepmind.google/en/blog/an-empirical-analysis-of-compute-optimal-large-language-model-training/
- Kaplan et al., Scaling Laws for Neural Language Models  
  https://arxiv.org/abs/2001.08361
- Hoffmann et al., Training Compute-Optimal Large Language Models (Chinchilla)  
  https://arxiv.org/abs/2203.15556
- Wei et al., Emergent Abilities of Large Language Models  
  https://arxiv.org/abs/2206.07682
- Schaeffer et al., Are Emergent Abilities of Large Language Models a Mirage?  
  https://arxiv.org/abs/2304.15004

---

## ดูต่อ

- [[03 - การฝึกและ Post-Training]] — training lifecycle และ preference alignment
- [[16 - Model Compression และ Inference Optimization]] — quantization, distillation, pruning ที่เกี่ยวข้องกับ model size decisions
- [[04 - Inference, Context และ RAG]] — runtime behavior ของ request
- [[LLM Foundations - MOC]]
