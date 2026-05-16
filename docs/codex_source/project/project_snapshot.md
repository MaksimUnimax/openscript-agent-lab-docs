# Project snapshot

STATUS: PARTIAL_SNAPSHOT

This is a lightweight summary of the repo shape, generated from repo tree inspection only.

Current snapshot:
- source-of-truth docs: `docs/codex_source/**`
- vendor source: `docs/codex_source/vendor/**`
- project memory: `docs/codex_source/project/**`, `docs/codex_source/context/**`, `docs/codex_source/roadmap/**`, `docs/codex_source/module_map/**`, `docs/codex_source/project_snapshot/**`, `docs/codex_source/rules/**`
- application tree: `agent_lab/`
- tests: `tests/`
- utility tools: `tools/`
- registry: `tool-registry/`
- local Hermes vendor source: `vendor/hermes-agent/`
- package workspace: `agent-packages/`
- local virtual environment: `.venv-hermes/`

Source directories:
- `agent_lab/` - runtime application code and static assets
- `tests/` - automated tests
- `tools/` - utility scripts
- `tool-registry/` - tool registry data
- `vendor/hermes-agent/` - local Hermes source checkout

Runtime directories:
- `.venv-hermes/` - local runtime environment
- `agent_lab/static/` - static UI assets

Agent packages:
- `agent-packages/` exists and currently contains unrelated dirty/untracked work
- do not stage or modify it unless the scope explicitly requires it

Hermes profiles:
- NEEDS_MAPPING

Telegram runtime state:
- NEEDS_MAPPING

Docs source-of-truth:
- `docs/codex_source/index.yaml`

Vendor docs:
- `docs/codex_source/vendor/hermes/**`
- `docs/codex_source/vendor/telegram/**`

Project docs:
- `docs/codex_source/project/**`
- append-only memory files under `docs/codex_source/context/**`, `docs/codex_source/roadmap/**`, `docs/codex_source/module_map/**`

Things not to touch without explicit scope:
- `agent-packages/**`
- secrets and auth files
- runtime config files
- vendor source trees
- generated caches

How to refresh this snapshot:
- re-run safe tree inspection only
- update this file and `docs/codex_source/project_snapshot/project_snapshot_manifest.yaml`
- do not paste full file contents here
