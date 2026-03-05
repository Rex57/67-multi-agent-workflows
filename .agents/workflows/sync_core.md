---
description: Synchronizes the core agent Framework (Workflows, Rules, and README) from the Multi-Agentic Workflows upstream repository without overwriting local project documentation.
trigger: User explicitly requests to update the agent framework or calls /sync_core.
---

# Sync Core Framework (Maintenance Mode)

## Goal
To retrieve the latest core instructions, automation logic, and rules from the Multi-Agentic Workflows repository while preserving project-specific documentation and state.

## Constraints
- **PRESERVE**: You MUST **NEVER** overwrite `docs/`, `requirements.json`, or `progress.txt`.
- **UPDATE**: You only sync the "Engines" (`workflows/`), "Police" (`rules/`), and the framework map (`README.md`).

---

## Step 1: Clone the Multi-Agent Framework
1. Run a command to temporarily clone the Multi-Agent framework repository to an external temporary directory.
   - **Command**: `git clone https://github.com/Rex57/67-multi-agent-workflows.git "$env:TEMP\multi-agent-framework"`
   - *Note: If the directory exists, run `Remove-Item -Recurse -Force "$env:TEMP\multi-agent-framework"` first.*

## Step 2: Synchronize Core Logic
1. Copy the updated engines and rules into the current project's `.agents/` directory.
2. **Action**: Use the following commands to sync ONLY core files:
   ```powershell
   # Sync Workflows (Engines)
   Copy-Item -Path "$env:TEMP\multi-agent-framework\.agents\workflows\*" -Destination ".agents\workflows" -Recurse -Force
   
   # Sync Rules (Police)
   Copy-Item -Path "$env:TEMP\multi-agent-framework\.agents\rules\*" -Destination ".agents\rules" -Recurse -Force
   
   # Sync Main Entry Point
   Copy-Item -Path "$env:TEMP\multi-agent-framework\.agents\README.md" -Destination ".agents\README.md" -Force
   ```

## Step 3: Validation & Cleanup
1. **Cleanup**: Remove the temporary cloned repository.
   - **Command**: `Remove-Item -Recurse -Force "$env:TEMP\multi-agent-framework"`
2. **Knowledge Refresh**: Read the newly synced `.agents/README.md` to identify any new tools, workflows, or standards.
3. **Report**: Inform the user that the synchronization is complete and summarize any major changes found in the updated `README.md`.
