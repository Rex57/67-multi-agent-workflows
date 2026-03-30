---
name: dart-code-simplifier
description: Simplifies and refines Dart or Flutter code for clarity, consistency, and maintainability while preserving exact behavior.
---

# Dart Code Simplifier

Use this skill for behavior-preserving cleanup and refactor work in Dart or Flutter codebases.

## Objective

Improve readability, structure, and maintainability without changing:

- public behavior
- routes or navigation targets
- state management wiring
- backend calls
- auth, billing, or persistence behavior

## Grounding

Before editing:

1. Read the relevant code files.
2. Read `.agents/docs/PROJECT_STANDARDS.md` and `.agents/docs/SYSTEM_MAP.md` when they exist.
3. If those docs are absent, infer the existing architecture from the codebase and preserve it.

## Apply These Rules

- Prefer clearer structure over clever compression.
- Remove dead code, unused imports, and redundant branches.
- Extract helpers or widgets when it reduces cognitive load without hiding important logic.
- Prefer early returns, clear naming, and explicit control flow.
- Keep dependency boundaries intact.
- Do not rewrite the architecture during cleanup.
- Document any durable lesson or repeated pitfall in `PROJECT_MEMORY.md`.

## Validation

- Format touched files.
- Run Dart or Flutter analysis on the affected area.
- Run targeted tests when available.
- If validation cannot run, state the gap explicitly.

## Output

Report:

- files changed
- simplifications made
- behavior preserved
- validation run
- any follow-up risk
