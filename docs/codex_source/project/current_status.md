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

## 2026-06-18 — Current active block: YouTube editor queue target divergence

Current active block:

`youtube_prepare_post_draft_action_target_divergence_five_step_proof`

The prior June 15 fresh YouTube pipeline restart pointer is superseded.

### Current proven facts

* Fresh `youtube.prepare_post_draft` / `list_editor_queue` returned seven ready-for-creation candidates in an observed live queue response.
* A later real editing action attempted `zexcKJYQooU`.
* That ID was not in the immediately preceding fresh seven-item queue.
* The action treated the unrelated candidate as finalized / not suitable.
* The first target-ID substitution point is not yet proven.
* No source fix is accepted for this failure until the exact first divergence is traced.
* Publication is separate and forbidden in the next proof.
* The next proof is read-only and does not execute editing, create drafts, send moderation, or publish.

### Exact next run

`OPENSCRIPT_AGENT_LAB_YOUTUBE_EDITOR_QUEUE_FIRST_TARGET_DIVERGENCE_FIVE_STEP_PROOF_20260618_01`

### Required result

The run must report five direct runtime transitions before the first broken step, then the first broken step itself, with exact input/output IDs, file/function, and value provenance.

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

2026-05-30 update:
- the visible `База / кандидаты` tab now shows only two main summary rows:
  - `Загружено в последнем поиске`
  - `Доступно к ранжированию`
- `Загружено в последнем поиске` is sourced from `latest_search_summary.stored_new_count`;
- if `latest_search_summary` is missing, the UI shows a safe placeholder instead of falling back to all-time DB totals;
- `Доступно к ранжированию` is sourced from `selection_overview.available_for_selection_count`;
- the candidates list now uses 10-row pages with previous/next controls and replaces the current page instead of accumulating rows;
- the candidates API now carries `limit`, `offset`, `has_more`, and `latest_search_summary` as the source of truth for the base tab;
- the main base-tab summary no longer shows provider, all-time DB total, already-in-selection, ranked total, pending moderation, full-description raw rows, DB path, or active-batch/debug counters;
- sorting counter semantics remain distinct from the base tab:
  - `Доступно к ранжированию` is the selection-overview count;
  - `Доступно к отправке на модерацию` is the active batch `pending_count + ranked_count`;
- the candidate-base frontend now guards against loading 50 rows by default and caps the request/render path at 20;
- contract sanitizer hardening remains accepted:
  - unknown `skipped_video_ids` and `rejected_video_ids` do not abort ranking;
  - unknown `selected_video_ids` still hard-fail;
  - validator remains enabled;
  - no hardcoded video IDs were introduced;
- `/agent-lab/api/youtube/moderation/batches` has the route-specific 300s nginx timeout for read/send;
- the latest UI cleanup commit reported in code validation was `1ba686b1d00e6d9dbe71fddbb0df8f3bf2a20092`;
- the current active block is still the YouTube ranked batch moderation lifecycle, and the open docs question remains whether ranking start should be a separate Telegram command or stay a UI/backend operator action while Telegram continues moderation and inline next stack.

2026-06-01 update:
- post-20260530 YouTube search/readiness is fixed: search now auto-completes readiness/enrichment when needed and can increase `available_to_rank` through Telegram/Hermes proof;
- rank pool consistency is fixed: `available_to_rank` and the actual rank pool use one shared source-of-truth, with live proof at `target_count=13` and `ranked_count=13`;
- cleanup recent-days is fixed and proven through Telegram/Hermes/tool actions, with `N=1` meaning candidates collected today;
- global Telegram/Hermes no-reply caused by stale poller cursor was fixed at commit `36d0f6d08c727afc412c9c75e89eac501a14d16e`;
- Kilo/CLI backend exploration was canceled by the user and is not current active roadmap work;
- receipt full extraction remains historical/pending context and must not be duplicated as the current active pointer without an explicit user switch;
- do not infer the next stage from old Provider/Auth, Fin Instrument, Kilo, or receipt blocks without current-state alignment;
- the current next step is not auto-selected by docs; it must follow the next explicit user task and current docs alignment.

## 2026-06-01 — Current active status: YouTube post draft editor live-gate skeleton

