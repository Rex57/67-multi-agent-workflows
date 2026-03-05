# Project Memory

Long-term strategic memory and historic context for the Gemini Codex Multi-Agentic Framework.

## 1. Project Strategy
- **Core Framework**: Protytype Multi-Agentic orchestration using Gemini (Orchestrator) and Codex (Builder).
- **Communication Protocol**: Model Context Protocol (MCP) for tool binding.

## 2. Design Law
- Follows the "Liquid Glass UI" standards (Radius 32) as specified in `PROJECT_STANDARDS.md`.

## 3. Business Logic
- Multi-agent handoffs between Gemini and Codex to ensure code quality through a "Plan -> Code -> Verify" lifecycle.

## 4. Feature Blueprint
- **Super-Agent Harness**: Automated feature implementation.
- **Deep Audit**: Automated code simplification and refactoring.

## 5. Implementation History
### March 2026
- Initial documentation of Codex MCP rules and Agents SDK integration patterns.
- Verification of `codex-cli` v0.107.0 as the primary Builder tool.

## 6. Security Protocol
- No secrets allowed in the `.agents` folder.
- Guardrails implemented via MCP approval policies.

## 7. Lessons Learned & Discoveries
- **Discovery**: The `codex-mcp-server` relies on the `codex` command being globally available via `npm install -g @openai/codex-cli`.
- **Fix**: Verified that `codex --version` is the reliable way to check health before starting an orchestration run.
- **Gotcha**: Sessions in Codex are maintained via a `threadId` (or `thread_id` depending on API version). Always store and pass this ID to maintain state across multiple turns in a single task.
