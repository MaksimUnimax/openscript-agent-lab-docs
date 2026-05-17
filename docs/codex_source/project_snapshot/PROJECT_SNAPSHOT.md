# PROJECT SNAPSHOT

STATUS: BOUNDED_CODEX_REPO_SNAPSHOT
SOURCE_KIND: bounded_codex_repo_snapshot
SNAPSHOT_ID: PROJECT_SNAPSHOT_20260516_FIN_TOOL_TAB_AGENT_FARM_TZ_EXPANSION
DATE_UTC: 2026-05-17T01:06:37Z

## Git State

- private source repo HEAD at snapshot: `dd19a8752bcb46f073cc290cc60e0b9f42a3985c`
- current branch: `main`
- `origin/main` matched `HEAD` before edits
- working tree status: dirty
- dirty summary: pre-existing `agent-packages/**` modifications and untracked files were present
- docs-only snapshot scope: `docs/codex_source/**` only
- no auth files were read
- no secrets were printed

## Top-Level Repo Structure

Bounded top-level directories observed:
- `agent-packages/`
- `agent_lab/`
- `docs/`
- `tests/`
- `tool-registry/`
- `tools/`
- `vendor/`

Bounded top-level directory notes:
- `agent-templates/` was not present in the bounded inventory
- `vendor/hermes-agent/` exists under `vendor/`
- `.venv-hermes/` was referenced by imported docs as runtime/environment state, not inventoried as source

## docs/codex_source Status

Current docs roots:
- `docs/codex_source/project/**`
- `docs/codex_source/roadmap/**`
- `docs/codex_source/module_map/**`
- `docs/codex_source/context/**`
- `docs/codex_source/project_snapshot/**`
- `docs/codex_source/rules/**`
- `docs/codex_source/vendor/**`
- `docs/codex_source/task_cards/**`

Current imported direction:
- current technical spec remains v0.3
- new technical spec extension v0.4 records “Фин инструмент”, Agent Farm, and agent tools
- roadmap v0.7 remains imported and append-only
- module map and safe boundaries remain imported and append-only
- current dialogue context remains append-only
- public docs repo content rule remains `docs/codex_source/**` only

## Application Module File List Summary

Application/backend/UI inventory from bounded commands:
- backend/admin: `agent_lab/admin_server.py`
- agent reply and routing: `agent_lab/agent_reply.py`, `agent_lab/routing.py`
- agent/provider orchestration: `agent_lab/agentctl_core.py`, `agent_lab/hermes_binding.py`, `agent_lab/hermes_execution.py`, `agent_lab/hermes_status.py`, `agent_lab/llm_connections.py`
- storage/path/runtime helpers: `agent_lab/paths.py`, `agent_lab/request_cache.py`, `agent_lab/response_shapes.py`, `agent_lab/runtime_apply.py`, `agent_lab/storage.py`
- Telegram/voice layer: `agent_lab/system_filter_hooks.py`, `agent_lab/telegram_bot_api.py`, `agent_lab/telegram_commands.py`, `agent_lab/telegram_connector.py`, `agent_lab/telegram_polling.py`, `agent_lab/telegram_runtime.py`, `agent_lab/telegram_voice_transport.py`
- tool registry: `agent_lab/tool_registry.py`
- static UI: `agent_lab/static/app.js`, `agent_lab/static/index.html`, `agent_lab/static/style.css`

Utility / tests / registry inventory from bounded commands:
- `tools/agentctl`
- `tools/restore_hermes_vendor.py`
- `tool-registry/tools.json`
- tests present under `tests/test_*.py`

## Bounded Inventory Notes

- `agent-packages/**` remained dirty/untracked and unrelated to this docs run
- `agent_lab/__pycache__`, `tests/__pycache__`, `tools/__pycache__`, and `vendor/hermes-agent/__pycache__` were visible in the bounded tree output but are not treated as source-of-truth
- `vendor/hermes-agent/` was only inventoried at the top level
- no runtime secret files were read
- no Telegram API calls were run
- no model calls were run

## Snapshot Scope

This snapshot is intentionally bounded.
It records repo shape, docs roots, and current state markers only.
It does not rewrite application code, runtime state, or secrets.
