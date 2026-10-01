---
name: dodo-knowledge
description: Search Dodo Payments documentation via the Knowledge MCP before coding against the API. Combine with dodopayments-api Code Mode for accurate implementations.
---

# Dodo Knowledge (docs MCP)

Use this skill for documentation questions about Dodo Payments **before** writing payment/subscription code.

## Workflow

1. Confirm `dodo-knowledge` is connected (`dodo-setup`). Use **exact** tool names from that server — never invent search tool slugs.
2. Ask the Knowledge MCP for the relevant docs (API shapes, webhooks, subscription lifecycle, licenses, usage billing, auth, environments).
3. Cite or summarize what the docs return; do not invent API fields or endpoints.
4. When ready to act on the account (create payment, refund, etc.), switch to the **dodo-payments** skill / `dodopayments-api` Code Mode and implement against what the docs describe.

## Combine with payments MCP

| Need | Server |
| --- | --- |
| “How does X work?” / schema / examples | `dodo-knowledge` |
| “Do X on my account” | `dodopayments-api` |

## Guardrails

- Prefer Knowledge MCP over guessing from memory.
- Official docs fallback: https://docs.dodopayments.com (and MCP guide: https://docs.dodopayments.com/developer-resources/mcp-server).
- Never print API keys.