- Current active block: `youtube_post_draft_editor_live_gate_skeleton`.
- Current tool: `youtube.prepare_post_draft`.
- Current UI surface: `Ютуб → Редакторская оценка`.
- Latest accepted source HEAD for this branch: `bd32dbee9ef9f0ce358f250ee5e69d46229b5384`.
- Guarded live route skeleton is repeat-proven.
- `POST /api/youtube/post-drafts/editor-execute-live` exists.
- Live route requires `confirm="HERMES_EDITOR_LIVE"`.
- Readiness/precondition guards fail closed before runner call.
- Default/no-runner path does not call Hermes/provider/model.
- Fake route remains fake-only.
- No live Hermes/provider/model call has been attempted.
- No Telegram send, image generation, or publication behavior has been added.
- Next step: separately approved live-smoke proof/design only.

## 2026-06-02 — Current active status: YouTube post draft editor live source-invisible success / manual review

- Current active block: `youtube_post_draft_editor_live_source_invisible_success`.
- Current working draft proof target remains `post-draft-6af43220e9bb` for manual review.
- The final successful live editor run used source HEAD `3047fb23c403428057466c44929a6f92dd74feac`.
- The live run validated successfully and persisted a standalone editorial/news draft.
- `draft_status=ready_for_moderation`.
- `moderation_status=needs_review`.
- `approved_at=null`.
- `published_at=null`.
- `publication_status=null`.
- `text_is_standalone_news_not_video_recap=true`.
- `news_items_expanded_beyond_topic_listing=true`.
- `forbidden_source_reference_phrases_present=false`.
- `text_contains_numbered_or_bulleted_list=true`.
- `image_brief_is_collage_or_composite=true`.
- `image_prompt_is_collage_or_composite=true`.
- The next step is manual UI review of the persisted draft text, not another live execution.
- If accepted, the illustration path may reuse the saved `image_brief`, `image_prompt`, and `image_negative_prompt` through the normal project workflow.
- Temporary Hermes timeout/session-correlation diagnostics remain cleanup debt and should later be reduced to a bounded production-safe summary.

2026-06-04 update:
- Current active block: `youtube_post_draft_moderation_revision_flows`.
- Latest dialogue evidence showed `✏️ Запрошены правки текста. Черновик поставлен на текстовую доработку.`
- That evidence proves text revision flow, not image revision.
- Latest moderation draft target: `post-draft-2479cdb8ffb4`.
- Latest moderation card message id: `952`.
- The next technical run should rewrite the caption only, keep the same titled image, and resend/replace the full Telegram photo+caption+buttons moderation card.
- Image revision stays a separate later block unless fresh proof shows the image action was clicked.
- Do not reopen receipt, Fin Instrument, Telegram auth, or Hermes auth blocks from this stop-point.

2026-06-05 update:
- current active block: `youtube_post_draft_manual_callback_identity_current_card_proof`.
- current unresolved blocker: real manual `callback_query` not observed after deployed `ce34fd2` fix.
- latest accepted implementation head: `ce34fd2b70a10c4a64f9b3180d05637d8a02a67e`.
- closed/proven:
  - repeated text revision;
  - caption grounding normalization;
  - caption formatting normalization;
  - repeated illustration regeneration;
  - titled image asset regeneration and preview;
  - bot polling re-enabled via official route;
  - request-status ordering source fix;
  - safe `codex exec failed` surfacing.
- next correct technical run: proof-only current-card callback identity/intake test.
- not next:
  - new listener;
  - text/image business fix without fresh callback reaching that layer;
  - receipt/OCR;
  - Fin Instrument;
  - publication;
  - Hermes/auth debugging.

## 2026-06-08 — Current active status: YouTube prepare_post_draft attachable tool and editor queue proven

Current active block:
`youtube_prepare_post_draft_attachable_tool_editor_queue_proven`

The active YouTube post-draft line has advanced beyond the previous manual callback identity/intake stop-point.

Proven current state:

* `youtube.prepare_post_draft` is now a public attachable tool.
* `youtube_post_editor_agent` is an internal/system editor agent inside the tool, not the public tool id and not the normal recipient agent.
* Active proof recipient: `plankton`.
* `plankton` has the tool in source package and Hermes runtime profile.
* Manual attach UI exists in `Ютуб → Редакторская оценка` and was manually observed as connected/applied.
* Hermes model-visible callable name is `youtube_prepare_post_draft`.
* Explicit prepare-post-draft requests are routed/forced to the correct model-visible tool when enabled.
* `list_ready_drafts` returns categorized post-draft lifecycle buckets.
* `list_editor_queue` returns full editor queue:

  * ready-for-creation candidates;
  * existing post-draft lifecycle buckets.

