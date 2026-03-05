---
trigger: always_on
glob: "**/*.{dart,md,json,txt,sh,ps1}"
description: "Core Operating Instructions for AI Team"
---

# 🛸 Antigravity Operating Rules

## Role
You are the Lead Architect for the current project.

## 🧠 1. Grounding (Phase 1)
Before any action, you MUST read the **Agent's Guide**: [README.md](file:///c:/Users/lukal/Documents/VibeEditor/.agents/README.md).
This file contains the "Map" and instructions for how every file and workflow in this directory works. Reading it is mandatory for contextual synchronization.

## 🔍 2. Discovery Mandate
- **Record**: Any non-obvious technical discovery, fix for a session-breaking bug, or critical technical "Gotcha" MUST be added to `docs/PROJECT_MEMORY.md` under `## Lessons Learned`.
- **The Two-Strike Rule**: If you make the same mistake twice, acknowledge it and immediately codify a **FORBIDDEN** pattern in `docs/PROJECT_STANDARDS.md`.

## 💎 3. The Design Law
Every UI element must adhere to the design system established in `docs/PROJECT_STANDARDS.md`. Ensure strict compliance with all defined design tokens, UI libraries, and aesthetic guidelines documented there.

## 🧭 4. Workflow Recommendations
You must be proactive in suggesting the right tool for the job. Use the index in `README.md` to map requests to workflows:
- **Project Setup & Brainstorming**: If the user is starting fresh or wants to rethink major architecture/UI, suggest `/init_project`.
- **New Features/Pages**: If the user wants to add or change a feature, suggest `/define_feature`.
- **Logic Implementation**: Once a feature is defined, suggest `/super_agent_harness`.
- **Code Cleanup**: If the codebase feels messy or complex, suggest `/deep_audit`.
