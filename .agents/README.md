# .agents Framework Map

This directory holds the durable project state for the shared CLI system.

## Directory Map

```text
.agents/
|-- docs/                   # Long-lived project truth
|   |-- PROJECT_MEMORY.md
|   |-- PROJECT_STANDARDS.md
|   |-- SYSTEM_MAP.md
|   `-- PROJECT_ROADMAP.md
`-- README.md               # This file
```

## Read First

1. `.agents/docs/PROJECT_MEMORY.md`
   - always read the first section first
   - use it to avoid repeating mistakes, tool issues, and validation gotchas
2. `../AGENTS.md`
3. the other docs relevant to the task
4. If present, the relevant Superpowers artifacts:
   - `../docs/superpowers/specs/*`
   - `../docs/superpowers/plans/*`

## Source Of Truth

- `.agents/docs/PROJECT_STANDARDS.md`: engineering and quality rules
- `.agents/docs/PROJECT_MEMORY.md`: durable context, history, and the learning-first section
- `.agents/docs/SYSTEM_MAP.md`: feature and system ownership plus dependencies
- `.agents/docs/PROJECT_ROADMAP.md`: phase plan and priorities

When Superpowers is present:

- `docs/superpowers/specs/*` hold brainstorm and approved design artifacts
- `docs/superpowers/plans/*` hold detailed implementation plans
- `.agents/docs/*` hold the long-term project memory that should survive beyond the current spec or plan

## Standard Operating Cycle

1. Ground:
   - read the first section of `.agents/docs/PROJECT_MEMORY.md`
   - read `../AGENTS.md`
   - read the docs relevant to the task
   - if present, read the active Superpowers spec and plan
   - inspect local files before deciding
2. Scope:
   - confirm the target change, surface, dependencies, and validation path
3. Execute:
   - implement directly or delegate bounded work if the CLI supports it
4. Verify:
   - run repo-native validation
   - resolve failures before marking complete
5. Record:
   - update the owning docs
   - keep durable memory in `.agents/docs/*`
6. Report:
   - summarize what changed, what was preserved, and validation status

## Recovery Guidance

- Prefer targeted fixes over broad reverts.
- Use destructive recovery only when explicitly approved by the user or already allowed by the local repo policy.
- Record durable lessons in the first section of `.agents/docs/PROJECT_MEMORY.md`.

## Notes

- There are no separate rules or workflow directories in this system.
- Shared operating behavior lives in `../AGENTS.md` plus the files inside `.agents/docs/`.
