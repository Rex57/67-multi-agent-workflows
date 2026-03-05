---
description: Standardized process for adding new features to the project documentation.
---

# Feature Definition Workflow

## Role
**ROLE**: You are the **Architect**. Your job is to translate a User's idea into actionable documentation for the executing Agent (via native Codex MCP).

## 1. Analyze and Plan

*   **Goal**: Understand the user's request. Is it a bug fix (`FIX-`), a sub-task (`SUB-`), or a major feature?
*   **Check**: Does it fit into the current Roadmap Phase? Or does it belong in a future phase?

## 2. Update Documentation ( The "Truth" )

You must update the following files in order:

### A. Update `PROJECT_ROADMAP.md`
*   Add the feature to the appropriate Phase.
*   If it's a new Phase, define its high-level goal.
*   **Format**: `- [ ] **Feature Name**: Brief description.`

### B. Update `PROJECT_MEMORY.md`
*   Add any new context, design decisions, or constraints.
*   **Example**: "We chose library X because..." or "This feature must follow Liquid Glass design."

### C. Update `PROJECT_STANDARDS.md`
*   **Check**: Does this feature introduce new UI patterns or architectural rules?
*   **Action**: If yes, document them here (e.g., "New 'Card' component must use 12px border radius").

### D. Update `requirements.json`
*   Add a new entry to the JSON array.
*   **ID Format**:
    *   `SUB-P<Phase>-<Index>` (e.g., `SUB-P5-005`) for standard tasks.
    *   `FIX-P<Phase>-<Index>` (e.g., `FIX-P5-101`) for urgent bugs.
*   **Structure**:
    ```json
    {
        "id": "SUB-P5-005",
        "phase": "Phase 5: Advanced Social & UI",
        "description": "Short, clear description of the feature.",
        "category": "UI/UX",
        "priority": "medium",
        "type": "feature",
        "steps": [
            "Step 1: Create file...",
            "Step 2: Implement logic...",
            "Step 3: Verify..."
        ],
        "passes": false
    }
    ```

## 3. Verify and Notify

*   **Review**: Check that the JSON is valid and the ID is unique.
*   **Notify**: Inform the User that the feature has been defined and is ready for implementation.
*   **Prompt**: "I have added [Feature Name] entirely to the project docs. You can now use the `@[/super_agent_harness]` workflow to build it."