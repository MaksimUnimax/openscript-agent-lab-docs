# Append-only memory rules

STATUS: IMPORTED_FROM_CHATGPT_UPLOAD

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
- do not rewrite old context or roadmap blocks to "clean them up"
- do not add new memory content without an append block id
- when appending, keep provenance and source kind explicit
- if an append target is not the exact file named by the prompt, stop
