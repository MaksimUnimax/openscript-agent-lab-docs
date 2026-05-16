# Runtime git canon

STATUS: IMPORTED_FROM_CHATGPT_UPLOAD

Canonical git baseline captured for docs and memory work:
- repo: `/opt/openscript-agent-lab`
- branch: `main`
- head: `8f34733debfdf9ae38482618a9a9113f9995bcaa`
- remote: `git@github.com:MaksimUnimax/openscript-agent-lab.git`
- public docs repo: `git@github.com:MaksimUnimax/openscript-agent-lab-docs.git`
- public docs visibility: yes
- unrelated dirty state: `agent-packages/**`

Rules:
- do not use destructive git commands
- do not stage unrelated dirty files
- docs runs should stage only `docs/codex_source/**`
- if a future run needs push visibility, configure remote explicitly rather than inventing one

This file is a baseline record, not a source for product logic.
