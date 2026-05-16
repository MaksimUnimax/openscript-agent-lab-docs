# Current status

STATUS: INITIAL_FROM_CURRENT_REPO_DOCS

Confirmed facts:
- repo path: `/opt/openscript-agent-lab`
- docs foundation exists under `docs/codex_source/**`
- Hermes vendor docs have been extracted
- Telegram vendor docs have been extracted
- `git remote -v` is currently empty
- unrelated dirty state exists under `agent-packages/**`

Needs confirmation:
- STATUS: NEEDS_CONFIRMATION service `openscript-agent-lab-ui.service` is active
- STATUS: NEEDS_CONFIRMATION UI listener is `127.0.0.1:18765`

Next planned step:
- import project docs / memory and set up GitHub push visibility before resuming further main ТЗ work

Notes:
- This file is a live project status marker, not a replacement for the technical spec.
- If a fact is not proven by repo docs or current git state, it should stay marked as `NEEDS_CONFIRMATION`.
