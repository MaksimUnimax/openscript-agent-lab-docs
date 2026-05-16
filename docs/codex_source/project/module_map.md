# Module map

STATUS: IMPORTED_FROM_CURRENT_REPO_INVENTORY

This is the short human-readable module map summary.

Current detailed snapshot:
- `docs/codex_source/module_map/imported/current_module_map_snapshot.md`
- `docs/codex_source/module_map/imported/safe_boundaries_snapshot.md`

Current append-only module map:
- `docs/codex_source/module_map/module_map.md`

Current manifest:
- `docs/codex_source/module_map/module_map_manifest.yaml`

Current summary:
- `docs/codex_source/**` is the docs source-of-truth layer for ChatGPT and Codex.
- `agent_lab/**` is application/backend/UI code.
- `agent-packages/**` is agent package workspace and unrelated dirty state that must not be accidentally staged.
- `vendor/hermes-agent/**` is the local Hermes vendor source checkout.
- `tools/**` and `tests/**` are supporting code roots.
- `tool-registry/**` stores tool capability registry data.
- `agent-templates/` is absent in the current bounded inventory.
- `/.venv-hermes` and `/var/lib/openscript-agent-lab/**` are runtime/environment areas, not docs source-of-truth.
- task card readiness still needs re-evaluation after this snapshot import.
