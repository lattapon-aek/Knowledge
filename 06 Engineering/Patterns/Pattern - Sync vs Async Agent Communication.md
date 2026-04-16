---
tags:
  - engineering
  - patterns
  - multi-agent
  - messaging
  - communication
  - version-sensitive
  - derived
type: note
status: evergreen
source: "https://www.digitalocean.com/community/tutorials/single-to-multi-agent-infrastructure · https://microsoft.github.io/autogen/stable/user-guide/core-user-guide/design-patterns/group-chat.html · https://docs.crewai.com/en/concepts/flows"
parent_note: "[[06 Engineering/Patterns/Patterns - MOC]]"
---

# Pattern - Sync vs Async Agent Communication

## ภาพรวม

Communication between agents is a design choice, not an implementation detail. Use synchronous communication when you need strict ordering and simpler control flow. Use asynchronous communication when you need decoupling, retries, and better throughput.

---

## การสื่อสารแบบ Synchronous

Use when:
- the caller should wait for an answer before continuing
- ordering matters
- the flow is short and easy to debug
- you want simpler ownership and failure visibility

Characteristics:
- request/response
- tighter coupling
- lower conceptual overhead
- easier to reason about in a small pipeline

---

## การสื่อสารแบบ Asynchronous

Use when:
- agents can work independently
- the system needs decoupling
- retries and buffering matter
- you expect bursts or long-running tasks

Characteristics:
- queue / pub-sub / topic-based
- better isolation between producers and consumers
- requires more infrastructure discipline
- needs retry, backpressure, and dead-letter handling

---

## เมื่อควรเลือก Sync

- orchestrator calling a helper agent
- low-latency handoff
- strict sequencing
- small number of agents

## เมื่อควรเลือก Async

- data collection followed by later analysis
- independent specialist agents
- long-running workflows
- higher throughput or burst tolerance

---

## หลักออกแบบ

- decide message semantics before choosing a transport
- if async, define idempotency and retry policy up front
- if multiple agents share a topic, define ownership and namespaces
- keep the message payload small enough to avoid context bloat
- do not use async just because it sounds more scalable

---

## Failure Modes ที่พบบ่อย

- treating a queue as a magic fix for poor orchestration
- blocking a synchronous call chain that should have been async
- losing the trace of who sent what and why
- duplicating work because idempotency is undefined

---

## ลิงก์ที่เกี่ยวข้อง

- [[04 Synthesis/Synthesis - Single to Multi-Agent Infrastructure]]
- [[06 Engineering/Architecture to Code/Architecture - Multi-Agent Infrastructure]]
- [[06 Engineering/Patterns/Pattern - Retry and Backoff]]
- [[02 AI Systems/Agent Frameworks/Core/04 - Tool Orchestration]]
- [[02 AI Systems/Agent Frameworks/Core/07 - Checkpointing and Resumability]]
