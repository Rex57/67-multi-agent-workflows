# CLI Multi-Agent System

This repository is a CLI-agnostic multi-agent operating system for software delivery. It is designed to be used from Claude Code, Codex, or Gemini CLI without assuming a single model vendor or orchestration product.

## Supported Entry Points

- `AGENTS.md`: canonical shared instructions
- `CLAUDE.md`: Claude Code bootstrap
- `GEMINI.md`: Gemini CLI bootstrap

## Repository Structure

- `.agents/README.md`: framework map and operating cycle
- `.agents/docs/`: project memory, standards, system map, and roadmap
- `skills/`: reusable specialist prompts and CLI adapters

## Operating Model

- `AGENTS.md` is the only canonical operating contract.
- The first section of `.agents/docs/PROJECT_MEMORY.md` is mandatory reading on every task.
- The durable system memory lives in `.agents/docs/*`.
- There are no separate `.agents/rules`, `.agents/workflows`, audit folders, queue files, or progress logs.

## Superpowers Long-Term Memory Support

This system is designed to work alongside Superpowers.

Use the two layers for different jobs:

- `docs/superpowers/specs/*`: brainstormed and approved specs
- `docs/superpowers/plans/*`: detailed implementation plans
- `.agents/docs/*`: durable long-term memory, standards, system map, and roadmap

Recommended pattern:

1. Let Superpowers generate and maintain the current spec and plan.
2. Keep durable lessons, architecture decisions, validation notes, and project constraints in `.agents/docs/*`.
3. Update `.agents/docs/PROJECT_MEMORY.md` when something should survive beyond the current spec, plan, or branch.

## How To Use

1. Start from your CLI entry file:
   - Codex: `AGENTS.md`
   - Claude Code: `CLAUDE.md`
   - Gemini CLI: `GEMINI.md`
2. Read the first section of `.agents/docs/PROJECT_MEMORY.md`.
3. Read `.agents/README.md` and continue with `AGENTS.md`.
4. If Superpowers artifacts exist, read the relevant spec and plan in `docs/superpowers/`.
5. Update `.agents/docs/*` as the task evolves.

## Notes

- The system is intentionally plain Markdown so different CLIs can consume it with minimal adaptation.
- Superpowers can drive the active workflow, while `.agents/docs/*` act as the repo's long-term memory layer.
