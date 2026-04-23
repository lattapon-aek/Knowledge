---
tags:
  - claude-code
  - openclaw
  - comparison
  - agent-architecture
type: note
status: evergreen
source: "arxiv 2604.14228"
parent_note: "[[Claude Code - Multi-Agent MOC]]"
created: "2026-04-20"
updated: ""
---

# Claude Code vs OpenClaw — Comparative Architecture

> สรุปจาก arxiv 2604.14228 (Dive into Claude Code) Section 10
> เปรียบเทียบ design choices ของ 2 agent systems ที่ตอบ design questions เดียวกันจาก deployment context ต่างกัน

---

## ทำไมเปรียบเทียบ

Claude Code คือ CLI coding harness ผูกกับ repository session เดียว
OpenClaw คือ persistent WebSocket gateway เชื่อม ~24 messaging surfaces (WhatsApp, Telegram, Slack, Discord, Signal ฯลฯ) เข้ากับ embedded agent runtime

ทั้งสองตอบ **design questions เดียวกัน** (reasoning อยู่ตรงไหน, safety posture เป็นอย่างไร, context จัดการอย่างไร, extensibility วางอย่างไร) แต่ได้คำตอบต่างกันเพราะ deployment context ต่างกัน

สิ่งที่น่าสนใจคือ OpenClaw สามารถ host Claude Code เป็น external coding harness ผ่าน ACP (Agent Client Protocol) ได้ — ทำให้ทั้งสองเป็น **composable** ไม่ใช่แค่ alternative

---

## เปรียบเทียบ 6 มิติ

| มิติ | Claude Code | OpenClaw |
|---|---|---|
| **System scope** | CLI/IDE coding harness, ephemeral per-session | Persistent WS gateway daemon, multi-channel control plane |
| **Trust model** | Deny-first per-action, 7 modes, ML classifier | Single trusted operator per gateway, DM pairing + allowlists, opt-in sandboxing |
| **Agent runtime** | queryLoop() async generator เป็นศูนย์กลาง | Agent runner embedded ใน gateway RPC dispatch |
| **Extension architecture** | 4 mechanisms จัดตาม context cost | Manifest-first plugin system, 12 capability types, central registry |
| **Memory & context** | CLAUDE.md 4-level + 5-layer compaction | Workspace bootstrap files + separate memory system (MEMORY.md, daily notes, dreaming) |
| **Multi-agent** | Task-delegating subagents + worktree isolation | Multi-agent routing (isolated agents, binding-based dispatch) + sub-agent delegation (configurable nesting) |

---

## Insight หลัก 3 ข้อ

### 1. Design Questions เดียวกัน คำตอบต่างกัน

design questions ที่ recurring (reasoning อยู่ตรงไหน, safety posture, context management, extensibility) ใช้ได้กับ agent systems ทุกประเภท ไม่ใช่แค่ coding agents — **คำถามนิ่ง คำตอบเปลี่ยนตาม deployment context**

### 2. Opposite Bets

| ด้าน | Claude Code | OpenClaw |
|---|---|---|
| Safety | per-action classification + graduated modes | perimeter-level identity + access control |
| Architecture center | agent loop เป็นศูนย์กลาง | gateway control plane เป็นศูนย์กลาง, agent loop เป็น component |
| Extensions | modify context window ของ agent เดียว | extend gateway capability surface ข้าม agents ทั้งหมด |
| Memory | graduated context compression (5 layers) | structured long-term memory promotion (dreaming, daily notes) |

### 3. Composable ไม่ใช่ Exclusive

design space ของ AI agents ไม่ใช่ flat taxonomy แต่เป็น **layered** — gateway-level systems และ task-level harnesses สามารถ compose กันได้

---

## ความสัมพันธ์กับโน้ตอื่น

- [[03 Tools/Claude Code/Core/01 - Claude Code คืออะไร|Claude Code คืออะไร]] — ภาพรวม Claude Code
- [[03 Tools/Claude Code/Reference/09 - Permissions และ Settings|Permissions และ Settings]] — trust model ของ Claude Code
- [[03 Tools/Claude Code/Core/25 - Context Compaction Pipeline|Context Compaction Pipeline]] — context management ของ Claude Code
- [[03 Tools/Claude Code/Core/26 - Extensibility Mechanisms|Extensibility Mechanisms]] — extension architecture ของ Claude Code
- [[02 AI Systems/AI Agent Fundamentals/Core/07 - รูปแบบ Agent Architectures|Agent Architectures]] — patterns ที่ทั้งสองระบบ implement
- [[04 Synthesis/Decision/Synthesis - Workflow vs AI Agent|Workflow vs AI Agent]] — decision framework ที่เกี่ยวข้อง
- [[03 Tools/Claude Code/Claude Code - Multi-Agent MOC|Claude Code - Multi-Agent MOC]]