Latest proven queue counts:

* ready-for-creation candidates: 2
* current post drafts: 3
* ready-for-publication drafts: 3
* total work items: 5

Current stop-point:

* manual review of the final Telegram response from the `list_editor_queue` proof.

Correct next technical block after acceptance:

* choose explicitly with the user;
* likely `youtube_prepare_post_draft_ready_candidate_creation_flow` if the user wants to create drafts from the 2 ready candidates;
* this would be a mutating action and must use proof/design, DB lifecycle guards, no publication, and simulated Telegram/tool proof if user-facing.

Not next by default:

* publication;
* old YouTube search/subtitles/select work;
* receipt/OCR;
* Fin Instrument;
* Telegram auth;
* Hermes auth;
* 2026-05-05 callback identity proof.

Hard boundaries:

* `youtube.prepare_post_draft` must not publish.
* Approve means ready for future publication, not published.
* Runtime profile must remain sync target only.
* Business facts/lifecycle counts belong in deterministic service/tool layer, not UI text or prompt wording.
* Agent/tool proof must go through project handler → selected agent → Hermes → tool → business layer → delivery proof when user-facing.

## 2026-06-10 — Telegram Publication two-bot migration and admin live-send trigger ready

Current active block:

- `telegram_publication_admin_live_send_trigger_source_ready_pending_main_integration`

Latest proven main/runtime state before the admin-trigger branch:

- `c47f2c62be26998c7f1c6de9d3ab0185cd65b49e`

Runtime Telegram env keys after migration:

- `TELEGRAM_BOT_TOKEN`
- `TELEGRAM_ROUTER_BOT_TOKEN`
- `TELEGRAM_PUBLICATION_BOT_TOKEN`

Post-migration Router proof:

- proof message `PING_AFTER_SECRET_MIGRATION_20260610`
- selected agent `plankton`
- Telegram reply message id `1063`

YouTube continuation blocker:

- closed
- stuck draft `post-draft-80c04bfaf644` resumed
- image generated
- moderation sent with message id `1059`

Telegram Publication live-send blocker:

- identified as missing normal product surface
- live send must go through the admin/product run-cycle endpoint after source integration and deploy

Source branch ready for the next technical run:

- branch `feature/telegram-publication-admin-live-send-trigger-20260610-agent1`
- commit `481fa4ee4ce862245142144098629dbf7094b91e`
- adds `POST /api/telegram-publication/run-cycle`
- preview/dry-run by default
- explicit `confirm_live_send: true` required for live send
- first proof capped to one post

Next exact run:

- integrate the source branch into main
- no runtime deploy
- no live send
- no Telegram API call
- no Hermes live tool call
- no env/token changes

## 2026-06-14 — Telegram Publication admin trigger source integrated, pending runtime proof

Current active block:
`telegram_publication_admin_trigger_source_integrated_pending_runtime_proof`

Source integration completed:

* private source commit `fcde3149e4baa0ba6a01664e1ba029da0e1399f4` is now on `origin/main`;
* only these four source/test files were committed:

  * `agent_lab/admin_server.py`
  * `agent_lab/telegram_publication_run_cycle.py`
  * `tests/test_admin_server.py`
  * `tests/test_telegram_publication_run_cycle.py`
* the endpoint source contract remains:

  * `POST /api/telegram-publication/run-cycle` exists;
  * preview/dry-run is the default path;
  * `confirm_live_send: true` is required for live send;
  * first live proof remains capped to `max_posts=1`;
  * the endpoint delegates to `telegram_publication_run_cycle.run_telegram_publication_run_cycle`;
  * the run-cycle layer delegates to `telegram_publication_send_execution.run_telegram_publication_send_execution`;
  * the endpoint does not call Telegram API directly;
  * the endpoint does not read or print token values;
  * the endpoint does not hardcode agent, user, chat, provider, or message id values;
