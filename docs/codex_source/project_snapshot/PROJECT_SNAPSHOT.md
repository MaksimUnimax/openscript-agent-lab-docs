# PROJECT SNAPSHOT

STATUS: BOUNDED_CODEX_REPO_SNAPSHOT
SOURCE_KIND: bounded_codex_repo_snapshot
SNAPSHOT_ID: PROJECT_SNAPSHOT_20260520_RECEIPT_EXTRACTION_AND_DOCS_WORKFLOW
DATE_UTC: 2026-05-20T05:12:01Z

## Git State

- private source repo HEAD at snapshot: `d731611e8ec96d31f8aa62398a157cd9282c1e18`
- current branch: `main`
- `origin/main` matched `HEAD` before edits
- working tree status: dirty outside docs only
- dirty summary: unrelated tracked changes exist in `agent_lab/**`, `tests/**`, and `tools/**`; unrelated untracked files exist in `agent-packages/squidward/**` and `tools/hermes_vendor_overlay/hermes-agent/tools/**`; none were staged for this docs run
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
- roadmap append-only memory now records receipt full extraction as the active blocker
- module map append-only memory now records receipt extraction boundary and docs-update workflow clarification
- current dialogue context now records the receipt extraction blocker and the docs-update workflow correction
- public docs repo content rule remains `docs/codex_source/**` only

## Application Module File List Summary

Bounded application/backend/UI inventory:
- backend/admin: `agent_lab/admin_server.py`
- agent reply and routing: `agent_lab/agent_reply.py`, `agent_lab/routing.py`
- agent/provider orchestration: `agent_lab/agentctl_core.py`, `agent_lab/hermes_binding.py`, `agent_lab/hermes_execution.py`, `agent_lab/hermes_status.py`, `agent_lab/llm_connections.py`
- storage/path/runtime helpers: `agent_lab/paths.py`, `agent_lab/request_cache.py`, `agent_lab/response_shapes.py`, `agent_lab/runtime_apply.py`, `agent_lab/storage.py`
- Telegram/voice layer: `agent_lab/system_filter_hooks.py`, `agent_lab/telegram_bot_api.py`, `agent_lab/telegram_commands.py`, `agent_lab/telegram_connector.py`, `agent_lab/telegram_polling.py`, `agent_lab/telegram_runtime.py`, `agent_lab/telegram_voice_transport.py`
- Fin instrument: `agent_lab/fin_instrument/contracts.py`, `agent_lab/fin_instrument/handlers.py`, `agent_lab/fin_instrument/hermes_adapter.py`, `agent_lab/fin_instrument/readiness.py`, `agent_lab/fin_instrument/receipt_hermes_adapter.py`, `agent_lab/fin_instrument/receipt_ocr.py`, `agent_lab/fin_instrument/schema.py`, `agent_lab/fin_instrument/storage.py`, `agent_lab/fin_instrument/storage_initializer.py`
- tool registry: `agent_lab/tool_registry.py`
- static UI: `agent_lab/static/app.js`, `agent_lab/static/index.html`, `agent_lab/static/style.css`

Utility / tests / registry inventory:
- `tools/agentctl`
- `tools/agent_lab_public_auth_toggle.py`
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
- current dialogue context append saved with id `CTX_20260520_TELEGRAM_HERMES_FIN_RECEIPT_EXTRACTION_AND_DOCS_WORKFLOW`
- current roadmap append saved with id `RM_20260520_RECEIPT_FULL_EXTRACTION_ACTIVE_BLOCKER`
- current module map append saved with id `MM_20260520_RECEIPT_EXTRACTION_BOUNDARY_AND_DOCS_WORKFLOW`
- current project snapshot id is `PROJECT_SNAPSHOT_20260520_RECEIPT_EXTRACTION_AND_DOCS_WORKFLOW`
- current blocker is receipt OCR/full structured extraction
- pending next prompt after this docs update should target receipt extraction proof/design/fix
