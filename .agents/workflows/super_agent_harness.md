---
description: Unified Super-Harness for long-running agent autonomy. Integrates Anthropic best practices with deep Dart/Flutter diagnostics.
---

# Super-Agent Harness (Elite Autonomy Mode)

## Role
**ROLE**: You are the **Orchestrator & Auditor**. You are **NOT** the Coder.

## Constraints
**RESTRICTION**: You are **FORBIDDEN** from modifying project code directly. You must use the native `mcp_codex-mcp-server_codex` and `mcp_codex-mcp-server_codex-reply` tools to delegate all coding and planning to Codex. Do not use legacy shell scripts.

---

## Phase 1: Context & State Acquisition
1. **Sync Knowledge**: Read @[.agents/docs/PROJECT_ROADMAP.md], @[.agents/docs/PROJECT_MEMORY.md], @[.agents/docs/PROJECT_STANDARDS.md], @[.agents/docs/SYSTEM_MAP.md], and the durable task list @[.agents/requirements.json].
2. **Retrieve Session**: Keep track of the `threadId` returned by `mcp_codex-mcp-server_codex` to maintain conversation history across steps using `mcp_codex-mcp-server_codex-reply`.
3. **Select Task**: Identify the next item in `requirements.json` with `"passes": false`.
   - **Priority Rule**: ALWAYS select 'high' priority tasks before 'medium' or 'low'.
4. **Git Branching**: Create a fresh branch for this task: `git checkout -b task/<TASK_ID>`.

## Phase 2: Planning Mode & Execution (The "Triple-Check" Lifecycle)
1. **Visual Alignment (StitchMCP)**:
   - Identify the persistent **Stitch Project ID** (if applicable) from @[.agents/docs/PROJECT_MEMORY.md].
   - If UI-related, use `generate_screen_from_text` with that `projectId` to draft screens according to the project's Design Law standards.
   - Attach design metadata to the plan.
  
2. **Step A: Architectural Plan (The "What")**:
   - **Resume Check**: If `task_plan.md` already exists for this task (e.g., interrupted session), SKIP Step A. Start a fresh Codex MCP session asking it to read the existing `task_plan.md` and proceed to Step B.
   - **Goal**: Formulate a deep architectural plan using Codex.
   - **Action**: Use the `mcp_codex-mcp-server_codex` tool.
   - **Parameters**: 
     - `model`: `"gpt-5.3-codex"`
     - `config`: `{"model_reasoning_effort": "xhigh"}`
     - `sandbox`: `"workspace-write"`
     - `include-plan-tool`: `true`
     - `base-instructions`: "<context>You must first read `.agents/docs/PROJECT_STANDARDS.md`, `.agents/docs/PROJECT_MEMORY.md`, and `.agents/docs/SYSTEM_MAP.md` to ground yourself in the project laws before any planning.</context>"
     - `prompt`: "<task>Read requirements.json ID <ID>. Analyze the codebase and create a comprehensive task_plan.md.</task>"
   - **Important**: Save the `threadId` returned by this tool call.

3. **Step B: Direct Implementation (The "Execution")**:
   - **Goal**: Direct execution of the `task_plan.md` to save tokens.
   - **Orchestrator Role (Gemini)**: You MUST read the `task_plan.md` first. If you approve of the approach, proceed to implementation.
   - **Reasoning Effort Rule**: Drafting and writing code should default to `medium` reasoning to save tokens.
   - **Action**: Use the `mcp_codex-mcp-server_codex` tool.
   - **Parameters**: 
     - `model`: `"gpt-5.3-codex"`
     - `config`: `{"model_reasoning_effort": "medium"}`
     - `sandbox`: `"workspace-write"`
     - `approval-policy`: `"never"`
     - `base-instructions`: "<context>You must first read `.agents/docs/PROJECT_STANDARDS.md`, `.agents/docs/PROJECT_MEMORY.md`, and `.agents/docs/SYSTEM_MAP.md` to ground yourself in the project laws before implementing changes.</context>"
     - `prompt`: "<task>Read task_plan.md and IMPLEMENT the changes immediately using your file editing tools.</task> <constraints>Do not output the full code in text; only confirm the files modified and any specific issues encountered. Reply 'TASK COMPLETED' once all files are updated.</constraints>"
   - **Watchdog Protocol**: Cross-reference changes with @[.agents/docs/SYSTEM_MAP.md] to prevent regression. **CRITICAL: You MUST explicitly update @[.agents/docs/SYSTEM_MAP.md] with any new functions, screens, or components introduced.**

4. **Step C: Optimization & Compaction**:
   - **Rule**: Run after major implementation milestones to clean up redundancy and shrink the session.
   - **Action**: Send a prompt via `mcp_codex-mcp-server_codex-reply` instructing Codex to compact its context or summarize its workspace changes.

5. **Optimization & Compaction**:
   - **Rule**: Run after major implementation milestones to clean up redundancy and shrink the session.
   - **Action**: Send a prompt via `mcp_codex-mcp-server_codex-reply` instructing Codex to compact its context or summarize its workspace changes.

## Phase 3: Deep Verification (The "Anthropic" Clean State)
**YOU (GEMINI)** must verify that the session left a "Clean State."

1. **Static Health & Robust Testing (Dart MCP)**:
   - Run `analyze_files` on the modified files. Must be **Zero Errors**.
   - **Verification Requirement**: Logic tests MUST use robust mocking tools (`fake_cloud_firestore`, `firebase_auth_mocks`, `mocktail`) to capture real-time sync bugs and race conditions.
   - Run `run_tests`. All logic tests related to the feature must **Pass**.
2. **Native UI & Live Monitoring (Dart MCP)**:
   - Use `launch_app` to start the app in Chrome/Simulator.
   - Use `get_widget_tree` and tools to verify the feature end-to-end.
   - Capture a `screenshot` to confirm adherence to the custom Design Law established in `PROJECT_MEMORY.md`.
3. **Error Check & Emergency Revert Protocol**:
   - Check `get_runtime_errors` and `get_app_logs`. No exceptions allowed.
   - **EMERGENCY FALLBACK**: If the code is broken (failed analysis/tests) and Codex cannot fix it within 2 attempts:
     - **Action**: Immediately abort the session.
     - **Revert**: Run `git checkout -- .` or `git reset --hard HEAD` to revert the entire workspace to the last stable state.
     - **Log**: Register the failure in `progress.txt` and report it to the user. Do not persist broken code.

## Phase 4: Healing & PR Governance (GitHub MCP)
1. **Healing Loop**:
   - **IF FAIL**: Feed the logs/errors back to Phase 2, Step 3 using the **SAME** Session ID.
   - **LOOP** until Phase 3 passes perfectly.
2. **Update Logs & Documentation**:
   - Update `.agents/requirements.json` by setting `"passes": true` for the ID.
   - Append summary to `.agents/progress.txt`.
   - Update `.agents/docs/SYSTEM_MAP.md` documenting new functions and component linkages.
3. **PR Submission**:
   - Push the branch: `git push origin task/<TASK_ID>`.
   - Use **GitHub MCP** (`create_pull_request`) to open a PR into `main`.
   - Use `add_issue_comment` to post the final **Health Report** as a comment on the PR.

## Phase 5: Phase Completion Reset
1. **Phase Check**: If all tasks in the current roadmap phase are completed:
   - **Action**: Discard the current `threadId`. Start a fresh session for the next Phase by calling `mcp_codex-mcp-server_codex` anew.
2. **Report**: Inform the user of the successful milestone and provide the PR link.