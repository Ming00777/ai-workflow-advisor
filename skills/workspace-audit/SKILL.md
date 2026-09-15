---
name: workspace-audit
description: Audit a user-authorized local workspace to identify file types, installed commands, project dependencies, and possible AI workflow needs without reading sensitive file contents or changing the system.
---

# Workspace Audit

Use this skill when a user asks what AI tools, CLI programs, MCP servers, or Agents fit their current work environment.

## Operating rules

1. Explain the exact scan scope and ask for authorization before inspecting local paths or command availability.
2. Prefer cheap, read-only checks: current working directory, bounded file-name inventory, package manifests, Git metadata, and version/help commands for explicitly requested binaries.
3. Never print secrets. Do not read API keys, cookies, tokens, OAuth files, private message contents, or full document bodies. Redact environment variables and configuration values.
4. Distinguish facts from inferences. A `.xlsx` file proves that a spreadsheet exists; it does not prove the user's recurring job.
5. If access is unavailable, say so and ask the user about their workflow instead of pretending to have historical usage data.

## Scan scope

Unless the user sets a different boundary, inspect only the current workspace at a bounded depth and a small allowlist of manifest names. You may check whether a `.git` directory or remote exists, but do not print credentials or remote URLs containing tokens. Check command existence and versions only for a short relevant list; do not enumerate every installed program.

## Output

Return a compact audit with:

- scan scope and timestamp;
- observed facts, such as file-extension counts, manifests, Git presence, and command/version evidence;
- user-provided context, kept separate from machine observations;
- likely tasks, clearly marked as hypotheses;
- capabilities not observed in this scope, never phrased as proof of absence;
- files, secrets, or permissions intentionally not inspected;
- follow-up questions that would materially change recommendations.

Do not install, authenticate, modify PATH, edit config files, or call third-party services in this mode.
