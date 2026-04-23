---
tags:
  - llm
  - ml
  - fundamentals
  - bridge
type: note
status: evergreen
source: "Google ML Crash Course · Microsoft Learn ML Fundamentals · DeepLearning.AI ML Specialization · Stanford CS229 · IBM ML Hub"
parent_note: "[[01 Foundations/LLM Foundations/LLM Foundations - MOC|LLM Foundations - MOC]]"
created: "2026-04-23"
updated: ""
---

# ML Primitives สำหรับ LLM

> bridge note ที่รวม ML fundamentals ที่จำเป็นต่อการเข้าใจ LLM
> ไม่ใช่ canonical home ของ ML — เป็นสะพานเชื่อม ML concepts เข้ากับ LLM notes ที่มีอยู่

---

## ทำไมต้องรู้ ML Primitives

LLM ถูกสร้างบน ML fundamentals — ถ้าไม่เข้าใจ primitives เหล่านี้ จะเข้าใจ LLM training, evaluation, และ optimization ได้แค่ผิวเผิน

---

## 1. Supervised vs Unsupervised vs Reinforcement Learning

| ประเภท | กลไก | เชื่อมกับ LLM |
|---|---|---|
| **Supervised** | เรียนจาก labeled data (input → expected output) | fine-tuning, instruction tuning (input = prompt, output = desired response) |
| **Unsupervised** | เรียนจาก unlabeled data หา patterns เอง | pretraining (next-token prediction ไม่มี explicit labels) |
| **Self-supervised** | สร้าง labels จาก data เอง | LLM pretraining เป็น self-supervised — mask/predict tokens |
| **Reinforcement Learning** | เรียนจาก rewards/penalties | RLHF, DPO — ปรับ model ตาม human preferences |

→ เชื่อมกับ [[01 Foundations/LLM Foundations/Core/03 - การฝึกและ Post-Training|การฝึกและ Post-Training]]

---

## 2. Loss Functions

loss function วัดว่า model ผิดแค่ไหน — เป็นสัญญาณที่ optimizer ใช้ปรับ weights

| Loss Function | ใช้กับ | เชื่อมกับ LLM |
|---|---|---|
| **Cross-entropy** | classification (รวม next-token prediction) | loss หลักของ LLM training — วัดว่า predicted probability distribution ต่างจาก actual token แค่ไหน |
| **MSE** (Mean Squared Error) | regression | ไม่ค่อยใช้ใน LLM โดยตรง แต่ใช้ใน embedding training |
| **Contrastive loss** | similarity learning | ใช้ใน embedding model training (เช่น sentence-transformers) |

**Perplexity** = exp(cross-entropy loss) — metric มาตรฐานสำหรับวัด LLM quality ยิ่งต่ำยิ่งดี

→ เชื่อมกับ [[01 Foundations/LLM Foundations/Core/07 - Logits, Decoding และ Sampling|Logits, Decoding และ Sampling]]

---

## 3. Gradient Descent และ Optimization

model เรียนรู้โดยปรับ weights ตาม gradient ของ loss function:

| Concept | คำอธิบาย |
|---|---|
| **Gradient** | ทิศทางที่ loss เพิ่มขึ้นเร็วที่สุด — ปรับ weights ไปทิศตรงข้าม |
| **Learning rate** | ขนาดของ step ที่ปรับ — ใหญ่เกินจะ overshoot, เล็กเกินจะช้า |
| **SGD** | Stochastic Gradient Descent — ปรับทีละ mini-batch |
| **Adam** | adaptive learning rate per parameter — optimizer มาตรฐานของ LLM training |
| **Learning rate schedule** | ปรับ learning rate ระหว่าง training (warmup → decay) |

→ เชื่อมกับ [[01 Foundations/LLM Foundations/Core/03 - การฝึกและ Post-Training|การฝึกและ Post-Training]]

---

## 4. Overfitting, Underfitting, Regularization

| Concept | คำอธิบาย | เชื่อมกับ LLM |
|---|---|---|
| **Overfitting** | model จำ training data ได้ดีแต่ generalize ไม่ได้ | LLM ที่ train นานเกินบน data ซ้ำ ๆ |
| **Underfitting** | model เรียนไม่พอ | LLM ที่ train ไม่นานพอหรือ model เล็กเกิน |
| **Regularization** | เทคนิคป้องกัน overfitting | dropout, weight decay ใช้ใน LLM training |
| **Data mixture** | สัดส่วนของ data types ใน training | Chinchilla insight: data quantity สำคัญเท่า model size |

→ เชื่อมกับ [[01 Foundations/LLM Foundations/Core/08 - Data, Pretraining และ Model Modes|Data, Pretraining และ Model Modes]]
→ เชื่อมกับ [[01 Foundations/LLM Foundations/Core/05 - ข้อจำกัดและการประเมินผล LLM|ข้อจำกัดและการประเมินผล]]

---

## 5. Bias-Variance Tradeoff

| Concept | คำอธิบาย |
|---|---|
| **Bias** | error จากการ simplify ปัญหามากเกิน (underfitting) |
| **Variance** | error จากการ sensitive ต่อ training data มากเกิน (overfitting) |
| **Tradeoff** | model ที่ดีต้อง balance ทั้งสอง |

