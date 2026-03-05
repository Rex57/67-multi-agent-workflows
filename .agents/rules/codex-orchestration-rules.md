---
description: "Guidelines for Codex MCP Server & Agents SDK Integration"
trigger: "mcp_usage, orchestration_task"
---

# 🤖 Codex MCP & Agents SDK Rules

This file documents the standards for using the Codex MCP server and integrating the patterns from the OpenAI Agents SDK within the Gemini Codex Multi-Agentic Framework.

## 🛠️ 1. Codex MCP Server Management

### ✅ Installation & Health Check
Before using Codex as a Builder, verify the connection:
- **Command**: `codex --version`
- **MCP Verification**: Ensure `codex-mcp-server` is listed in `mcp_config.json` with the command `codex`.
- **Manual Install/Update**: If `codex` is missing, install it via:
  ```bash
  npm install -g @openai/codex-cli
  ```

### 🧰 Available Tools (Tool-Specific Usage)
When calling Codex tools outside of predefined workflows, adhere to these parameter standards:

#### `codex` (The Main Builder)
Use this for starting new implementation tasks or complex logic runs.
- **`prompt`**: Provide clear, high-level goals.
- **`approval-policy`**: 
  - `untrusted`: Default for new code.
  - `on-failure`: Used during debugging loops.
  - `never`: Only for read-only or low-risk tasks.
- **`sandbox`**: 
  - `workspace_write`: Required for the Builder role to modify files.
  - `read_only`: Used for data extraction or audits.
- **`model`**: Defaults to the optimized Codex engine for the current session.

#### `codex-reply` (The Session Handler)
Use this to continue a conversation without losing context.
- **`threadId`**: ALWAYS pass the active thread ID obtained from the initial `codex` call.
- **`prompt`**: Specific follow-up instructions (e.g., "Fix the lint error on line 42").

---

## 🏗️ 2. OpenAI Agents SDK Standards
Based on the [OpenAI Agents SDK Documentation](https://developers.openai.com/codex/guides/agents-sdk), our framework adopts these core patterns:

### 🎭 Agent Profiles
Each agent in this framework is defined by:
- **Instructions**: A unique set of rules (like this file).
- **Tool Access**: Only the MCP servers required for its specific role.
- **Handoff Logic**: The ability to delegate to other roles (e.g., Gemini handing off to Codex).

### 🤝 Handoff Protocol
When one agent needs to coordinate with another:
1.  **Context Passing**: The orchestrator (Gemini) must provide a full summary of the current workspace state.
2.  **Explicit Delegation**: Use phrases like "Handing off to Builder [Codex] for implementation" to signal state transitions.
3.  **Return Gates**: The Builder must signal completion so the Gatekeeper (Gemini) can initiate verification via `dart-mcp-server`.

---

## 🚦 3. Operating Laws for Multi-Agent Workflows
- **Statelessness**: Assume each new `codex` call might be a fresh start unless a `threadId` is used.
- **Verification First**: NEVER accept a Codex output as "final" until verified by the `dart-mcp-server` diagnostics.
- **Atomic Commits**: Codex should aim for small, atomic changes that are easily verifiable.
- **Grounding Requirement**: Every Codex run MUST cite the specific section of `PROJECT_STANDARDS.md` it is adhering to.
