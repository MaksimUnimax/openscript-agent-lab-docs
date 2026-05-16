# Source vs runtime

STATUS: INITIAL_FROM_CURRENT_REPO_DOCS

Source-of-truth layers:
- vendor docs under `docs/codex_source/vendor/**`
- project docs under `docs/codex_source/project/**`
- append-only memory under `docs/codex_source/context/**`, `docs/codex_source/roadmap/**`, `docs/codex_source/module_map/**`

Runtime state:
- local virtual environment
- application runtime tree
- package workspaces
- caches and generated artifacts

Principle:
- source-of-truth files are for decisions and prompt grounding
- runtime files are for execution state and should not be confused with documentation

Current boundary note:
- Telegram and Hermes vendor docs are already separated from project memory
