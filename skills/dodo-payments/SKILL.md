---
name: dodo-payments
description: Use the Dodo Payments MCP Code Mode to create and manage payments, subscriptions, customers, products, refunds, licenses, and usage billing. Prefer TypeScript against the SDK in the sandbox; confirm destructive actions with the user.
---

# Dodo Payments (API Code Mode)

Use this skill when working with live Dodo Payments data via the **dodopayments-api** MCP (Code Mode).

## Prefer Code Mode

1. Confirm `dodopayments-api` is connected (`dodo-setup` skill). Use **exact** tool names from the server — never invent slugs.
2. Prefer writing **TypeScript** that uses the Dodo Payments SDK inside the MCP sandbox / code-execution tool the server exposes, rather than guessing REST paths.
3. Use **test-mode** API keys in development. Switch to live only when the user explicitly asks.
4. For product/API behavior you are unsure about, query **dodo-knowledge** first (see `dodo-knowledge` skill), then code.

## Typical domains (not tool names)

Operate within these product areas when the user asks — still only via tools the MCP actually exposes:

- Payments / checkouts
- Customers
- Products and pricing
- Subscriptions (create, update, cancel)
- Refunds
- Licenses
- Usage / metered billing

Do **not** invent endpoint paths or SDK method names; follow docs from Knowledge MCP or official docs at https://docs.dodopayments.com.

## Destructive actions

- **Refunds, subscription cancels, deletes, and live-mode charges** require explicit user confirmation before executing.
- Summarize what will change (ids, amounts, environment test vs live) and wait for approval.

## Guardrails

- Never print API keys, customer PII beyond what the user needs, or raw secret fields from responses.
- Never claim a tool exists that is not listed by the connected server.
- Prefer idempotent, reversible steps in test mode when exploring.
