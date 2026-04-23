---
tags:
  - glossary
  - ai-systems
type: glossary
status: evergreen
created: "2026-04-12"
source: ""
parent_note: "[[Home]]"
---

# Glossary - AI Systems

## Agent

ระบบที่พยายามทำเป้าหมายให้สำเร็จโดยสังเกตสถานะ เลือก action และใช้ tools ระหว่างทาง

## Context Window

งบ token ที่โมเดลใช้กับ input และ output ภายในการประมวลผลหนึ่งครั้ง

## Prompt Engineering

การออกแบบ instruction, structure, examples, และ evaluation ให้โมเดลทำงานได้ตามเป้าหมาย

## RAG

การดึงข้อมูลที่เกี่ยวข้องจาก external knowledge source แล้วส่งกลับเข้า context ก่อนให้โมเดลตอบ

## Memory

การเก็บและเรียกใช้ข้อมูลข้ามรอบการทำงานของระบบหรือ agent ทั้งในรูป context, external store, และ reusable instructions

## Eval

กระบวนการวัดว่าระบบ AI ทำงานได้ตาม success criteria หรือไม่ ทั้งแบบ offline, online, และ human review

## Guardrails

กลไกที่ใช้ควบคุมความเสี่ยง ข้อจำกัด พฤติกรรม และความปลอดภัยของ AI system

## Agent Framework

framework หรือ runtime ที่ช่วยสร้างและ orchestration การทำงานของ agents, tools, state, และ workflows

## Harness

ทุกสิ่งที่ไม่ใช่ model ใน agent system — code, configuration, execution logic ที่ทำให้ raw model กลายเป็น agent ที่ทำงานได้จริง (Agent = Model + Harness)

## Harness Engineering

discipline ของการออกแบบระบบรอบ ๆ model เพื่อให้ agent ทำงานได้ reliable, steerable, และ long-running — ครอบคลุม context management, tool orchestration, feedback loops, safety controls, และ multi-agent coordination

## MCP

protocol สำหรับเชื่อม LLM application เข้ากับ tools, resources, และ prompts แบบมาตรฐาน

## Tokenization

กระบวนการแปลงข้อความเป็น token IDs ที่โมเดลใช้จริง

## Cross Links

- [[Home]]
- [[01 Foundations/LLM Foundations/LLM Foundations - MOC]]
- [[02 AI Systems/AI Agent Fundamentals/AI Agent Fundamentals - MOC]]
- [[02 AI Systems/MCP/MCP - MOC]]
- [[02 AI Systems/RAG/RAG - MOC]]
- [[02 AI Systems/Agent Frameworks/Agent Frameworks - MOC]]
- [[02 AI Systems/Evals/Evals - MOC]]
- [[02 AI Systems/Guardrails/Guardrails - MOC]]
