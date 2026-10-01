# Dodo Payments

A Cursor plugin that connects Cursor / Grok Bot to **[Dodo Payments](https://dodopayments.com)** via the official remote MCP servers: **API Code Mode** (payments, subscriptions, refunds, licenses, usage billing) and **Knowledge** (docs search).

Author: Lovin Maxwell (`lovinmaxwell`). Upstream Dodo agent plugin: [dodopayments/dodo-agent-plugin](https://github.com/dodopayments/dodo-agent-plugin). Docs: [MCP server guide](https://docs.dodopayments.com/developer-resources/mcp-server).

## What you get

Two MCP servers (wired in this plugin’s `.mcp.json`):

| Server | Remote URL | Role |
| --- | --- | --- |
| `dodopayments-api` | `https://mcp.dodopayments.com/mcp` | Payments API via Code Mode (TypeScript against the Dodo SDK in a sandbox) |
| `dodo-knowledge` | `https://knowledge.dodopayments.com/mcp` | Search / retrieve Dodo Payments documentation |

On first connect, complete **OAuth** and supply a Dodo Payments **API key** (test or live). Prefer **test mode** keys while developing. **Never print API keys.**

## Prerequisites

- Node.js ≥ 18 (for `npx` + `mcp-remote`).
- A [Dodo Payments](https://dodopayments.com) account and API key.
- Cursor with MCP enabled, **or** Claude Desktop / Claude Code configured as below.

## Recommended: remote MCP via `mcp-remote`

This is the official remote pattern. Merge into Cursor `~/.cursor/mcp.json` (or rely on this plugin’s `.mcp.json` when installed as a local/marketplace plugin):

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

Reload Cursor / restart MCP, finish the OAuth / API key flow in the browser when prompted, then confirm tools appear. Use **exact tool names** from the connected servers — do not invent slugs.

### Claude Desktop (macOS)

Edit `~/Library/Application Support/Claude/claude_desktop_config.json` with the same `mcpServers` block (stdio `npx` + `mcp-remote@latest` URLs above), then restart Claude Desktop.

### Claude Code

```bash
claude mcp add dodopayments-api -- npx -y mcp-remote@latest https://mcp.dodopayments.com/mcp
claude mcp add dodo-knowledge -- npx -y mcp-remote@latest https://knowledge.dodopayments.com/mcp
```

(Exact `claude mcp add` flags may vary by CLI version — check `claude mcp --help`.)

## Install for local testing (Cursor)

1. Copy this directory to:

   ```text
   ~/.cursor/plugins/local/dodo-payments-code
   ```

2. Reload Cursor (**Developer: Reload Window**).
3. Confirm skills appear under Customize / plugins.
4. Ensure MCP is wired (plugin `.mcp.json` and/or `~/.cursor/mcp.json`).

## Marketplace vs Grok Bot

- **Cursor local plugins:** copy under `~/.cursor/plugins/local/…` as above.
- **Cursor marketplace:** publish via [cursor.com/marketplace/publish](https://cursor.com/marketplace/publish).
- **Grok Bot** only installs **marketplace** plugins (not arbitrary local folders). Skills still help once the marketplace plugin (or MCP in `~/.cursor/mcp.json`) is connected.

## Skills

| Skill | When to use |
| --- | --- |
| `dodo-setup` | Install MCP, OAuth / API key, verify tools |
| `dodo-payments` | Payments, subscriptions, customers, products, refunds, licenses, usage via Code Mode |
| `dodo-knowledge` | Docs questions before coding; combine with payments MCP |

## Guardrails

- Never invent tool names — list what the connected MCP exposes.
- Never print API keys, OAuth tokens, or secrets from tool output.
- Confirm destructive actions (refunds, cancels) with the user first.
- Prefer test-mode keys in development.

## Publishing

Cursor marketplace: <https://cursor.com/marketplace/publish>.
