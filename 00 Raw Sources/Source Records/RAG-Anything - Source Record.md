---
tags:
  - source-record
  - rag
  - multimodal
  - framework
type: note
status: evergreen
source: "RAG-Anything GitHub + arxiv 2510.12323"
parent_note: "[[00 Raw Sources/Source Records/Source Records - MOC]]"
created: "2026-04-20"
updated: ""
---

# RAG-Anything - Source Record

## ข้อมูล Source

| Field | Value |
|---|---|
| ชื่อ | RAG-Anything: All-in-One RAG Framework |
| ผู้แต่ง | Zirui Guo, Xubin Ren, Lingrui Xu, Jiahao Zhang, Chao Huang (HKUDS) |
| ประเภท | Framework + Technical Report |
| URL (GitHub) | https://github.com/HKUDS/RAG-Anything |
| URL (Paper) | https://arxiv.org/abs/2510.12323 |
| สร้างบน | LightRAG |

## ขอบเขตเนื้อหา

- Multimodal RAG pipeline สำหรับ documents ที่มี text, images, tables, equations, charts
- Multimodal document parsing (MinerU, Docling, PaddleOCR)
- Modality-specific analysis (image, table, equation, extensible)
- Multimodal Knowledge Graph Index (cross-modal entity extraction + relationship mapping)
- Hybrid retrieval: vector similarity + graph traversal (modality-aware ranking)
- VLM-enhanced query mode

## เนื้อหาหลักที่เกี่ยวกับ Vault

| หัวข้อ | เกี่ยวกับหมวด |
|---|---|
| Multimodal RAG architecture | `02 AI Systems/RAG` |
| Cross-modal Knowledge Graph | `02 AI Systems/RAG/Retrieval/RAG - Knowledge Graph RAG` |
| Vector-Graph Fusion retrieval | `02 AI Systems/RAG/Retrieval/RAG - Hybrid Retrieval` |
| VLM-enhanced query | `02 AI Systems/RAG/Core/RAG - Agentic RAG` |
| Multimodal foundations | `01 Foundations/LLM Foundations/Core/11 - Multimodal Foundations` |

## สถานะ Ingest

- ใช้ใน: [[00 Raw Sources/Articles/2026-04 New Sources - Ingest Plan]]

## Cross-Links

- [[02 AI Systems/RAG/RAG - MOC]]
- [[00 Raw Sources/Source Records/Source Records - MOC]]
