# Module map

STATUS: INITIAL_FROM_CURRENT_REPO_DOCS

Current high-level module view:
- `agent_lab/` - runtime application and UI layer
- `docs/codex_source/` - source-of-truth and project memory docs
- `vendor/hermes-agent/` - local Hermes source checkout
- `agent-packages/` - package workspace and unrelated dirty state
- `tests/` - test suite
- `tools/` - utility and maintenance scripts
- `tool-registry/` - registry data
- `.venv-hermes/` - local Hermes runtime environment

Related append-only memory:
- `docs/codex_source/module_map/module_map.md`

Purpose:
- give ChatGPT a small current map before it reads the larger append-only module map
