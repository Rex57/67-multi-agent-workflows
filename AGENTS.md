# Repository AGENTS

## Purpose

This file is the canonical operating contract for agents working in this repository. Claude Code, Codex, Gemini CLI, and optional workflow layers such as Superpowers should all follow this file and treat any CLI-specific entry files as thin wrappers around the same shared system.

## Mandatory Read Order

1. `.agents/docs/PROJECT_MEMORY.md`
   - always read the first section first
   - treat it as the live learning log for mistakes, tool usage notes, and durable gotchas
2. `.agents/README.md`
3. `.agents/docs/PROJECT_STANDARDS.md`
4. `.agents/docs/SYSTEM_MAP.md`
5. `.agents/docs/PROJECT_ROADMAP.md` when roadmap or milestones matter
6. If Superpowers artifacts exist, read the relevant approved files before implementation:
   - `docs/superpowers/specs/*`
   - `docs/superpowers/plans/*`
7. `README.md` if framework context is still needed

## Superpowers Compatibility

If Superpowers is installed in the target project:

- use Superpowers for brainstorming, spec writing, detailed implementation plans, and execution flow
- treat `docs/superpowers/specs/*` and `docs/superpowers/plans/*` as task artifacts
- treat `.agents/docs/*` as the durable long-term memory and project context layer
- copy durable lessons, architectural decisions, constraints, and validation notes from Superpowers artifacts into `.agents/docs/*` when they should persist beyond a single spec or plan

Superpowers artifacts help the agent execute the current initiative. `.agents/docs/*` preserve what future sessions should know even after a branch, spec, or plan is no longer front and center.

## Task Handling

- Initialize or reset the docs when the project state is missing or stale.
- Scope requests directly in the relevant docs before implementation when needed.
- Implement the requested change directly.
- Audit or simplify in small validated batches.
- Sync framework files carefully.

## Core Implementation Behavior

Before changing files:

1. Identify the target surface, subsystem, or task.
2. Classify the change:
   - implementation
   - architecture
   - docs or process
   - validation or deployment
3. Determine what must remain stable by default:
   - public APIs
   - routes or entrypoints
   - data contracts
   - provider or state wiring
   - auth, billing, or persistence flows
4. Check the owning docs before editing code or project instructions.

While implementing:

- Prefer the smallest coherent change that satisfies the request.
- Use repo-native commands, tests, and formatters.
- If the active CLI supports delegation, delegate only bounded, non-overlapping work.
- If the active CLI does not support delegation, complete the task sequentially in the main session.
- Keep docs in sync in the same task whenever behavior or process changes.

## Documentation Behavior

Update the file that owns the truth:

- `.agents/docs/PROJECT_STANDARDS.md`: engineering rules, validation rules, UI rules, forbidden patterns
- `.agents/docs/PROJECT_MEMORY.md`: durable context, decisions, incidents, and the top-section learning log
- `.agents/docs/SYSTEM_MAP.md`: feature-to-code wiring, routes, services, dependencies
- `.agents/docs/PROJECT_ROADMAP.md`: phases, milestones, current priorities

When Superpowers is present:

- specs stay in `docs/superpowers/specs/*`
- plans stay in `docs/superpowers/plans/*`
- durable memory stays in `.agents/docs/*`

## Learning Behavior

Capture durable lessons in the first section of `PROJECT_MEMORY.md` when a task reveals:

- repeated mistakes
- root causes
- tooling quirks
- validation gaps
- architecture traps
- user preference patterns
- commands or tool usage notes future agents should not rediscover

Each note should say what happened, why it mattered, and what to do next time.

## Validation Behavior

Minimum validation after non-trivial changes:

1. Format touched files with the repo's formatter.
2. Run lint or analyze for the affected area.
3. Run targeted tests.
4. Run a broader smoke or integration check if the change crosses subsystem boundaries.

If validation cannot be run, state exactly why and record the gap in `PROJECT_MEMORY.md`.

## Reporting Behavior

Prefer a concise report with:

- what changed
- what was preserved
- docs updated
- validation run
- risks or follow-ups

## Success Definition

A task is complete when:

1. the requested change is implemented or intentionally scoped
2. documentation is updated
3. validation ran or the gap is explicit
4. the final report is concrete about outcome and remaining risk
