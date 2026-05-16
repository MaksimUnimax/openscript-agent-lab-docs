# Safe boundaries

STATUS: INITIAL_FROM_CURRENT_REPO_DOCS

Do not modify without explicit scope:
- `agent-packages/**`
- application code under `agent_lab/**`
- vendor source trees
- auth files and secrets
- runtime config and service files
- generated caches

Docs-only runs:
- may create or update files only under `docs/codex_source/**`
- should keep vendor docs separate from project memory
- should preserve append-only files

Why this exists:
- to prevent accidental edits outside the requested documentation scope
