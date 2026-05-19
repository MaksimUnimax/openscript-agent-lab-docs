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
- STATUS: CONFIRMED service `openscript-agent-lab-ui.service` is active
- STATUS: CONFIRMED UI listener is `127.0.0.1:18765`
- STATUS: CONFIRMED task card re-evaluation for Telegram user_id allowlist has completed and the task card is advisory/history-only

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
- workflow rules were updated to risk-based combined runs;
- separate design-run is no longer mandatory by default for narrow ordinary fixes;
- high-risk or unclear tasks still require separate design approval;
- the next active project step remains Telegram user_id allowlist task-card re-evaluation, then a possible combined proof/design/fix run if the task card allows it.
- task-card readiness is now advisory metadata rather than the primary permission gate;
- stale `ready_for_fix_run: false` should not block a guarded combined run by itself;
- the next Telegram user_id allowlist pass should proceed as a guarded combined run if docs gate and combined guard pass.
- Telegram user_id allowlist access control has now been implemented in code and verified by tests.
- the task card remains advisory/checklist metadata and should not be read as a blocking permission gate.
- the visible Telegram tab label has now been updated to “Фин инструмент” and the live UI service was restarted to load the current bundle.
- the same “Фин инструмент” tab now again shows the existing Telegram bot controls/status, access control, bot-router and voice readiness blocks alongside the financial storage/read-only sections.
- the internal compatibility route slug remains `telegram`; only the visible product label is “Фин инструмент”.
- allowlist normalization was verified for both string and integer `user_id` values.
- next step is controlled manual verification of allowed/denied Telegram user_id behavior through the UI/runtime path, if needed.
- live polling stage instrumentation is now exposed through safe runtime status fields for the canonical service (`runtime_loop` and `polling_cycle`).
- current live proof shows the canonical polling loop entering the update and reply path, with `current_cycle_stage: before_reply` and the last completed cycle failing with `reply_failed` / `Hermes runtime did not return a reply`.
- the remaining blocker is now in the reply/Hermes path, not in Telegram inbound polling, webhook configuration, or allowlist matching.
- next step is targeted reply-path diagnosis using the new stage fields, or a separate narrow fix run if the exact module becomes proven.
- Hermes pre-reply auth readiness gate has now been implemented in the reply path.
- Telegram replies now fail closed with a safe reason when Hermes/auth/provider readiness is degraded, instead of silently calling Hermes and returning an empty reply.
- The reply path now carries safe status fields for auth block reasons, and the UI can surface that Telegram replies are blocked by auth.
- Existing Codex-CLI recovery flow remains intact and is still the approved way to restore Hermes readiness.
- current next active block is now the Fin Instrument / Financial Tool line, not the Agent Farm line.
- Agent Farm / Task Runtime is deferred until the Fin Instrument financial-tool design/proof block is progressed.
- this run is docs-only product correction; no application code was implemented.
- first source-only Fin Instrument financial-tool contracts skeleton has now been implemented.
- the slice added deterministic contracts, no-op handlers, readiness summary, and regression tests only.
- no SQLite schema, runtime storage writes, UI integration, Telegram integration, voice integration, or Agent Farm implementation was added in this slice.
- the next slice should be reviewed separately: SQLite schema design or runtime storage initializer proof/design, not both blindly.
- the Fin Instrument SQLite schema design has now been proposed as a docs-only slice.
- the schema proposal stays source-only and does not create a database or migration file.
- the next slice should stay narrow: runtime storage initializer proof/design or source SQL migration skeleton.
- the Fin Instrument runtime storage initializer design has now been proposed as a docs-only slice.
- the initializer proposal stays source-only and does not create a runtime directory, database file, or migration file.
- the next slice should be the runtime storage initializer implementation with temp-dir tests, not UI or Telegram integration.
- the Fin Instrument runtime storage initializer has now been implemented as source code with temp-dir tests.
- the implementation stays source-only, does not auto-create the production runtime root, and is not wired into UI, Telegram, service startup or Agent Farm.
- the next slice should be deterministic storage scripts or a read-only readiness surface, not an immediate UI/Telegram mix.
- deterministic storage scripts for the Fin Instrument financial tool are now implemented.
- `expense_add`, `expense_recent`, and `expense_month_summary` now have deterministic SQLite-backed storage paths that require an explicit runtime root.
- the production runtime root `/var/lib/openscript-agent-lab/fin-instrument/` was not created in this run.
- the read-only UI readiness surface for Fin Instrument is now implemented.
- the next slice should be a controlled runtime initialization operator action, not a UI/Telegram mix.
- the controlled runtime initialization operator action is now implemented through the live admin endpoint.
- the shared production Fin Instrument runtime root `/var/lib/openscript-agent-lab/fin-instrument/` now exists and the shared SQLite DB `finance.sqlite3` was created through the controlled endpoint.
- Fin Instrument status now reports `schema_ready`/`ready` after initialization and the next likely slice is a read-only expense view or a later Telegram/voice design slice.
- the read-only Fin Instrument expense view is now implemented in the shared UI/backend surface.
- recent expenses and current-month summary now render read-only from the shared Fin Instrument SQLite database.
- the combined Fin Instrument surface now keeps the Telegram controls/status visible instead of hiding them behind the legacy wrapper.
- the “Голос для Telegram-агентов” section now again shows per-agent Telegram voice checkboxes, using Telegram-owned per-agent config with default-false behavior for future agents.
- no expense write UI, Telegram/voice integration, Agent Farm integration, or new security middleware was added in this slice.
- the next slice should now move to controlled manual expense add UI or, separately, Telegram/voice financial-tool integration design.
- the UI-only emergency rollback restored the working Telegram-only tab baseline before the Telegram interface was hidden/removed.
- the financial blocks are deferred again for this run; the production DB/backend remain preserved, but the visible tab is Telegram-only now.
- the previously mixed Fin Instrument UI layers were superseded in the frontend by the rollback baseline from the last working Telegram tab.
- UI-only rollback to the working Telegram baseline completed at private commit `b38a8bd35095dc0cf7117227215bd483fd2f3df1`.
- financial UI re-add is deferred until the Telegram reply path is restored and the user reviews the Telegram-only baseline again.
- Fin Instrument backend/storage/production DB remain preserved, but are currently not shown in the visible UI.
- the active blocker after rollback is Telegram no-reply for the already-sent message `кто ты`.
- the next exact run is `OPENSCRIPT_AGENT_LAB_TELEGRAM_NO_REPLY_EXISTING_KTO_TY_AFTER_UI_ROLLBACK_20260517_01`.
- Fin Instrument UI work must not resume until Telegram reply behavior is restored.

