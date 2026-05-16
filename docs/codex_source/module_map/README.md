# Module map memory

STATUS: CURRENT_SNAPSHOT_FROM_REPO_INVENTORY

This directory stores the append-only module map and the current bounded snapshot derived from repo inventory.

Current snapshot files:
- `docs/codex_source/module_map/imported/current_module_map_snapshot.md`
- `docs/codex_source/module_map/imported/safe_boundaries_snapshot.md`

Rules:
- append only for `docs/codex_source/module_map/module_map.md`
- keep short blocks in the append log
- prefer directory and ownership summaries over copied source contents
- keep the snapshot files aligned with the current repo tree and imported docs
