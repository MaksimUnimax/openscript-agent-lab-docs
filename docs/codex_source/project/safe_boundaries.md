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

Current module map reference:
- `docs/codex_source/module_map/imported/current_module_map_snapshot.md`
- `docs/codex_source/module_map/imported/safe_boundaries_snapshot.md`

Current boundary summary:
- `docs/codex_source/**` is the docs source-of-truth for ChatGPT and Codex.
- public docs repo mirrors only `docs/codex_source/**`.
- `agent_lab/**` is application/backend/UI code and stays out of docs-only runs.
- `agent-packages/**` is agent package workspace and unrelated dirty state.
- `vendor/hermes-agent/**` is a vendor checkout and should not be casually edited in docs runs.
- `/var/lib/openscript-agent-lab/hermes/**` is runtime state, not source-of-truth.
- runtime auth, secrets, memories, sessions and logs must not go to git or public docs.
- if a boundary is unclear, stop and seek proof first.

Docs-only runs:
- may create or update files only under `docs/codex_source/**`
- should keep vendor docs separate from project memory
- should preserve append-only files

Why this exists:
- to prevent accidental edits outside the requested documentation scope
