# Roadmap

STATUS: INITIAL_FROM_CURRENT_REPO_DOCS

This directory stores append-only roadmap memory.

Rules:
- never rewrite history destructively
- append new roadmap blocks instead
- keep roadmap separate from vendor docs
- future Codex runs should read the manifest and tail, not the entire roadmap

Current roadmap note:
- v0.7 is the current actual roadmap state
- v0.2 through v0.6 are lineage/history
- imported normalized current roadmap content should live under `docs/codex_source/roadmap/imported/`
