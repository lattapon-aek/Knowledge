# Knowledge Vault

This repository is my Obsidian knowledge vault for AI systems, LLMs, agents, prompting, and related tooling.

The goal is to keep the repo portable:

- content pages are tracked in git
- machine-specific Obsidian state is ignored
- the vault can be opened on a different machine without carrying local UI state

## Table of Contents

- [What lives here](#what-lives-here)
- [How to use](#how-to-use)
- [Git and Obsidian behavior](#git-and-obsidian-behavior)
- [Conventions](#conventions)
- [Useful entry points](#useful-entry-points)
- [Contributing](#contributing)

## What lives here

The vault is organized into a few layers:

- `00 Raw Sources/` for source material and source-of-truth inputs
- `01 Foundations/` for core concepts and fundamentals
- `02 AI Systems/` for system design topics like agents, MCP, RAG, memory, guardrails, and evals
- `03 Tools/` for tool-specific notes, especially Claude Code
- `04 Synthesis/` for cross-topic comparison and higher-level synthesis
- `05 Use Cases/` for practical reading paths and applied examples
- `_Templates/` for reusable note templates

Top-level navigation lives in:

- `Home.md` for the main reading paths
- `index.md` for the catalog view
- `AGENTS.md` for vault workflow and editing rules

## How to use

If you are reading the vault:

1. Start at `Home.md` for the main paths
2. Use `index.md` when you want to jump to a specific topic
3. Use the relevant MOC page before diving into individual notes

If you are editing the vault:

- keep raw sources in `00 Raw Sources/`
- keep derived knowledge in the numbered folders
- add or update cross-links when a note belongs in more than one path
- prefer existing notes and MOCs over creating duplicates

## Git and Obsidian behavior

This repo intentionally ignores machine-specific files such as:

- `.DS_Store`
- `.obsidian/`

That means Git should track the knowledge content, not local editor state.

## Conventions

- MOC pages act as entry points for each section
- numbered notes are ordered learning paths
- synthesis notes connect multiple topics
- use cases focus on practical application

## Useful entry points

- `Home.md`
- `index.md`
- `AGENTS.md`
- `Vault Standards - Note Lifecycle.md`
- `Vault Standards - Properties.md`
- `Vault Workflow - Capture to Evergreen.md`
- `Glossary - AI Systems.md`

## Notes

This repository is a living knowledge base. Some notes are evergreen reference material, while others are drafts or working notes that may evolve over time.

## Contributing

When adding or editing notes:

- keep raw sources in `00 Raw Sources/`
- keep derived notes in the numbered folders
- update MOCs and cross-links when a topic belongs in more than one path
- avoid duplicating notes when a merge into an existing page is enough
- keep machine-specific Obsidian state out of git

If you are using this vault on another machine, you should be able to clone the repo and open it directly in Obsidian without carrying local workspace state.