Additional current direction:
- Fin Instrument schema v2 / product-field work completed successfully at private commit `f0235cbeed7f27392c5d3bcca88a44c6315654dd`.
- the expense model now has a dedicated required `product` / `Товар` field stored separately from `description`;
- `category` is now optional and defaults to `Без категории` / `bez_kategorii`;
- `description` is now optional comment text;
- legacy description-only add payloads are rejected safely;
- live controlled POST proof succeeded with `amount=12`, `product=хлеб`, `currency=RUB`, `payment_source=card`;
- `/api/state` now shows `product=хлеб` and `category=Без категории`;
- the test baseline reached 143 passed tests and the service/healthz remained healthy;
- Telegram UI/auth/provider paths were left untouched by this docs update.
- current dialogue context was appended with the full CONTEXT/TOOLS/VOICE working block for the pending universal voice/tool capability prompt.
- CONTEXT receipt hydration remains reported live-ready via commit `8cdba40` (`Hydrate receipt context for next turns`).
- TOOLS Hermes receipt tool loop remains reported live-ready via commit `fb6f892569dc78db5d24bc8541d297fc9ab22556` (`Add Hermes receipt tool loop`).
- VOICE remains the next unresolved architecture task and is preserved here as the next pending prompt instead of being executed in this docs-only run.
- the pending next Codex prompt is `OPENSCRIPT_AGENT_LAB_VOICE_AS_UNIVERSAL_HERMES_TOOL_CAPABILITY_20260519_01`.
