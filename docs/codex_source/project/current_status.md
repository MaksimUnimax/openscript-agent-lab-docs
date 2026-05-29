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
- 2026-05-21: the future tool family “Ютуб” has been specified in docs as a planned Hermes-visible agent tool, not as a standalone script, UI-only parser, app-local shortcut, or LLM-only transcript generator.
- First planned capability: retrieve available YouTube subtitles/transcript segments with timings by YouTube video URL.
- Implementation has not started.
- Next allowed step for this tool is vendor/API/legal proof and Hermes tool design, not application code.
- 2026-05-21: exact upstream `youtube-transcript-api` docs were imported under `docs/codex_source/vendor/youtube_transcript_api/**`; the concrete planned mechanism is deterministic `video_id` extraction followed by `YouTubeTranscriptApi` transcript listing/fetching for public subtitles/transcripts only.

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
- current project docs update has now been appended to repo memory with the CONTEXT / TOOLS / VOICE project-status block.
- the project docs update records the active next step as `OPENSCRIPT_AGENT_LAB_VOICE_AS_UNIVERSAL_HERMES_TOOL_CAPABILITY_20260519_01`.
- do not mark unrelated task cards ready in this run.
- do not resume Telegram user_id allowlist work unless the user explicitly switches priority.

Current docs update after receipt proof:
- the current active blocker is receipt OCR/full structured extraction, not Telegram/auth/Hermes routing;
- the latest real receipt photo reached `receipt_photo_draft` and the tool result returned `amount=null`;
- the visible receipt total was not recovered by OCR, so the first failing step was `OCR_total_missing`;
- date extraction came from OCR text and resolved to `28.05.2025`, which differs from the user-visible `24.05.2025 14:32`;
- the next technical run should target full receipt extraction for merchant, date/time, total, item names, quantities, item prices, and item sums;
- future Telegram/Hermes/Fin runs must end in a working bot state when live checks are in scope;
- the docs-update workflow now requires ChatGPT to find the last saved docs point first and provide explicit inline append blocks to Codex.

## 2026-05-28 — Current active block: full receipt extraction, not Telegram/Hermes

Current active blocker has moved to deterministic receipt extraction.

Proven receipt-chain facts:
- receipt photo reached the Telegram chain;
- receipt photo reached the selected agent;
- receipt photo invoked `receipt_photo_draft` through Hermes;
- the current failure is not proven in Telegram routing, Telegram auth, Hermes reply, or Telegram send;
- the current proven failing step is receipt OCR/parsing;
- failing step label: `OCR_total_missing`;
- a visible amount `1 189.63` was present on the receipt image;
- OCR candidate text did not produce a usable total line;
- tool result had `amount=null` and `item_count=0`;
- OCR produced date `28.05.2025`, while the visible receipt indicated a different expected date;
- this is a shared receipt-extraction class problem, not a one-image workaround.

User requirement:
- extract all useful receipt information, not only final total;
- fields include merchant, date/time, total, item rows, item names, quantities, unit prices, item sums, payment facts, tax if visible, and `missing_fields` when data cannot be honestly recovered.

Architecture boundary:
- receipt extraction belongs to deterministic business layer;
- Hermes/agent must not invent financial facts;
- Telegram/auth/Hermes must not be reopened unless a fresh proof shows `receipt_photo_draft` is not called or the first broken step moved back to routing/auth/Hermes/send.

Next technical block:
- full receipt extraction proof/design/fix over OCR/preprocessing/parser;
- not a Telegram fix;
- not an auth fix;
- not a Hermes fix;
- not acceptable if it extracts only final total.

- 2026-05-21: the first “Ютуб” capability is no longer only planned. `youtube.subtitles_get` has been implemented as a Hermes-visible agent tool, operator-tested through the `Ютуб` UI tab, connected to an agent through UI, and manually proven in Telegram with `squidward` returning subtitles.
- Current YouTube status: IMPLEMENTED / UI_CONNECTED / AGENT_ATTACHABLE_VIA_UI / MANUALLY_TELEGRAM_PROVEN.
- Language selection policy is now `ru -> en -> any available transcript`; operator language input is a priority hint, not a strict filter.
- Do not repeat vendor/API/design/implementation work for this first YouTube subtitles capability unless a new regression is reported.
- Next YouTube work, if requested, should be treated as extension/polish: long transcript chunking, continuation UX, summary/search modes, or adding the tool to other agents through UI.

- 2026-05-21: after the successful “Ютуб” subtitles MVP, the next product direction is a future Telegram AI/Vibecoding Publisher Agent. The agent will eventually help run a Telegram public channel about neural networks, AI tools, coding agents, and vibe coding.
- The next technical block is not publishing yet. It is the YouTube Research pipeline: search YouTube videos, store metadata in a database, collect subtitles via existing `youtube.subtitles_get`, deduplicate, rank/sort, and prepare candidates for later editorial evaluation.
- Planned initial research tools/stages: `youtube.search_candidates`, `youtube.collect_subtitles_for_candidates`, `youtube.rank_candidates`, and `youtube.editorial_evaluate`.
- Publication, image generation, and Telegram posting are later separate blocks and must not be mixed into the YouTube search MVP.
- Next immediate step: discuss/evaluate YouTube search providers and design `youtube.search_candidates`.
- 2026-05-21: `yt-search-python` vendor docs were imported as the primary proof candidate for the future `youtube.search_candidates` stage; it is not production-selected yet.
- The search-provider design note records search-only usage, and the future `Поиск видео` subtab should expose editable profile parameters inside the subtab itself rather than a separate `Настройки` subtab.
- 2026-05-21: `youtube.search_candidates` MVP is now implemented as operator-only intake with `yt-search-python` search/metadata, deterministic local filters, shared SQLite candidate storage, and a `Поиск видео` subtab in the existing `Ютуб` tab; trusted-channel provider-native search is still not approved.

