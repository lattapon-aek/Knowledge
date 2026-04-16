---
tags:
  - synthesis
  - multi-agent
  - failure-modes
  - reliability
  - version-sensitive
  - derived
type: synthesis
status: evergreen
source: "https://platform.openai.com/docs/guides/agent-builder-safety · https://platform.openai.com/docs/guides/trace-grading · https://platform.openai.com/docs/guides/agent-evals · https://docs.langchain.com/oss/javascript/langgraph/persistence · https://docs.langchain.com/oss/javascript/langchain/human-in-the-loop · https://microsoft.github.io/autogen/stable/user-guide/core-user-guide/design-patterns/group-chat.html · https://docs.crewai.com/en/concepts/flows"
parent_note: "[[04 Synthesis/Synthesis - MOC]]"
---

# Synthesis - Multi-Agent Failure Modes

## ภาพรวม

multi-agent systems fail in ways single-agent systems usually do not. The biggest risks are not just bad answers, but broken handoffs, stale shared state, duplicated work, prompt injection through tool paths, and observability gaps that make the failure invisible.

This note separates failure modes by layer so they can be debugged and prevented systematically.

---

## 1. ความผิดพลาดด้าน Orchestration

### Handoff ที่หลุดเจ้าของ

An agent delegates work, but no one owns the next step.

Symptoms:
- task disappears after a transfer
- a specialist finishes but no downstream agent consumes the result
- the orchestrator has no clear completion signal

Why it happens:
- handoff contract is implicit
- task ownership is not encoded in state
- routing logic does not know what “done” means

### เลือก Agent ถัดไปผิด

The orchestrator selects the wrong specialist or loops between agents.

Symptoms:
- repeated routing to the wrong role
- unnecessary back-and-forth
- task never converges

Why it happens:
- role boundaries are too vague
- router criteria are underspecified
- there is no stop condition

### ลำดับการทำงานแฝง

The system looks parallel on paper but is effectively sequential in execution.

Symptoms:
- parallel agents block on the same shared state
- one agent becomes a bottleneck
- turns are serialized unintentionally

AutoGen group chat is explicitly sequential under a manager agent, so “multi-agent” does not automatically mean concurrent execution.

---

## 2. ความผิดพลาดด้าน State และ Memory

### Shared State ที่ล้าสมัย

One agent reads state that is no longer valid.

This is especially likely when:
- state is persisted across long-running workflows
- human approval interrupts the flow
- state is updated by multiple participants

LangGraph persistence and CrewAI flows both show that long-running agent workflows need explicit state persistence; that also means state versioning and ownership matter.

### มุมมอง State ที่ไม่ตรงกัน

Different agents hold inconsistent versions of the same task state.

Symptoms:
- agents disagree on the current status
- one agent acts on outdated context
- repeated or conflicting outputs

### Memory ปนเปื้อน

Long-term memory absorbs transient or incorrect information.

Symptoms:
- the system keeps recalling one-off mistakes
- user preferences and task facts get mixed
- a recovered thread behaves differently than expected

---

## 3. ความผิดพลาดด้านการสื่อสาร

### งานซ้ำซ้อน

Two agents do the same task because the communication channel or task assignment is unclear.

### Queue ล่าช้าหรือ Backpressure

Async messaging decouples agents, but it can create backlog or delayed execution if no one monitors the queue.

### ข้อความกำกวม

Agents send messages that are too large, too vague, or missing required fields.

### Context หายตอน Handoff

The receiving agent gets a summary that omits critical evidence or constraints.

This is common when the team relies on messages instead of structured state or checkpoints.

---

## 4. ความผิดพลาดด้าน Tool และ Security

### Prompt Injection ผ่าน Tool Inputs

OpenAI’s agent safety guidance explicitly warns that untrusted text or data entering a workflow can try to override instructions or cause unintended downstream actions.

This matters more in multi-agent systems because:
- one agent may process untrusted content
- another agent may receive the transformed result
- tool calls can carry malicious payloads downstream

### Tool Access กว้างเกินไป

If every agent can use every tool, the blast radius of a bad decision grows quickly.

### Handoff ที่ไม่ปลอดภัยไปยัง MCP หรือ External Tools

If the system does not separate read-only from side-effecting actions, a simple routing mistake can become an actual external action.

---

## 5. ความผิดพลาดด้าน Observability

### มอง Trace ไม่เห็น

OpenAI trace grading emphasizes that traces capture decisions, tool calls, and reasoning steps; without them, workflow-level failures are hard to locate.

### เห็นแค่ Final Answer

The output looks fine, but the process was expensive, unsafe, or brittle.

### ไม่มีสัญญาณ Regression

The system changes over time, but nobody notices that handoff quality or failure recovery got worse.

OpenAI agent evals and trace grading are designed to make those regressions visible.

---

## 6. ความผิดพลาดด้าน Recovery

### Retry Storm

Multiple agents retry the same failing step without a common policy.

### วนลูปไม่จบ

The team keeps revisiting the same unresolved branch.

### Recovery ได้แค่บางส่วน

One subtask is recovered, but the system cannot resume the full workflow consistently.

LangGraph interrupt/resume and CrewAI resume semantics show why recovery must be designed at the workflow level, not only at the tool-call level.

---

## กติกาป้องกันความผิดพลาด

- make ownership explicit at every handoff
- persist state with versioning and stable identifiers
- keep agent roles narrow and observable
- separate read-only agents from agents that can cause side effects
- require traces before you optimize
- use evals on trajectories, not just final answers
- define retry and escalation limits up front

---

## ลิงก์ที่เกี่ยวข้อง

- [[04 Synthesis/Synthesis - Single to Multi-Agent Infrastructure]]
- [[06 Engineering/Architecture to Code/Architecture - Multi-Agent Infrastructure]]
- [[06 Engineering/Architecture to Code/Architecture - Multi-Agent Security and Permissions]]
- [[06 Engineering/Architecture to Code/Architecture - Multi-Agent Deployment and Topology]]
- [[06 Engineering/Patterns/Pattern - Sync vs Async Agent Communication]]
- [[02 AI Systems/Evals/Application/09 - Multi-Agent Evals]]
- [[02 AI Systems/Guardrails/Guardrails - MOC]]
- [[02 AI Systems/Agent Frameworks/Core/07 - Checkpointing and Resumability]]
- [[Home]]

---

## แหล่งอ้างอิง

- OpenAI Safety in Building Agents: https://platform.openai.com/docs/guides/agent-builder-safety
- OpenAI Trace Grading: https://platform.openai.com/docs/guides/trace-grading
- OpenAI Agent Evals: https://platform.openai.com/docs/guides/agent-evals
- LangGraph Persistence: https://docs.langchain.com/oss/javascript/langgraph/persistence
- LangGraph HITL: https://docs.langchain.com/oss/javascript/langchain/human-in-the-loop
- AutoGen Group Chat: https://microsoft.github.io/autogen/stable/user-guide/core-user-guide/design-patterns/group-chat.html
- CrewAI Flows: https://docs.crewai.com/en/concepts/flows
