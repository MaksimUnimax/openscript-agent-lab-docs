# Runtime git canon

STATUS: INITIAL_FROM_CURRENT_REPO_DOCS

Canonical git baseline captured for docs and memory work:
- repo: `/opt/openscript-agent-lab`
- branch: `main`
- head: `3eb2ce35026f75928d45865ba9e6919650be98e2`
- remote: empty
- unrelated dirty state: `agent-packages/**`

Rules:
- do not use destructive git commands
- do not stage unrelated dirty files
- docs runs should stage only `docs/codex_source/**`
- if a future run needs push visibility, configure remote explicitly rather than inventing one

This file is a baseline record, not a source for product logic.
