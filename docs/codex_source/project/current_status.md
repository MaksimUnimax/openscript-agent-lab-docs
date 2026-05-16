# Current status

STATUS: IMPORTED_FROM_CHATGPT_UPLOAD

Confirmed facts:
- repo path: `/opt/openscript-agent-lab`
- docs foundation exists under `docs/codex_source/**`
- Hermes vendor docs have been extracted
- Telegram vendor docs have been extracted
- private source repo pushed successfully to `git@github.com:MaksimUnimax/openscript-agent-lab.git`
- public docs repo exported successfully to `git@github.com:MaksimUnimax/openscript-agent-lab-docs.git`
- public docs repo is visible through ChatGPT web access
- normalized working context has been appended to repo memory
- the current technical spec is v0.3, imported from `Тз(2).md`
- v0.2 is historical/original and not the current source-of-truth spec
- roadmap v0.7 has now been imported as the current roadmap state
- Telegram voice/universal Hermes path was already accepted by server-side proof in roadmap v0.7
- unrelated dirty state exists under `agent-packages/**`

Needs confirmation:
- STATUS: NEEDS_CONFIRMATION service `openscript-agent-lab-ui.service` is active
- STATUS: NEEDS_CONFIRMATION UI listener is `127.0.0.1:18765`
- STATUS: NEEDS_CONFIRMATION rules pack has not yet been imported
- STATUS: NEEDS_CONFIRMATION module map expansion has not yet been imported

Next planned step:
- import actual rules pack and module map into the append-only project docs layer
- keep main feature work paused until required docs imports are complete

Notes:
- This file is a live project status marker, not a replacement for the technical spec.
- If a fact is not proven by repo docs or current git state, it should stay marked as `NEEDS_CONFIRMATION`.