ใน LLM: model ใหญ่ขึ้นลด bias แต่อาจเพิ่ม variance ถ้า data ไม่พอ — นี่คือเหตุผลที่ scaling laws สำคัญ

→ เชื่อมกับ [[01 Foundations/LLM Foundations/Core/05 - ข้อจำกัดและการประเมินผล LLM|ข้อจำกัดและการประเมินผล]]

---

## 6. Evaluation Metrics

| Metric | ใช้กับ | เชื่อมกับ LLM |
|---|---|---|
| **Accuracy** | classification ทั่วไป | ใช้ใน benchmark tasks |
| **Precision** | สัดส่วน positive predictions ที่ถูก | ใช้ใน classification tasks, retrieval |
| **Recall** | สัดส่วน actual positives ที่จับได้ | ใช้ใน retrieval, safety detection |
| **F1** | harmonic mean ของ precision + recall | balanced metric |
| **Perplexity** | วัด language model quality | metric มาตรฐานของ LLM |
| **BLEU / ROUGE** | วัด text generation quality | ใช้ใน translation, summarization |

→ เชื่อมกับ [[01 Foundations/LLM Foundations/Core/13 - Evaluation Foundations|Evaluation Foundations]]
→ เชื่อมกับ [[02 AI Systems/Evals/Evals - MOC|Evals - MOC]]

---

## 7. Neural Network Basics

| Concept | คำอธิบาย | เชื่อมกับ LLM |
|---|---|---|
| **Layer** | ชั้นของ neurons ที่ transform input | Transformer มีหลาย layers (attention + FFN) |
| **Activation function** | non-linear function หลัง linear transform | GELU ใช้ใน modern LLMs |
| **Backpropagation** | คำนวณ gradients ย้อนกลับจาก loss | กลไกหลักของ training |
| **Parameters / Weights** | ค่าที่ model เรียนรู้ | LLM มี billions of parameters |

→ เชื่อมกับ [[01 Foundations/LLM Foundations/Core/02 - สถาปัตยกรรม Transformer|สถาปัตยกรรม Transformer]]

---

## 8. Classification vs Regression

| ประเภท | Output | ตัวอย่าง LLM |
|---|---|---|
| **Classification** | discrete categories | next-token prediction (เลือก 1 token จาก vocabulary) |
| **Regression** | continuous values | embedding similarity scores |

LLM ที่ core เป็น **classification problem** — ทุก token ที่ generate คือการเลือก 1 จาก vocabulary ทั้งหมด

→ เชื่อมกับ [[01 Foundations/LLM Foundations/Core/07 - Logits, Decoding และ Sampling|Logits, Decoding และ Sampling]]

---

## 9. Feature Engineering → Embeddings

| Concept | คำอธิบาย |
|---|---|
| **Feature engineering** | การเลือก/สร้าง features จาก raw data สำหรับ model | 
| **Embeddings** | learned features ที่ model สร้างเอง |

ใน classical ML ต้อง engineer features ด้วยมือ ใน LLM model เรียนรู้ representations (embeddings) เองจาก data — embeddings คือ automated feature engineering

→ เชื่อมกับ [[01 Foundations/LLM Foundations/Core/10 - Embeddings และ Semantic Similarity|Embeddings และ Semantic Similarity]]
→ เชื่อมกับ [[01 Foundations/LLM Foundations/Core/14 - Vector Representations และ Similarity Search|Vector Representations]]

---

## ความสัมพันธ์กับโน้ตอื่น

- [[01 Foundations/LLM Foundations/Core/02 - สถาปัตยกรรม Transformer|Transformer]] — neural network architecture ของ LLM
- [[01 Foundations/LLM Foundations/Core/03 - การฝึกและ Post-Training|Training]] — supervised/unsupervised/RL ใน LLM context
- [[01 Foundations/LLM Foundations/Core/05 - ข้อจำกัดและการประเมินผล LLM|ข้อจำกัด]] — overfitting, bias, evaluation
- [[01 Foundations/LLM Foundations/Core/07 - Logits, Decoding และ Sampling|Logits]] — loss functions, classification
- [[01 Foundations/LLM Foundations/Core/08 - Data, Pretraining และ Model Modes|Data]] — data mixture, scaling
- [[01 Foundations/LLM Foundations/Core/10 - Embeddings และ Semantic Similarity|Embeddings]] — learned features
- [[01 Foundations/LLM Foundations/Core/13 - Evaluation Foundations|Evaluation]] — metrics
- [[02 AI Systems/Evals/Evals - MOC|Evals - MOC]] — system-level evaluation
- [[01 Foundations/LLM Foundations/LLM Foundations - MOC|LLM Foundations - MOC]]

---

## References

- Google ML Crash Course: https://developers.google.com/machine-learning/crash-course/
- Microsoft Learn ML Fundamentals: https://learn.microsoft.com/en-us/training/modules/fundamentals-machine-learning/
- DeepLearning.AI ML Specialization: https://www.deeplearning.ai/courses/machine-learning-specialization/
- Stanford CS229: https://cs229.stanford.edu/
- IBM ML Hub: https://www.ibm.com/think/machine-learning
