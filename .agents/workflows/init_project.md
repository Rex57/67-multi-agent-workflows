---
trigger: always_on
glob: ".agents/workflows/init_project.md"
description: "Initializes a new project by brainstorming with the user and setting up core documentation."
---

# `init_project` Workflow

## Goal
This workflow is designed to brainstrom ideas with the user and create a new set of core project documentation: `PROJECT_ROADMAP.md`, `PROJECT_STANDARDS.md`, and `PROJECT_MEMORY.md`. It will keep asking the user questions to understand what the project will look like until it is 100% sure before writing anything to the three important files.

## Step 1: Brainstorming & Requirement Gathering
- Proactively ask the user questions to define the project. Ask about:
  1. The **Core Purpose** and features of the app/project.
  2. The **Tech Stack** to be used.
  3. The **Design Law** and UI/UX aesthetic (e.g., specific design systems, color palettes, border radius rules).
  4. Core **Business Logic** requirements.
- **Visual Drafts (Stitch MCP)**: During brainstorming, use `mcp_StitchMCP_create_project` to initialize a design workspace. Then, use `mcp_StitchMCP_generate_screen_from_text` to quickly draft visual previews of the requested UI aesthetic. Share these with the user and refine until the visual style is approved. The resulting Stitch Project ID will serve as the persistent design reference.
- Wait for user responses and iteratively refine the initial concept. Do not proceed to Step 2 until you have a detailed understanding of the app's architecture, design, and roadmap.

## Step 2: Drafting Core Documents
Once you are 100% sure about the project details, generate and update the following files based on the `.agents/README.md` conventions:
1.  **`docs/PROJECT_MEMORY.md`**: Document the Project Strategy, Design Law, Business Logic, and Feature Blueprint.
2.  **`docs/PROJECT_STANDARDS.md`**: Codify the core philosophy, workflow standards, tech stack mastery expectations, and testing/mocking guidelines.
3.  **`docs/PROJECT_ROADMAP.md`**: Create phase-based progress tracking from Phase 1 through Phase N.

## Step 3: Defining Actionable Tasks
Based on the finalized `PROJECT_ROADMAP.md`:
- Split the roadmap task into smaller, actionable component-level tasks.
- Overwrite **`requirements.json`** with these initial tasks formatted properly (e.g., ID, phase, description, priority, type, steps, passes). Do not inject tasks before the previous 3 documents are finalized.

## Conclusion
Notify the user that the project space is initialized and suggest the next best action from the roadmap using the appropriate workflow (e.g., `/super_agent_harness`).
