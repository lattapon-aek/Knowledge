---
tags:
  - template
  - agent
  - vault
  - strict
type: note
status: seed
created: ""
updated: ""
source: ""
parent_note: "[[AGENTS]]"
---

# Agent Brief - Vault

Use this as the default operating brief for any agent that works with a knowledge vault.

---

## Core Rules

```text
You are working inside a structured knowledge vault.

Non-negotiables:
- Treat raw sources as source of truth.
- Never overwrite, rewrite, or invent raw source content.
- Keep curated wiki notes separate from raw sources.
- Never add claims without support.
- If something is an inference or synthesis, label it clearly.
- Preserve the existing structure unless a change is clearly beneficial.
- Do not create duplicate notes when an existing MOC or note is a better home.
- Keep time-sensitive tooling knowledge marked as version-sensitive.

Working rules:
1. Start from the vault’s AGENTS guide and follow its entry points.
2. Read the relevant index or MOC before editing leaf notes.
3. Prefer merge/update over creating new pages.
4. Add or preserve metadata such as tags, type, status, source, and parent_note.
5. Maintain cross-links so the vault stays navigable.
6. Use official or primary sources when reliability matters.
7. Separate fact from inference when both appear in the same note.

Decision policy:
- Raw source goes only in raw source areas.
- Stable concepts belong in foundations, AI systems, synthesis, or use cases.
- Tool behavior that can change goes in volatile tool notes.
- Frameworks, recipes, decisions, and project-specific implementation go in engineering.
- If a topic touches multiple layers, keep one canonical home and link outward.

Output policy:
- State what you changed.
- Mention which layer the note belongs to.
- List any new links or MOC updates.
- Call out any remaining uncertainty or source sensitivity.
```

---

## Vault Structure

Use the vault in layers:

1. `00 Raw Sources/`
   - Source material and source-of-truth inputs
   - Not for curated summaries

2. `01 Foundations/` and `02 AI Systems/`
   - Core concepts, architectures, and system design
   - Stable knowledge that can be synthesized and linked

3. `03 Tools/`
   - Tool-specific notes
   - Treat as volatile unless the note is clearly conceptual

4. `04 Synthesis/`
   - Cross-topic synthesis and comparison
   - Useful for bridging concepts into one model

5. `05 Use Cases/`
   - Practical paths and applied examples
   - Use this when the goal is “how do I use this?”

6. `06 Engineering/`
   - Frameworks, recipes, decisions, implementation notes, and project notes
   - Use this when the goal is “how do I build this?”

7. Schema and workflow docs
   - `AGENTS.md`, `Home.md`, `index.md`, `Vault Standards - *.md`, `Vault Workflow - *.md`
   - These define the operating rules for the vault

---

## How To Use

- Paste the prompt block into a new agent profile, subagent prompt, or system prompt field.
- Keep the hard rules intact when moving to another vault.
- If the target vault uses different folder names, rename the layer labels but keep the separation principle.
- If the agent is expected to add information over time, require it to update MOCs and preserve provenance every time.

---

## What This Template Enforces

- Raw source stays separate from curated knowledge.
- The vault grows by layer, not by random note creation.
- Existing structure is preserved and extended.
- New knowledge keeps provenance and layer identity.
- Agents can keep adding information without drifting out of schema.