* `telegram.publication` Hermes tool remains no-live-send;
* runtime deploy, restart, live-send, and env/token changes were not performed;
* the frontend/auth repo was not touched and belongs to another agent/repo;
* unrelated untracked pollution remains and is not part of this docs run:

  * `agent-packages/**`
  * `tools/hermes_vendor_overlay/hermes-agent/tools/fin_receipt_tool.py`
  * `.venv-hermes/**`
  * `**/__pycache__`
  * `vendor/**`
* new stop-point:

  * source is integrated, but runtime/product proof is still pending;
* recommended next run:

  * proof_only source-vs-runtime / endpoint availability check;
  * verify whether the running service exposes `POST /api/telegram-publication/run-cycle`;
  * no live send;
  * no Telegram API call;
  * no deploy/restart unless a later explicitly approved deploy run is created;
  * if endpoint is absent in runtime, stop and propose a separate deploy/restart design/proof.

## 2026-06-14 — Telegram Publication live proof success, pending preview/live selection stability

Current active block:

`telegram_publication_live_proof_success_pending_preview_live_selection_stability`

Confirmed facts:

- one-post live proof succeeded through the normal admin/product endpoint `POST /api/telegram-publication/run-cycle`;
- private source commit `c8d4520e0dd0cf55f608118cd76849878ebc5a51` was already on `main` at the time of the proof;
- the runtime service was active and `/healthz` returned `200 OK`;
- safe target summary remained available as `@openscriptwibe via @EditorWaib_bot`;
- approved drafts were ingested through `agent_lab.telegram_publication_ready_materials.ingest_ready_materials`;
- three publication jobs were created from the approved unpublished drafts;
- the live call was made with `{"confirm_live_send": true, "dry_run": false, "max_posts": 1}`;
- the live result was `LIVE_PROOF_SUCCESS`;
- `live_send_executed` was `true`;
- `jobs_sent` was `1`;
- `jobs_published` was `1`;
- `telegram_message_id` was `8`;
- no direct Telegram API call was made by Codex;
- no Hermes live-send was used;
- no source edits, deploys, restarts, env/token changes, or secrets exposure occurred in this docs run;
- the frontend/auth repo was not touched;
- tracked source tree remained clean;
- unrelated untracked pollution remains untouched.

Follow-up issue:

- preview selected job id:
  `telegram-publication-job:v1:a81eed31baa9d5c5eb8b3643bc97fa89d959c2dfe7830ad9654f5df3557c52de`
- live sent job id:
  `telegram-publication-job:v1:7f8de8ded4b92c0e09a640345a34041fa2b0886b058f4ff6cfe7c352f2857c10`
- the live proof is valid because exactly one approved publication job was sent through the correct path;
- the preview/live mismatch should be stabilized in future work so approval can point at the same selected job identity before execution.

Recommended next step:

- add a deterministic preview-to-live selection identity, such as `selected_job_id`, `preview_plan_id`, or a confirmation token, and prove that preview and live operate on the same job before any future live-proof approval.

## 2026-06-14 — Telegram Publication media live proof success

Current active block:

`telegram_publication_media_live_proof_success`

Confirmed facts:

- the final accepted Telegram Publication path now includes a safe operator retry endpoint plus the normal admin/product run-cycle endpoint;
- preview remains dry-run by default;
- `confirm_live_send: true` is required for live send;
- `max_posts=1` remains the live proof cap;
- `selected_job_id` exact binding is implemented for both preview and live;
- media/photo send path is implemented and used for approved media jobs;
- Telegram photo captions are capped safely at `TELEGRAM_PHOTO_CAPTION_LIMIT=1024`;
- safe failed-job retry endpoint exists:
  - `POST /api/telegram-publication/jobs/retry`
  - `failed -> retry_pending`
  - preserves media metadata
  - does not send Telegram messages
- exact media job live proof succeeded through the product/admin run-cycle endpoint;
- one Telegram message was published for the exact job id:
  - `telegram-publication-job:v1:8b53c4871b838e3fd2fdb3cd7c11af0d2302f1add553db21c649fc2c7d08847b`
  - retry proof transitioned `failed -> retry_pending`
  - preview proof selected the exact job id
  - live proof published message id `9`
- earlier historical proof remains recorded:
  - message id `8`
  - earlier text-only proof before the media/retry path was fixed