## 2026-05-22 — YouTube search agent visibility fixed

Current YouTube Research status:

- `youtube.subtitles_get` remains implemented, UI-connected, attachable, and Telegram-proven.
- `youtube.search_candidates` search/intake is implemented and operator-proven.
- full-description enrichment is implemented as a separate metadata-only stage over saved candidates.
- the test candidate DB was cleaned after proof runs while preserving the saved search profile.
- `youtube.search_candidates` is attachable to agents through the UI/source-package/runtime/Hermes path.
- Hermes wrapper propagation was fixed universally through the UI startup restore flow.
- the final visibility blocker was the search gate/profile detection path, not session refresh, wrapper propagation, runtime apply, or Telegram routing.
- fix commit: `df3a3b009132ada4ff3ada75178a97e46fd2a686`.
- current validation stop point: manual Telegram acceptance of the search tool with Squidward.
- next technical block after acceptance: metadata pre-evaluation/ranking for saved/enriched candidates.
- the next YouTube Research pipeline tool is `youtube.select_candidates`.
- this tool is manual-first, but manual-first does not mean bypassing Hermes: the operator-facing path must still use the same Hermes/tool contract that future agents will use.
- `youtube.select_candidates` is independent and must not directly call the future editing/formatting tool.
- the design must keep separate roles for human operator, selection tool, internal curator/evaluator Hermes profile, future public-manager agent, and the next editing/formatting tool.
- operator MVP feedback buttons are exactly `✅ Подходит`, `⏭ Пропустить`, and `❌ Не подходит`.
- DB stores objective facts/lifecycle state; Hermes memory stores learned curator taste; source policy stores current priorities and outranks learned memory.
- the existing `system_filter` protected system agent must not be reused for curator taste memory or editorial selection.

Important debugging lesson:

- compare the working tool and broken tool across gate/check_fn/discovery before blaming session snapshots.
- `session_meta.tools` was a symptom layer, not the first broken layer.
- the search gate used the wrong Hermes-home resolution path before the fix and returned `profile_missing`.

## 2026-05-22 — Correction: `youtube.select_candidates` uses a system Hermes sorting operator

Correction to the previous wording:

`youtube.select_candidates` is not a direct human/manual backend tool.

It is a Hermes-mediated selection tool.

The sorting actor is a system Hermes operator / curator profile inside the tool.

A future public-manager agent may initiate the tool through the Hermes/tool contract and receive selected candidates.

The selection tool must not call the next editing/formatting tool directly.

A human review layer may be added later through Telegram buttons, but it is optional review, not the core backend execution model.

## 2026-05-22 — YouTube select_candidates / youtube_curator runtime and UI configuration ready

Current YouTube Research selection status:

- `youtube.select_candidates` deterministic response-only contract is implemented.
- Selection lifecycle storage is implemented with `youtube_selection_batches` and `youtube_candidate_selection_state`.
- `youtube_curator` source package exists and is protected as a system/internal package.
- Protected system agent registry includes `system_filter` and `youtube_curator`.
- Offline selector-to-curator boundary is implemented with snapshot builder, fake backend, strict response validation, and planned selection actions.
- `youtube_curator` runtime profile exists at `/var/lib/openscript-agent-lab/hermes/profiles/youtube_curator`.
- `Ютуб → Сортировка` now has a read-only YouTube Curator status/settings panel.
- The panel has a source-policy editor for `agent-packages/youtube_curator/rules.md`.
- The panel has apply controls:
  - `Предпросмотр apply`
  - `Применить правила в runtime`
- Apply controls reuse generic endpoints:
  - `POST /api/agents/youtube_curator/runtime/apply-dry-run`
  - `POST /api/agents/youtube_curator/runtime/apply`

Current stop point:

- User should hard-refresh browser and verify `Ютуб → Сортировка`.
- User can edit/save source policy, preview apply, and explicitly apply to runtime.
- No live Hermes-backed curator call has been implemented or tested yet.

Next technical block after manual UI/apply verification:

- design/proof for live Hermes-backed `youtube_curator` adapter inside `youtube.select_candidates`.

Not active now:

- Telegram/router fix;
- YouTube search provider redesign;
- subtitles redesign;
- publishing;
- image generation;
- editing/formatting tool;
- auto-mode.

2026-05-28 update:
YouTube ranked moderation lifecycle was corrected after a task drift into Telegram callback debugging. The accepted fix report is OPENSCRIPT_AGENT_LAB_FIX_YOUTUBE_RANKED_BATCH_LIFECYCLE_AND_CONFIGURED_STACK_SIZE_20260528_01 at commit e21a6874ee864a79ad4f2221b6ee4a8a3d723753. The runner now reuses the latest non-empty active ranked batch before calling Curator, uses configured stack size for stack display, keeps ranking target independent from stack size, and treats zero rows as structured failure rather than ok=true. Current docs gap: decide whether ТЗ should explicitly add a Telegram command for manual start ranking/selection run. Current ТЗ already has UI/backend start ranking action, Telegram continue moderation command, and inline next stack.

2026-05-29 update:
The current working stop-point is YouTube ranked batch lifecycle / moderation stack, not `receipt_full_extraction`. The receipt block remains historical, but the active/current docs pointers now belong to the YouTube ranked batch correction. No application code changes are needed for this docs-only correction. The next product/docs question remains whether to document a separate Telegram command for starting ranking or keep ranking start as a UI/backend operator action while Telegram only continues moderation and serves inline next stack.
