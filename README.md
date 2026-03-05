# Gemini Codex Multi-Agentic Framework (Prototype)

> [!IMPORTANT]
> This project is a **prototype** and is currently designed to work exclusively with **Codex as an MCP-server**.

Welcome to the **Gemini Codex Multi-Agentic Framework**. This repository contains the core logic, standards, and orchestration engines for AI-assisted development. 

Please note: This is not a "Super AI Agentic Framework." It is a specialized **Gemini Codex Multi-Agentic Framework** designed for high-precision code orchestration.

It is designed to be a standalone, reusable "Brain" that can be dropped into any project.

## Structure
- `workflows/`: The automation engines (step-by-step guides for the AI).
- `rules/`: The operating laws that govern AI behavior.
- `README.md`: The central map and instruction book for the agents.
- `docs/`: Template files for project-specific memory, standards, system maps, and roadmaps.

## How to use in your project
1. Clone this repository or copy the `.agents` folder into your project root.
2. Initialize the project-specific documents in the `docs/` folder (or run the `/init_project` workflow).
3. The AI agents will automatically read the `README.md` and adhere to the orchestrated workflows.
