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
- module map / safe boundaries snapshot has now been imported from bounded repo inventory
- Telegram voice/universal Hermes path was already accepted by server-side proof in roadmap v0.7
- rules pack has now been imported under the repo-based docs access schema
- repo documentation access model v2 has now been imported
- future Codex prompts must include exact DOCS_TO_READ paths
- unrelated dirty state exists under `agent-packages/**`

Needs confirmation:
- STATUS: NEEDS_CONFIRMATION service `openscript-agent-lab-ui.service` is active
- STATUS: NEEDS_CONFIRMATION UI listener is `127.0.0.1:18765`
- STATUS: NEEDS_CONFIRMATION task card re-evaluation has not yet been completed after module map import

Next planned step:
- re-evaluate task cards using imported ТЗ v0.3, roadmap v0.7, rules pack and module map
- keep main feature work paused until required docs imports are complete

Notes:
- This file is a live project status marker, not a replacement for the technical spec.
- If a fact is not proven by repo docs or current git state, it should stay marked as `NEEDS_CONFIRMATION`.

Additional current direction:
- product direction expanded to “Фин инструмент” plus a universal agent farm and agent tools;
- the immediate next step remains Telegram user_id allowlist task-card re-evaluation;
- that re-evaluation must account for moving/placing the allowlist inside the renamed “Фин инструмент” tab;
- after bot access is closed, the next strategic block is Agent Farm / Task Runtime design/proof;
- the financial tool is not just a database; it is a deterministic business tool with scripts, receipt handling and reports;
- Telegram publisher and YouTube parser are planned future tool families;
- none of these new tool families are implemented by this docs update.
- Telegram identity/privacy/access-control STUB docs were filled in this run;
- the next step after this docs-only unblock is to rerun task-card re-evaluation for `telegram_user_id_allowlist_ui`.
