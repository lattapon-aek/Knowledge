---
tags:
  - evals
  - multi-agent
  - evaluation
  - traces
  - reliability
  - version-sensitive
  - derived
type: note
status: evergreen
source: "https://platform.openai.com/docs/guides/agent-evals · https://platform.openai.com/docs/guides/trace-grading · https://platform.openai.com/docs/guides/evals · https://platform.openai.com/docs/guides/evaluation-best-practices · https://docs.langchain.com/oss/javascript/langgraph/persistence · https://docs.crewai.com/en/concepts/flows"
parent_note: "[[02 AI Systems/Evals/Evals - MOC|Evals - MOC]]"
---

# Evals - Multi-Agent Evals

## ภาพรวม

multi-agent evals must measure more than answer quality. They need to measure how well agents coordinate, hand off tasks, recover from failures, and stay within policy and budget.

OpenAI explicitly recommends trace grading for workflow-level errors, and its agent eval docs position trace grading as the right tool when you need to identify where an agent or workflow went wrong.

---

## สิ่งที่ต้องวัด

### 1. การทำงานสำเร็จ

- did the full workflow finish
- did all required subtasks complete
- did the system produce a usable final result

### 2. คุณภาพของ Handoff

- did the right agent receive the right task
- was the payload complete
- was ownership unambiguous
- did the next agent continue without rework

### 3. ความสอดคล้องของ State

- did all agents observe the same task state
- did interrupts or resumes preserve correctness
- did persisted state reflect the latest valid update

### 4. ความถูกต้องของ Tool

- were the right tools used
- were arguments valid
- were side effects authorized
- were failures handled correctly

### 5. ความปลอดภัยและการทำตามนโยบาย

- were permission boundaries respected
- did the workflow avoid unsafe actions
- did the team remain robust to prompt injection and untrusted inputs

### 6. ต้นทุนเชิงปฏิบัติการ

- number of tool calls
- number of retries
- latency per handoff
- token cost per completed task

---

## ทำไมประเมินแค่ Final Answer ไม่พอ

In multi-agent systems, the final answer can look correct while the system still:
- wasted steps
- took unsafe actions
- lost state between agents
- routed through the wrong specialist
- recovered from failure incorrectly

Trace grading is useful because it evaluates the actual trace of decisions and actions rather than only the end output.

---

## ชั้นของ Evaluation

```mermaid
flowchart TD
    A[Task] --> B[Trace]
    B --> C[Task completion]
    B --> D[Handoff quality]
    B --> E[Tool correctness]
    B --> F[Safety]
    B --> G[Cost / latency]
    C --> H[Decision]
    D --> H
    E --> H
    F --> H
    G --> H
```

### ชั้น 1: การให้คะแนนระดับตัวอย่าง

Score a single run:
- pass / fail
- rubric score
- LLM-judge score

### ชั้น 2: Trace Grading

Grade the sequence of actions:
- route choice
- intermediate decisions
- retries
- handoffs
- completion behavior

### ชั้น 3: Regression Testing

Compare current behavior to previous behavior:
- did coordination degrade
- did retries increase
- did latency jump
- did safety regress

### ชั้น 4: System Benchmarks

Run repeated tasks across multiple scenarios:
- typical cases
- edge cases
- adversarial cases
- interrupted runs

---

## เคสทดสอบเฉพาะ Multi-Agent

1. **Correct handoff**
   - one agent finishes, another consumes the result without losing context

2. **Broken handoff**
   - the next agent receives incomplete or stale state

3. **Interrupted run**
   - workflow pauses and resumes after human approval or failure

4. **Routing ambiguity**
   - multiple specialists are plausible and the router must choose

5. **Tool failure**
   - one agent’s tool call fails and the system must recover

6. **Prompt injection exposure**
   - untrusted input enters one agent and is forwarded downstream

7. **Budget pressure**
   - the team must finish within latency or cost constraints

---

## Metric ที่แนะนำ

- task success rate
- handoff success rate
- state consistency rate
- retry count per completed task
- median / p95 latency
- tool-call count
- escalation rate
- safety violation count

---

## หลักออกแบบ

- evaluate the trace, not just the answer
- make handoffs explicit in the test set
- include resume and interrupt cases
- include unsafe / adversarial cases
- measure cost and latency alongside quality
- keep a regression corpus for the actual workflow topology

---

## ลิงก์ที่เกี่ยวข้อง

- [[02 AI Systems/Evals/Application/08 - Agent Evals]]
- [[02 AI Systems/Evals/Core/09 - Observability and Feedback Loops]]
- [[04 Synthesis/Bridge/Synthesis - Multi-Agent Failure Modes]]
- [[06 Engineering/Architecture to Code/Architecture - Multi-Agent Infrastructure]]
- [[06 Engineering/Patterns/Pattern - Sync vs Async Agent Communication]]
- [[06 Engineering/Patterns/Pattern - Retry and Backoff]]
- [[Home]]

---

## แหล่งอ้างอิง

- OpenAI Agent Evals: https://platform.openai.com/docs/guides/agent-evals
- OpenAI Trace Grading: https://platform.openai.com/docs/guides/trace-grading
- OpenAI Evals: https://platform.openai.com/docs/guides/evals
- OpenAI Evaluation Best Practices: https://platform.openai.com/docs/guides/evaluation-best-practices
- LangGraph Persistence: https://docs.langchain.com/oss/javascript/langgraph/persistence
- CrewAI Flows: https://docs.crewai.com/en/concepts/flows
