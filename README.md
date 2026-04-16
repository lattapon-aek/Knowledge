# Knowledge Vault

![Vault](https://img.shields.io/badge/Vault-Obsidian-blueviolet)
![Content](https://img.shields.io/badge/Content-Markdown-brightgreen)
![Scope](https://img.shields.io/badge/Scope-AI%20Systems-informational)

Obsidian knowledge vault for AI systems, LLMs, agents, prompting, and tooling.

This repo is designed to stay portable:

- knowledge content is tracked in git
- machine-specific Obsidian state is ignored
- the vault can be opened on another machine without carrying local UI state

## Start Here

- `Home.md` for the main reading paths
- `index.md` for the catalog view
- `AGENTS.md` for vault workflow and editing rules

## Structure

- `00 Raw Sources/` source material and source-of-truth inputs
- `01 Foundations/` core concepts and fundamentals
- `02 AI Systems/` agents, MCP, RAG, memory, guardrails, evals
- `03 Tools/` tool-specific notes, especially Claude Code
- `04 Synthesis/` cross-topic comparison and higher-level synthesis
- `05 Use Cases/` practical reading paths and applied examples
- `06 Engineering/` implementation, frameworks, coding notes, and subdomains like RAG, Guardrails, Evals, MCP, and Memory
- `_Templates/` reusable note templates
  - includes [Agent Brief - Vault](_Templates/Agent%20Brief%20-%20Vault.md) for strict layer-preserving agent instructions

## How to Use

- Start with `Home.md` when you want the main paths
- Use `index.md` when you want a faster catalog view
- Open the relevant MOC before diving into individual notes

## Conventions

- MOC pages are entry points
- numbered notes are ordered learning paths
- synthesis notes connect multiple topics
- use cases focus on practical application
- raw sources stay in `00 Raw Sources/`

## Contributing

- keep raw sources separate from derived notes
- update MOCs and cross-links when a topic belongs in more than one path
- prefer merging into an existing note over creating duplicates
- keep `.obsidian/` state out of git
