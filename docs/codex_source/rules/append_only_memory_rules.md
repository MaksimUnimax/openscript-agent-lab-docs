# Append-only memory rules

STATUS: INITIAL_FROM_CURRENT_REPO_DOCS

Append-only memory files:
- `docs/codex_source/context/current_dialogue_context.md`
- `docs/codex_source/roadmap/roadmap.md`
- `docs/codex_source/module_map/module_map.md`

Rules:
- append new blocks only
- keep stable block ids
- keep manifest metadata in sync
- Codex should read manifest + tail only for updates
- no destructive rewrite of historical blocks
