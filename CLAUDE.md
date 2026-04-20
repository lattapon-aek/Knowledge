# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Repo Is

An Obsidian knowledge vault for AI systems, LLMs, agents, prompting, and tooling. Content is pure Markdown — there are no build, test, or lint commands. All work involves reading, creating, and editing `.md` files.

**Read `AGENTS.md` first** — it is the authoritative operating guide for vault agents and defines the mission, canonical rules, and all workflows.

---

## Vault Layers

The vault is organized into strict layers. Never mix content across layers.

| Layer | Purpose | Edit? |
|---|---|---|
| `00 Raw Sources/` | Source-of-truth inputs, articles, papers | Read only — never rewrite originals |
| `01 Foundations/` + `02 AI Systems/` | Core concepts and system architecture | Yes |
| `03 Tools/` | Tool-specific notes (treat as volatile) | Yes, mark version-sensitive content explicitly |
| `04 Synthesis/` | Cross-topic synthesis and comparison | Yes |
| `05 Use Cases/` | Practical reading paths and applied examples | Yes |
| `06 Engineering/` | Frameworks, recipes, decisions, implementation notes | Yes |
| `_Templates/` | Reusable note templates | Use as starting point |
| Root schema docs | `AGENTS.md`, `Home.md`, `index.md`, `Vault Standards - *.md` | Edit with care — these define vault rules |

**Entry points:** Start from `index.md` or the relevant MOC before editing leaf notes. Navigation hubs: `Home.md` → domains → MOC → numbered notes.

---

## Note Naming

- Numbered sequential notes: `NN - หัวข้อ.md`
- MOC (map of content) pages: `Topic - MOC.md`
- Synthesis notes: `Synthesis - ...`
- Engineering notes: `Architecture to Code - ...`, `Framework - ...`, `Pattern - ...`, `Recipe - ...`, `Decision - ...`, `Project Note - ...`
- Standards/workflow docs: `Vault Standards - ...` or `Vault Workflow - ...`

---

## Required Frontmatter

Every new note must include these properties (see `Vault Standards - Properties.md`):

```yaml
---
tags:
  - topic
type: note          # home | moc | note | synthesis | guide | glossary | template
status: draft       # seed | draft | evergreen
source: ""          # plain string, no markdown formatting
parent_note: "[[MOC or parent]]"
created: "YYYY-MM-DD"
updated: ""
---
```

- Use `parent_note` not `up`
- Empty fields use `""` not null
- Quick captures start at `seed`; regular notes start at `draft`; MOCs, synthesis, and reusable references use `evergreen`

---

## Writing Standards

- **Language:** Thai is primary. Keep English technical terms that would lose meaning if translated (e.g., `context window`, `RAG`, `tool calling`, `prompt caching`)
- **Sources:** When reliability matters, use only official docs or primary sources. Never fabricate claims. Label architectural inferences explicitly as `architectural inference` or `design inference`
- **Diagrams:** Use Mermaid for architecture, loops, workflows, and comparisons — only when it aids understanding

---

## Core Workflows

### Ingest (new source → wiki)
1. Confirm the source exists under `00 Raw Sources/`
2. Identify which wiki layer it belongs in
3. Merge into an existing note if possible; create a new one only if there is no good home
4. Fill `source:` on every touched note
5. Add cross-links to relevant MOC, synthesis, glossary, or use cases
6. If a new topic hub is needed, create the MOC first, then the leaf notes

### Query → file-back
1. Start from `index.md` or the relevant MOC
2. Answer from the vault first
3. If the answer has long-term knowledge value (comparison, synthesis, decision framework, glossary entry, reusable use case), offer to write it back as a new note

### Lint (health check)
Check for: broken wiki links, malformed frontmatter, notes missing `parent_note`, orphan pages with no MOC, topics mentioned repeatedly without a central note, inconsistent section labels.

---

## Key Rules

- **Prefer merge over creation.** If content fits an existing note, extend it — don't create a duplicate.
- **Raw sources are immutable.** Never rewrite or summarize directly into `00 Raw Sources/`.
- **`03 Tools/Claude Code/` is volatile.** Notes tied to specific releases, settings, or terminal behavior must be marked `version-sensitive`.
- **Always update MOCs and cross-links** when creating or moving a note.
- **One canonical home per topic.** If a topic spans multiple layers, pick the best layer and link outward from the others.
