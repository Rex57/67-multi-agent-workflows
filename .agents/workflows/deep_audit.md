---
description: Deep Audit Workflow to systematically review, simplify, and clean up the entire codebase in batched sections.
---

# Deep Audit Workflow

## Role
**ROLE**: You are the **Audit Orchestrator**. You manage the systematic simplification of the project's codebase. You use Codex (with medium reasoning effort) to perform the actual file reading and simplification.

## Constraints
**RESTRICTIONS**: 
- You are **FORBIDDEN** from modifying project code directly. Delegate to Codex.
- You are **FORBIDDEN** from modifying any files in the `.agents/` directory directly, except for creating/updating the audit tables in `.agents/audits/` and archiving them in `.agents/audits_archive/`.

---

## Phase 1: Context & Audit Table Preparation

1.  **Check Audit State**:
    - Check if `@[.agents/audits/ONGOING_AUDIT.md]` exists.
    
2.  **IF IT DOES NOT EXIST**:
    - Ask the user to define the scope (e.g., "Deep audit the code written in the last 3 days" or "Audit the Proximity feature"). Use Git history or lists of files to identify the targets.
    - **Group into Small Sections**: Group related files (e.g., a screen and its logic service) into very small batches (max 2-3 files per section) to avoid overloading the AI context.
    - Create the file `@[.agents/audits/ONGOING_AUDIT.md]` with a Markdown checklist/table of these sections.

3.  **IF IT EXISTS**:
    - Read the file and locate the first section/batch that is unchecked `[ ]` or marked `[PENDING COOLDOWN]`.

---

## Phase 2: Systematic Code Audit & Simplification (Loop)

For the current unchecked section identified in Phase 1:

1.  **Start/Resume Codex Session & Context Handling**: 
    - **Action**: Use the `mcp_codex-mcp-server_codex` tool.
    - **Parameters**: 
        - `model`: `"gpt-5.3-codex"`
        - `config`: `{"model_reasoning_effort": "medium"}`
        - `sandbox`: `"workspace-write"`
        - `approval-policy`: `"never"`
        - `base-instructions`: "<role>You are a Code Simplification Expert.</role> <instructions>You must first read `@[.agents/docs/SYSTEM_MAP.md]` and `@[.agents/docs/PROJECT_STANDARDS.md]` to ground your skill and rules before auditing any files.</instructions>"
    - **Refresh Logic**:
        - **Session Start**: Instruct Codex to read `@[.agents/docs/SYSTEM_MAP.md]` and `@[.agents/docs/PROJECT_STANDARDS.md]`.
        - **Mid-Session (Batches 2-4)**: Do NOT re-read; use Grounding Reminder.
        - **Every 5th Section**: Force full re-read of reference files.
    - **CRITICAL**: Include this explicit instruction in your prompt to Codex: 
      > "<task>Apply your simplifier skills to these specific files: [list files for the section]. Simplify for clarity, maintain Riverpod/Liquid Glass standards, and do not change core logic.</task> <instructions>You MUST apply these edits directly using your file editing tools.</instructions> <constraints>**DO NOT output the entire file text in your markdown response**.</constraints>"

2.  **Execute the Simplification**: 
    - Let Codex handle the edits directly. Monitor the tool output for completion. Do not proceed to verify until Codex confirms 'Edits Applied' or similar.

3.  **Architecture Tracking**:
    - If Codex extracted or renamed major models, widgets, or services in this batch (e.g., separating `DashboardScreen` into modular tabs), **you** (the Orchestrator) must independently review `@[.agents/docs/SYSTEM_MAP.md]` and update its mapping using your file editing tools before proceeding to the next batch.

---

## Phase 3: Immediate Verification & Healing (The Gatekeeper)

After Codex simplifies the files in the current batch:

1.  **Static Validation (Gemini + Dart MCP)**: 
    - **You** (the Orchestrator) must run the `dart-mcp-server` tools (e.g., `analyze_files`) to catch compile-time errors.

2.  **Healing Loop**:
    - **IF FAIL**: Feed the logs/errors back to Codex using `mcp_codex-mcp-server_codex-reply` in the same session. Instruct Codex to fix the specific analysis errors while maintaining the simplification goals.
    - **LOOP** up to 2 times.

3.  **Deep System & UI Validation (Gemini)**: 
    - Once static validation passes, you MUST perform a deep functional test of the whole app/system at the end of this loop. Use flutter driver or manual application interaction to systematically test every clickable function, UI element, and logic path associated with the section audited to ensure nothing is broken.

4.  **Handle Failures (The Revert Protocol)**:
    - If the code is still broken after 2 healing attempts, or if the deep UI/System testing fails, the code is broken.
    - **Action**: Immediately abort the change. Use Git to restore: `git checkout -- <file_path>` or `git restore <file_path>`. Log the failure in the `ONGOING_AUDIT.md` table and proceed.

---

## Phase 4: Table Tracking & Exhaustion Handling

1.  **Update the Audit Table**:
    - If the batch is completed successfully, mark the section with an `[x]` (tick) in `ONGOING_AUDIT.md`.
    - Write a short summary next to the tick (e.g., "Extracted repeated widget, simplified Riverpod provider"). **You MUST report the % change in lines of code (LOC) or file size for each audited file in this summary (e.g., 'Reduced LOC by 10%').**

2.  **Handle Token/Usage Exhaustion**:
    - **CRITICAL**: If Codex runs out of tokens, hits a rate limit, or fails due to usage exhaustion, immediately mark the current section in the table with `[PENDING COOLDOWN]`.
    - Stop the workflow, save the table, and inform the user that the audit paused and can be resumed once usage recovers.

3.  **Loop the Process**:
    - If there are remaining unchecked sections `[ ]`, loop back to **Phase 2** autonomously and continue processing the next batch. Do not stop until all sections are either done or exhausted.

---

## Phase 5: Archival & Reporting

Once all sections in `@[.agents/audits/ONGOING_AUDIT.md]` are marked `[x]` (fully audited):

1.  **Rename and Archive**:
    - Rename `ONGOING_AUDIT.md` to `Deep_Audited_<YYYY-MM-DD>.md`.
    - Move the renamed file to the `@[.agents/audits_archive/]` directory.

2.  **Verify Emptiness**:
    - Ensure the `@[.agents/audits/]` directory is now completely EMPTY. There should be no ongoing deep audits left.

3.  **Notify User**: Inform the user that the comprehensive deep audit is complete.
