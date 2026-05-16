# Current status

STATUS: INITIAL_FROM_CURRENT_REPO_DOCS

Confirmed facts:
- repo path: `/opt/openscript-agent-lab`
- docs foundation exists under `docs/codex_source/**`
- Hermes vendor docs have been extracted
- Telegram vendor docs have been extracted
- private source repo pushed successfully to `git@github.com:MaksimUnimax/openscript-agent-lab.git`
- public docs repo exported successfully to `git@github.com:MaksimUnimax/openscript-agent-lab-docs.git`
- public docs repo is visible through ChatGPT web access
- unrelated dirty state exists under `agent-packages/**`

Needs confirmation:
- STATUS: NEEDS_CONFIRMATION service `openscript-agent-lab-ui.service` is active
- STATUS: NEEDS_CONFIRMATION UI listener is `127.0.0.1:18765`
- STATUS: NEEDS_CONFIRMATION source repo post-sync HEAD is the new commit reported in the sync run output

Next planned step:
- import actual user-provided ТЗ / roadmap / rules / context / module map into the append-only project docs layer
- keep main feature work paused until actual docs imports are complete

Notes:
- This file is a live project status marker, not a replacement for the technical spec.
- If a fact is not proven by repo docs or current git state, it should stay marked as `NEEDS_CONFIRMATION`.
