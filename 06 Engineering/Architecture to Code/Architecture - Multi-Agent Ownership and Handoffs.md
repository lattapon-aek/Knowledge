---
tags:
  - engineering
  - architecture
  - multi-agent
  - ownership
  - handoff
  - state
  - derived
type: note
status: evergreen
source: "https://platform.openai.com/docs/guides/agent-builder-safety · https://platform.openai.com/docs/guides/trace-grading · https://docs.langchain.com/oss/javascript/langgraph/persistence · https://docs.langchain.com/oss/javascript/langchain/human-in-the-loop · https://microsoft.github.io/autogen/stable/user-guide/core-user-guide/design-patterns/group-chat.html · https://docs.crewai.com/en/concepts/flows"
parent_note: "[[06 Engineering/Architecture to Code/Architecture to Code - MOC]]"
---

# Architecture - Multi-Agent Ownership and Handoffs

## Summary

Multi-agent systems need an explicit ownership model. Every handoff should answer three questions:
- who owns the task now
- what state is transferred
- how completion or escalation is signaled

Without those answers, delegation becomes ambiguous and the workflow becomes hard to debug.

---

## Ownership Model

### 1. Orchestrator Owns The Workflow

The orchestrator or manager is responsible for:
- routing
- stopping conditions
- retry/escalation policy
- overall workflow state
- traceability of the run

OpenAI Agent Builder frames agents as workflows composed of agents, tools, and control-flow logic. That means ownership of the workflow itself is separate from the ownership of any individual specialist.

### 2. Specialists Own Narrow Subtasks

Specialist agents should own a bounded responsibility:
- retrieve evidence
- draft content
- validate output
- review policy compliance
- summarize state

If a specialist owns too much, handoffs become noisy and recovery gets harder.

### 3. State Owner Must Be Explicit

State should have one of these ownership patterns:
- orchestrator-owned shared state
- agent-local state with explicit handoff payloads
- persisted checkpoint state with thread/run identity

LangGraph persistence uses checkpoints organized into threads, and human-in-the-loop workflows require that the state be inspectable and resumable.

---

## Handoff Contract

Every handoff should define:
- source agent
- destination agent
- task id
- state payload
- expected output format
- success criteria
- escalation criteria

If the handoff is async, also define:
- retry policy
- idempotency key
- timeout
- dead-letter behavior

---

## Handoff Patterns

### Controller To Specialist

The controller decides who acts next.

Use when:
- the flow is mostly sequential
- you want tight control
- you need simple debugging

AutoGen group chat uses a manager agent to select the next speaker; even there, the manager remains the authority for sequencing.

### State-Based Handoff

Agents pass a task forward when state criteria are met.

Use when:
- work should advance only after explicit conditions
- the workflow has multiple phases
- the next agent can infer from persisted state

### Shared Topic Or Shared Thread

Agents subscribe to the same conversation or topic and take turns.

Use when:
- collaboration matters more than strict request/response
- the team needs a common context
- role-based turn taking is acceptable

CrewAI Flows and Tasks/Processes expose stateful orchestration primitives that fit this pattern.

---

## State Schema Rules

- keep state schema versioned
- separate transient state from long-term memory
- keep handoff payloads compact and structured
- include provenance for state that came from tools or retrieval
- do not place secrets in shared handoff payloads

---

## Security And Boundary Rules

- define which agents are read-only
- define which agents can call side-effecting tools
- require approval gates where needed
- isolate high-risk tools from low-trust inputs
- assume prompt injection can travel through tool outputs unless filtered

OpenAI’s agent safety guidance explicitly treats untrusted text and tool paths as security boundaries.

---

## Implementation Checklist

Before coding the workflow:
1. Define the orchestrator role.
2. Define each specialist’s scope.
3. Define handoff payload schema.
4. Define state ownership.
5. Define resume and interrupt behavior.
6. Define tool permissions.
7. Define trace logging fields.
8. Define retry and escalation thresholds.

---

## Design Rules

- never delegate without a handoff contract
- never persist state without an owner
- never let message payloads become an unstructured dump
- never use shared state as a shortcut for poor routing
- never allow handoffs to erase provenance

---

## Cross Links

- [[04 Synthesis/Synthesis - Single to Multi-Agent Infrastructure]]
- [[04 Synthesis/Synthesis - Multi-Agent Failure Modes]]
- [[06 Engineering/Architecture to Code/Architecture - Multi-Agent Infrastructure]]
- [[06 Engineering/Architecture to Code/Architecture - Multi-Agent Security and Permissions]]
- [[06 Engineering/Architecture to Code/Architecture - Multi-Agent Deployment and Topology]]
- [[06 Engineering/Patterns/Pattern - Sync vs Async Agent Communication]]
- [[02 AI Systems/Agent Frameworks/Core/07 - Checkpointing and Resumability]]
- [[02 AI Systems/MCP/MCP - MOC]]
- [[Home]]

---

## References

- OpenAI Agents / Agent Builder: https://platform.openai.com/docs/guides/agent-builder
- OpenAI Safety in Building Agents: https://platform.openai.com/docs/guides/agent-builder-safety
- OpenAI Trace Grading: https://platform.openai.com/docs/guides/trace-grading
- LangGraph Persistence: https://docs.langchain.com/oss/javascript/langgraph/persistence
- LangGraph HITL: https://docs.langchain.com/oss/javascript/langchain/human-in-the-loop
- AutoGen Group Chat: https://microsoft.github.io/autogen/stable/user-guide/core-user-guide/design-patterns/group-chat.html
- CrewAI Flows: https://docs.crewai.com/en/concepts/flows
