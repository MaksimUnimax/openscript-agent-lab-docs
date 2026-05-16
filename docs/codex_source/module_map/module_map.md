# Append-only module map

STATUS: INITIAL_FROM_CURRENT_REPO_DOCS

This file is append-only.

Do not rewrite historical blocks destructively.

<!-- MODULE_MAP_APPEND_BEGIN id=MM_20260516_0001 -->
Current high-level module map from repo tree:
- `agent_lab/` - runtime application code and static UI
- `docs/codex_source/` - source-of-truth docs and project memory
- `vendor/hermes-agent/` - local Hermes vendor source checkout
- `agent-packages/` - package workspace with unrelated dirty state
- `tests/` - automated tests
- `tools/` - utility scripts
- `tool-registry/` - registry data
- `.venv-hermes/` - local virtual environment
<!-- MODULE_MAP_APPEND_END id=MM_20260516_0001 -->

<!-- MODULE_MAP_APPEND_BEGIN id=MM_20260516_0002 -->
Current module map snapshot imported from bounded repo inventory and imported docs.

Use these files for the detailed current map and safe boundaries:
- `docs/codex_source/module_map/imported/current_module_map_snapshot.md`
- `docs/codex_source/module_map/imported/safe_boundaries_snapshot.md`

Current status:
- `docs/codex_source/` is the project documentation source-of-truth for ChatGPT and Codex.
- `agent_lab/` is application/backend/UI code and must not be edited in docs-only runs.
- `agent-packages/` is agent package workspace and unrelated dirty state that must not be accidentally staged.
- `vendor/hermes-agent/` is the local Hermes vendor source checkout and was only inventoried at top level in this run.
- `tools/` and `tests/` are supporting code roots used for backend commands and regression checks.
- `tool-registry/` stores tool registry data used by the runtime.

Pending proof:
- exact ownership split inside `agent_lab/` is based on bounded inventory and top-level imports;
- task cards still need re-evaluation after this module map import;
- `agent-templates/` is not present in the current tree snapshot and remains pending proof if introduced later.
<!-- MODULE_MAP_APPEND_END id=MM_20260516_0002 -->
