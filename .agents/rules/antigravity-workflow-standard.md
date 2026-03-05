---
trigger: always_on
glob: ".agents/workflows/*.md"
description: "Standards for creating and modifying AI workflows"
---

# 🛠️ Workflow Creation Standard

## Workflow Structure Rules
When building or modifying a workflow:
- **Instruction First**: You must read the master file `.agents/README.md` to know how and what is our standard. Additionally, read `docs/PROJECT_STANDARDS.md`.
- **Map Update**: If the workflow introduces new logic-to-UI connections, you MUST update `docs/SYSTEM_MAP.md`.
- **Central Index**: Every new workflow MUST be registered in the `.agents/README.md` index immediately.
- **Format**: Workflows must be `.md` files with YAML frontmatter describing the `description` and `trigger` logic.
- **Prompt vs. Markdown Structure**: You MUST use standard Markdown headers (`##`) for the file's structure. NEVER wrap entire sections of the markdown file itself in XML tags.
- **Agent Prompts**: You MUST use Anthropic-style XML tags (`<context>`, `<task>`, `<constraints>`) *inside* the strings that are passed as direct prompts or instructions to the LLM.
