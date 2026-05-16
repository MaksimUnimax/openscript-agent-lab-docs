# Safe boundaries

STATUS: IMPORTED_FROM_CHATGPT_UPLOAD

Do not modify without explicit scope:
- `agent-packages/**`
- application code under `agent_lab/**`
- vendor source trees
- auth files and secrets
- runtime config and service files
- generated caches

Architectural safety rules:
- the agent cannot own business logic;
- the agent cannot write SQL;
- the agent cannot read raw DB directly;
- the agent cannot see secrets;
- the agent cannot execute shell from user text;
- the agent cannot confirm a receipt without user confirmation;
- the system must not hardcode a fixed agent count;
- provider selection must remain independent from agent identity;
- Telegram Router must not be built before dependencies are ready;
- Hermes Dashboard must not be exposed as the public product UI.

Docs-only runs:
- may create or update files only under `docs/codex_source/**`
- should keep vendor docs separate from project memory
- should preserve append-only files

Why this exists:
- to prevent accidental edits outside the requested documentation scope
