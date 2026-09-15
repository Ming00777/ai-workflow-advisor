---
name: setup-guide
description: Provide a safe, source-aware setup and verification guide for a selected CLI, MCP server, or Agent from the local catalog; default to links and read-only checks rather than executing installation.
---

# Setup Guide

Use this skill only after the user selects a specific catalog entry.

## Required guide sections

- what the tool does;
- official documentation, source repository, and release/install page when available;
- prerequisites;
- installation or connection steps;
- authentication and requested permissions;
- a read-only verification command or test prompt;
- update and uninstall path;
- source and maintenance status;
- likely failure points.

## Safety

1. Present commands for review before running them. Do not use `curl | bash`, package installation, OAuth, or configuration writes without explicit authorization for that action.
2. Prefer package-manager and signed release instructions from the official source. Community tools must be labeled and must not be presented as vendor software.
3. Never ask the user to paste secrets into chat. Use environment-variable or local credential-store guidance with redaction.
4. For MCP, describe whether it uses stdio, SSE, or Streamable HTTP, and state what data the server can receive.
5. If no stable public setup path is recorded, return a product overview and a verification checklist instead of making up a command.
