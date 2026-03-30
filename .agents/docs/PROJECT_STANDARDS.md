# Project Standards

Project-specific engineering standards. Replace placeholders with the conventions of the target repository.

## Core Principles

- Prefer small, coherent changes over broad rewrites.
- Preserve stable interfaces unless the task explicitly changes them.
- Keep code, docs, queue state, and validation in sync.

## Architecture Rules

Document the patterns that should remain stable:

- preferred module boundaries:
- state or dependency injection rules:
- data access rules:
- integration boundaries:

## Implementation Rules

Capture the rules agents should follow by default:

- read the affected files before editing
- prefer existing project patterns over new abstractions by default
- use the repository's native formatters, linters, analyzers, and test tools
- keep shared instructions vendor-neutral unless a CLI-specific adapter is unavoidable

Add project-specific rules below this line.

## Validation Rules

Document the minimum validation bar for the target project:

- format touched files
- run lint or analyze on affected surfaces
- run targeted tests
- run broader smoke or integration checks when changes cross subsystem boundaries
- do not mark work complete with silent validation gaps

## Documentation Rules

Clarify what must be updated when work changes the system:

- keep long-lived lessons in the first section of `PROJECT_MEMORY.md`
- keep feature ownership and dependencies current in `SYSTEM_MAP.md`
- keep the roadmap and queue aligned with reality

## Forbidden Patterns

List the patterns agents should avoid:

- vendor lock-in in canonical instructions when a generic instruction would work
- broad rewrites without first scoping the affected surfaces
- hidden behavior changes made under the label of cleanup or refactor
- shipping changes without recording validation status
