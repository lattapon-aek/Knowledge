---
tags:
  - engineering
  - architecture
  - multi-agent
  - security
  - permissions
  - guardrails
  - version-sensitive
  - derived
type: note
status: evergreen
source: "https://developers.openai.com/api/docs/guides/agent-builder-safety · https://platform.openai.com/docs/guides/agent-builder · https://platform.openai.com/docs/guides/trace-grading"
parent_note: "[[06 Engineering/Architecture to Code/Architecture to Code - MOC]]"
---

# Architecture - Multi-Agent Security and Permissions

## ภาพรวม

Multi-agent security is mostly a trust-boundary problem. Every extra agent, tool, or handoff increases the places where untrusted input can affect behavior. The safe default is least privilege per agent, structured handoffs, approvals for side effects, and traceable boundaries between read, write, and human-review paths.

---

## โมเดลความเสี่ยง

Treat all of the following as untrusted unless explicitly validated:
- user input
- tool output
- retrieved documents
- downstream agent output
- MCP / connector data

OpenAI’s agent safety guidance explicitly warns that prompt injection happens when untrusted text or data enters an AI system and tries to override instructions. The same guidance also calls out private data leakage as a risk when agent workflows share too much context or too many privileges.

---

## โมเดลสิทธิ์

### 1. Read-only Agents

Use for:
- retrieval
- summarization
- classification
- evidence collection

Rules:
- no side effects
- no external writes
- no secret access
- output must be structured

### 2. Write-capable Agents

Use for:
- state updates
- tool calls with external impact
- content generation that becomes an input to later actions

Rules:
- only the minimum tool set
- only validated inputs
- every write must be traceable

### 3. Approval-gated Agents

Use for:
- payments
- irreversible actions
- production-side changes
- privileged MCP operations

OpenAI’s safety guide is explicit: keep tool approvals on, and use the human approval node in Agent Builder so end users can review and confirm each operation, including reads and writes.

### 4. สิทธิ์เฉพาะ Orchestrator

Reserve for:
- routing decisions
- escalation policy
- state ownership
- approval routing
- final handoff validation

This keeps control logic separate from specialist work.

---

## กติกาขอบเขต

- Never inject untrusted variables directly into developer messages.
- Pass untrusted inputs through user messages or validated structured fields.
- Prefer enums or fixed schemas over freeform text between agents.
- Do not let raw retrieved text drive tool calls without filtering.
- Keep secrets out of shared handoff payloads.
- Do not let a downstream agent inherit more privilege than the upstream step needed.

OpenAI recommends using structured outputs to constrain data flow and reduce injection surface area.

---

## ความปลอดภัยของ Handoff

Every handoff should include only:
- task id
- allowed next action
- bounded evidence
- validated state snapshot
- explicit completion criteria

Do not hand off:
- raw secrets
- arbitrary freeform tool output
- unbounded conversation history
- implementation details the next agent does not need

If one agent processes untrusted text and another agent uses the transformed result, sanitize before the handoff. That is where multi-agent systems often become vulnerable even if the first agent looked safe.

---

## ชั้นของ Guardrail

Use the following layers together:

1. input validation
2. structured outputs
3. permission scoping
4. human approval for side effects
5. trace logging
6. evals on risky traces

OpenAI recommends guardrails for user inputs, tool approvals for MCP operations, and trace graders / evals for catching mistakes in agent behavior.

---

## Checklist การลงมือทำ

Before shipping a multi-agent workflow:
1. Define which agents are read-only.
2. Define which agents can write state.
3. Define which agents can call side-effecting tools.
4. Define human approval points.
5. Define structured handoff payloads.
6. Define what never leaves the trust boundary.
7. Log enough trace data to reconstruct decisions.
8. Test prompt injection and unsafe handoff paths.

---

## หลักออกแบบ

- assume prompt injection can travel through tool output
- isolate high-trust and low-trust paths
- narrow permissions by role, not by convenience
- require approval where the action cannot be safely reversed
- make every privilege escalation explicit

---

## ลิงก์ที่เกี่ยวข้อง

- [[04 Synthesis/Synthesis - Multi-Agent Failure Modes]]
- [[06 Engineering/Architecture to Code/Architecture - Multi-Agent Ownership and Handoffs]]
- [[06 Engineering/Patterns/Pattern - Sync vs Async Agent Communication]]
- [[02 AI Systems/Guardrails/Guardrails - MOC]]
- [[02 AI Systems/Evals/Application/09 - Multi-Agent Evals]]
- [[02 AI Systems/MCP/MCP - MOC]]
- [[Home]]

---

## แหล่งอ้างอิง

- OpenAI Safety in Building Agents: https://developers.openai.com/api/docs/guides/agent-builder-safety
- OpenAI Agent Builder: https://platform.openai.com/docs/guides/agent-builder
- OpenAI Trace Grading: https://platform.openai.com/docs/guides/trace-grading
