---
name: tool-recommendation
description: Recommend a small, explainable set of China-focused CLI tools, MCP servers, and Agent products from the local catalog after understanding the user's work goals and authorized workspace audit.
---

# Tool Recommendation

Use the catalog under `catalog/` as the source of truth. Read only the relevant catalog file for the requested tool type.

## Workflow

1. Ask what the user is trying to accomplish and what data or collaboration tools they already use.
2. Use an authorized `workspace-audit` result if available. Never infer a tool choice from file names alone, and never treat a missing manifest or binary as proof that a user does not need that capability.
3. Match the task to a maximum of five candidates. Rank by task fit, current gap, installation feasibility, source quality, permission cost, and maintenance status.
4. Explain each recommendation: problem solved, why it matches the user's stated goal or a clearly labeled hypothesis, prerequisites, permission scope, official or community status, and a safe verification step.
5. Include one or two lower-risk alternatives and say why they were not ranked first.
6. Never invent an official download URL, CLI command, MCP endpoint, current version, or product integration. If the catalog says `needs_verification`, recommend checking official documentation instead.

## Recommendation classes

- `official`: maintained by the vendor or documented on its official site;
- `community`: useful third-party project, clearly labeled and subject to source review;
- `product_only`: an Agent product with no verified public CLI/MCP installation path in this catalog;
- `needs_verification`: candidate found during research but not safe to present as installable.

## Output format

1. Current user goal
2. Observed facts versus assumptions
3. Ranked recommendations
4. Installation order
5. Permissions and privacy notes
6. What to verify before installation

Do not auto-install or mutate any system state. Installation belongs to `setup-guide` and still requires explicit authorization immediately before execution.