- architecture boundary remains intact:
  - OpenScript remains an Agent Lab, not a one-off Telegram bot;
  - publication continues through the product/business layer;
  - no direct Telegram API shortcut by Codex;
  - `youtube.prepare_post_draft` still does not publish;
  - no Hermes live-send was used;
  - no secrets were printed;
  - no manual SQL was used;
  - tracked tree was clean apart from unrelated untracked pollution;
- runtime response caveat:
  - the runtime response did not expose a dedicated `media_caption_truncated` flag, so future polish could add safe media delivery/caption metadata to the response if needed.

Source commits recorded in this proof chain:

- `fcde3149e4baa0ba6a01664e1ba029da0e1399f4` - Add Telegram publication admin run-cycle trigger
- `c8d4520e0dd0cf55f608118cd76849878ebc5a51` - Add safe target summary fields
- `650feb52641bf79937d2ea48583a33d2bce7f660` - Bind Telegram publication live proofs to selected jobs
- `463f5eda2111575b4eb894272400ae99a28e1435` - Publish Telegram media via photo delivery
- `90065ef2d0b6eceaef1ff1ed929d0927b30eb554` - Bind Telegram publication preview to selected jobs
- `b3b7105cc202994008d3c5fc8fb155226cca7a14` - Cap Telegram photo captions safely
- `4b495fa7d0fb0a4d23f7f33b9265027b11eaa77c` - Add Telegram publication retry path

Recommended next step:

- no technical blocker remains for the proven publication path;
- optional docs/UI polish only unless a new bug appears;
- if future approval proof is needed, use the same exact selected job identity and retry/live path contract already proven here.

## 2026-06-15 — YouTube editor skill-selection experience ready for documentation, fresh pipeline restart next

Current active block: `youtube_editor_skill_selection_experience_documented_then_fresh_pipeline_restart`

Confirmed current dialogue facts:
- Telegram Publication media live proof remains the latest saved publication proof; no new publication is requested in this docs update.
- A later YouTube editor-quality exploration iterated over several writing/editor skills for `youtube_post_editor_agent`.
- Important editor-skill lessons are now consolidated in `docs/codex_source/project/youtube_post_editor_skill_selection_experience_20260615.md`.
- Text regeneration was proven to use source facts and transcript snapshots, not previous draft text as main model input.
- `human_telegram_editor.md` and `telegram_editorial_writer.md` were updated toward source-to-angle shaping during the dialogue and runtime-applied in proof runs.
- The latest regenerated draft moderation cards after source-to-angle update were:
  - `post-draft-aa6589f0fe2c` -> `1148`
  - `post-draft-bc7a951fa811` -> `1150`
  - `post-draft-a2dc0520ab53` -> `1152`
- The user judged the current editor result acceptable enough to proceed, but not final.
- The immediate requested action is docs-only memory update before any fresh YouTube pipeline rerun.

Next correct run:
- docs-only update for editor skill-selection experience and project memory.

After that, a separate run may repeat the previous safe cleanup + fresh YouTube pipeline chain.

Not next:
- publication;
- provider/model calls during docs update;
- DB cleanup inside docs update;
- application code edits inside docs update;
- direct Telegram API;
- manual SQL without later cleanup approval.

## 2026-06-15 — Docs correction: editor skill-selection experience documented, fresh YouTube pipeline restart next

Current active block: `youtube_fresh_pipeline_restart_after_editor_skill_docs_completed`

Correction:
The YouTube editor skill-selection experience docs update is complete.

Completed docs state:
- Dedicated document exists:
  `docs/codex_source/project/youtube_post_editor_skill_selection_experience_20260615.md`
- Context/roadmap/module-map/project snapshot were updated in the previous docs run.
- The previous blocker `editor_skill_selection_experience_not_yet_documented` is closed.
- The next run is no longer another docs-only memory update.

Next correct run:
- safe cleanup + fresh YouTube pipeline restart, as a separate technical run.

The next run must start with current-state proof before mutation:
- inspect active YouTube selection/draft/publication state;
- prove cleanup scope;
- preserve published history/proof rows;
- then run fresh YouTube candidate moderation and draft generation through Hermes/operator flow.

Not next:
- publication;
- direct Telegram API;
- image/overlay redesign;
- new editor skill search;
- docs-only repeat of the same skill-selection experience;
- provider/model calls outside official future pipeline path;
- DB cleanup without explicit proof of exact affected rows.
