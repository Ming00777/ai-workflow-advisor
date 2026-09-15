---
name: ai-workflow-advisor
description: Discover the user's authorized AI work environment and recommend a small, current set of China-focused CLI tools, MCP servers, and Agent products with official setup links and privacy-aware verification steps.
---

# AI Workflow Advisor

This is the user-facing entry point. Use it when the user asks which AI tools, CLI programs, MCP servers, or Agents they should use or install.

## Default flow

1. Ask what the user wants to improve and explain the read-only audit scope.
2. With authorization, perform the checks described in `../workspace-audit/SKILL.md`. If local inspection is unavailable, use only the user's answers and mark missing context.
3. Combine the audit with the user's stated work habits. File names and installed binaries are evidence about the current workspace, not proof of the user's job or historical usage.
4. Read the relevant catalog files under `../../catalog/` and apply `../tool-recommendation/SKILL.md`.
5. Return at most five ranked recommendations. Separate observed facts, user-provided context, hypotheses, and unresolved questions.
6. For selected items, follow `../setup-guide/SKILL.md` to provide official links, prerequisites, permissions, read-only verification, updates, and uninstall paths.
7. Stop before installing, authenticating, changing configuration, or connecting an MCP unless the user explicitly authorizes that specific action.

## Read-only trial mode

When the user says “先试一下”“只读分析” or equivalent, run a bounded audit and return the recommendation without changing files or system state. Include the exact scan scope, tools detected, file-type summary, manifests found or not found, and what was deliberately not inspected. Treat an empty result as “not observed in this scope”, never as proof that a capability is unnecessary.

## Historical usage

Do not claim access to a user's cross-application history. You may use user-provided exports, explicitly authorized local session metadata, or visible configuration names, but do not read secrets or message/document bodies. Explain what was observed and what remains unknown.

## Catalog policy

Use `official`, `community`, `official-product`, and `needs-verification` labels exactly as recorded. A product such as WorkBuddy may be recommended as an Agent while having no verified public CLI. A community Baidu Netdisk CLI must never be described as Baidu official. Never invent an endpoint or installation command for a catalog entry marked `needs-verification`.
