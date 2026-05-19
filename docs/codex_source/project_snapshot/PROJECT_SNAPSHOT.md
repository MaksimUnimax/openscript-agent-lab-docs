# PROJECT SNAPSHOT

STATUS: BOUNDED_CODEX_REPO_SNAPSHOT
SOURCE_KIND: bounded_codex_repo_snapshot
SNAPSHOT_ID: PROJECT_SNAPSHOT_20260519_CONTEXT_TOOLS_VOICE_STATUS
DATE_UTC: 2026-05-19T05:53:20Z

## Git State

- private source repo HEAD at snapshot: `ea0bc2b4e03b12f1895c9520ca8ad24fbfd0a1fe`
- current branch: `main`
- `origin/main` matched `HEAD` before edits
- working tree status: clean
- dirty summary: none detected in this run; `agent-packages/` exists in the tree but was not dirty
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
- hidden cache directories were ignored in the bounded snapshot

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
- roadmap v0.7 remains imported and append-only
- module map and safe boundaries remain imported and append-only
- current dialogue context remains append-only
- current dialogue context now also records the CONTEXT / TOOLS / VOICE project-docs update
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

High-level symbol inventory from the bounded scan:
- `agent_lab` contains the expected Telegram, Hermes, storage, conversation, fin-instrument, and reply orchestration functions/classes
- `tools` contains the agent toggle and vendor restore utility entry points
- `tests` contains focused regression modules for the same layers
- no secrets or auth payloads were read while collecting the inventory

## Current Project Status

- CONTEXT live-ready via commit `8cdba40`
- TOOLS live-ready via commit `fb6f892569dc78db5d24bc8541d297fc9ab22556`
- current dialogue context append saved with id `CTX_20260519_CONTEXT_TOOLS_VOICE_PENDING_PROMPT_V1`
- current project docs update append saved with id `CTX_20260519_PROJECT_DOCS_UPDATE_CONTEXT_TOOLS_VOICE_STATUS`
- voice remains the next unresolved architecture task
- pending next prompt: `OPENSCRIPT_AGENT_LAB_VOICE_AS_UNIVERSAL_HERMES_TOOL_CAPABILITY_20260519_01`
- do not resume Telegram user_id allowlist work unless the user explicitly switches priority
