# Shared Skills

These skills are reusable specialist prompt files. They are written to be readable from Claude Code, Codex, or Gemini CLI.

## Usage

- Codex or any agent with skill-loading can consume `SKILL.md` directly.
- Claude Code and Gemini CLI can use the same `SKILL.md` as a scoped reference prompt.
- CLI-specific adapter notes live next to the skill when needed.

## Rules

- Keep the skill core vendor-neutral.
- Put adapter or launcher text in `adapters/`.
- Reference repo docs such as `.agents/docs/*` when they exist, but define a fallback when they do not.

## Current Skills

- `dart-simplifier`: behavior-preserving Dart and Flutter cleanup
