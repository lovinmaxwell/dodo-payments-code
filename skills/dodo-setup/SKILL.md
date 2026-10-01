---
name: dodo-setup
description: Install and verify Dodo Payments MCP (API Code Mode + Knowledge) via mcp-remote, complete OAuth/API key setup, and confirm tools. Use before first Dodo Payments task or when MCP/auth fails.
---

# Dodo Payments setup

Use this skill before the first Dodo Payments task, or whenever the MCP servers are missing or authentication fails.

## Scope

- Official remote MCP endpoints:
  - API / Code Mode: `https://mcp.dodopayments.com/mcp`
  - Knowledge (docs): `https://knowledge.dodopayments.com/mcp`
- Upstream: [dodopayments/dodo-agent-plugin](https://github.com/dodopayments/dodo-agent-plugin) · docs: [MCP server](https://docs.dodopayments.com/developer-resources/mcp-server)
- Requires **Node.js ≥ 18** and `npx`.
- Auth: OAuth on first connect + Dodo Payments **API key** (test or live). Prefer **test** keys while developing.
- **Never print API keys, OAuth tokens, or secrets.**

## Install MCP (recommended: remote via `mcp-remote`)

Cursor — merge into `~/.cursor/mcp.json` (or use this plugin’s `.mcp.json`):

```json
{
  "mcpServers": {
    "dodopayments-api": {
      "type": "stdio",
      "command": "npx",
      "args": ["-y", "mcp-remote@latest", "https://mcp.dodopayments.com/mcp"]
    },
    "dodo-knowledge": {
      "type": "stdio",
      "command": "npx",
      "args": ["-y", "mcp-remote@latest", "https://knowledge.dodopayments.com/mcp"]
    }
  }
}
```

Claude Desktop (macOS) — same `mcpServers` block in:

```text
~/Library/Application Support/Claude/claude_desktop_config.json
```

Then fully quit and reopen Claude Desktop.

Claude Code:

```bash
claude mcp add dodopayments-api -- npx -y mcp-remote@latest https://mcp.dodopayments.com/mcp
claude mcp add dodo-knowledge -- npx -y mcp-remote@latest https://knowledge.dodopayments.com/mcp
```

(Confirm flags with `claude mcp --help` if your CLI version differs.)

## Verify

1. Reload the client (Cursor reload / Claude restart / Claude Code reconnect).
2. Confirm both `dodopayments-api` and `dodo-knowledge` show as connected.
3. List tools from each server. Expect docs-search style tools on Knowledge and code-execution / sandbox tools on the API server — use **only** the names the server exposes. **Never invent tool names.**
4. If auth prompts appear, complete them in the browser (API key + env). Do not paste keys into chat.
5. On failure: check Node ≥ 18, `npx` on PATH, network to the remote URLs, and the official docs — do not invent fix commands or fake endpoints.

## After setup

- Docs-first questions → `dodo-knowledge` skill.
- Create/manage payments, subscriptions, refunds, licenses, usage → `dodo-payments` skill.
