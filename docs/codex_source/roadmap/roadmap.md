# Roadmap

STATUS: INITIAL_FROM_CURRENT_REPO_DOCS

This file is append-only.

Do not rewrite historical blocks destructively.

<!-- ROADMAP_APPEND_BEGIN id=RM_20260516_0001 -->
Repo documentation foundation:
- source-of-truth docs exist under `docs/codex_source/**`
- Hermes vendor docs were extracted
- Telegram vendor docs were extracted
- the project docs / memory layer is being created
- main ТЗ work is paused until repo docs/memory and GitHub visibility are in place
<!-- ROADMAP_APPEND_END id=RM_20260516_0001 -->

<!-- ROADMAP_APPEND_BEGIN id=RM_20260516_PUBLIC_DOCS_VISIBILITY -->
## 2026-05-16 — Public docs repository is visible

Status: DONE

Facts:
- Private source repo was pushed successfully.
- Public docs-only repo was created and exported.
- Public docs repo contains only `docs/codex_source/**`.
- ChatGPT verified web visibility of `ENTRYPOINT_FOR_CHATGPT.md`.
- A stale HEAD reference in the entrypoint/current docs was corrected.

Next:
- Import actual user-provided ТЗ / roadmap / rules / context / module map.
- Keep imports append-only where required.

<!-- ROADMAP_APPEND_END id=RM_20260516_PUBLIC_DOCS_VISIBILITY -->

<!-- ROADMAP_APPEND_BEGIN id=RM_20260516_IMPORTED_ROADMAP_V0_7_CURRENT source=chatgpt_inline_roadmap accepted_by_user=yes -->

## 2026-05-16 — Imported actual roadmap v0.7 as current roadmap state

### Source

This roadmap import was based on inline roadmap content provided directly in the Codex prompt.
Codex did not need uploaded ChatGPT files.

### Current roadmap version

Current actual roadmap is:

`Roadmap v0.7 — Append-only final Telegram voice success`

v0.7 supersedes v0.6 as the active status.

### Roadmap lineage

- v0.2: historical standalone Expense Bot roadmap.
- v0.3: pivot to Hermes-first Agent Lab.
- v0.4: product layer rebuild, no simulation-response, Agent/source/runtime/provider/business separation.
- v0.5: Hermes runtime/tools/voice.telegram foundation.
- v0.6: Telegram voice + universal Hermes + auth UI blocker state.
- v0.7: final Telegram voice / universal Hermes path server-side success.

### Current accepted proof

Telegram voice / universal Hermes path is complete by server-side proof:

- auth-check before voice: live_ok
- fresh_voice_seen: yes
- selected_agent_slug: runtime_apply_smoke_20260507
- voice_receive_enabled: true
- transcript_handoff_enabled: true
- internal_file_id_available: yes
- recognized: yes
- provider_call_success: yes
- answer_created: yes
- telegram_send_success: yes
- telegram_message_id: 155

Delivery to the same inbound chat_id is also proven.

### Resolved blockers

- 401 token_invalidated after universal Hermes path: resolved by official import/adopt recovery.
- false auth-check live_ok: fixed earlier; live_ok accepted only after live readiness proof.
- false auth-recover already_valid: fixed earlier.
- Cloudflare-blocked device-code UI recovery: no longer used as automatic recovery path.
- public 502: resolved by starting canonical openscript-agent-lab-ui.service.

### Remaining notes

- unrelated agent-packages/** dirty state remains present and untouched.
- if user does not visually see Telegram message_id=155, this is not reflected in server-side persisted runtime state.
- thread/topic metadata is not persisted or passed on the delivery path; no current proof of topic mismatch, but also no topic telemetry.

### Current next roadmap direction

Do not continue auth/voice/send fixes unless a new proof shows a new issue.

Possible next blocks:
1. Normal Telegram text regression proof through the same universal Hermes path.
2. Optional redacted delivery telemetry for thread/topic/message metadata if Telegram topic visibility needs future debugging.
3. Move to the next planned roadmap block after Telegram voice acceptance.

Before main feature work continues, still import:
- rules pack;
- module map / safe boundaries;
- prompt templates if needed.

<!-- ROADMAP_APPEND_END id=RM_20260516_IMPORTED_ROADMAP_V0_7_CURRENT -->

<!-- ROADMAP_APPEND_BEGIN id=RM_20260516_EXPAND_TZ_FIN_TOOL_TAB_AGENT_FARM_AND_AGENT_TOOLS source=chatgpt_inline_product_update accepted_by_user=yes -->

## 2026-05-16 — Product direction expanded: “Фин инструмент”, Agent Farm and Agent Tools

### Context

The user clarified the next project direction and corrected the UI placement.

The financial tool must not be created as a separate new tab.

The current UI tab named “Телеграмм” is already specialized around the financial agent workflow, Telegram input and voice. It should become the “Фин инструмент” tab.

This is a documentation/product-direction update only.
No implementation is included in this update.

### Current priority order

1. Re-evaluate the Telegram user_id allowlist task card:
   - include placement in the current “Телеграмм” tab, to be renamed/treated as “Фин инструмент”.

2. Close access to the Telegram bot:
   - Telegram user_id allowlist UI/access control;
   - deny unknown users before resource use;
   - use from.id/user_id, not chat_id, as identity;
   - place this in “Фин инструмент”.

3. Build the universal Agent Farm:
   - many agents;
   - separate agent tasks;
   - task runtime;
   - task assignment;
   - execution tracking;
   - monitoring of completion/failure/repair needs.

4. Add first major agent business tool:
   - Financial Agent Business Tool;
   - not just a database;
   - database + scripts + receipt ingestion + reports + safe tool contract;
   - financial agents must call this tool and must not write SQL directly;
   - product surface belongs under “Фин инструмент”.

5. Add future tool families:
   - Telegram Post Publisher Agent/Tool;
   - YouTube Parsing Agent/Tool;
   - Additional task tools TBD.

### Status

- “Фин инструмент” tab direction: PLANNED / NEEDS_TASK_CARD_REEVALUATION / NEEDS_DESIGN / NEEDS_PROOF.
- Telegram user_id allowlist: pending task-card re-evaluation.
- Agent Farm / Task Runtime: PLANNED / NEEDS_DESIGN / NEEDS_PROOF.
- Financial Agent Business Tool: PLANNED / NEEDS_DESIGN / NEEDS_PROOF.
- Telegram Post Publisher: PLANNED / NEEDS_DESIGN / NEEDS_PROOF.
- YouTube Parser: PLANNED / NEEDS_DESIGN / NEEDS_PROOF.
- Other future tools: PLANNED_PLACEHOLDER / NEEDS_SPEC.

### Rules

- Do not create a separate new tab for the financial tool if the current “Телеграмм” tab is the intended financial tool surface.
- Do not implement Agent Farm before closing bot access and completing proof/design.
- Do not implement Financial Tool as a raw DB exposed to agents.
- Do not let agents write SQL or mutate DB directly.
- Do not mix Telegram access-control with Telegram post publishing.
- Do not implement YouTube parsing without separate vendor/legal/API docs proof.
- Do not mark any new tool family DONE from this docs update.

### Next step

Still next:
- task-card re-evaluation for `telegram_user_id_allowlist_ui`;
- the re-evaluation must include the “Фин инструмент” tab placement/rename decision.

After allowlist:
- design/proof for Agent Farm / Task Runtime.

<!-- ROADMAP_APPEND_END id=RM_20260516_EXPAND_TZ_FIN_TOOL_TAB_AGENT_FARM_AND_AGENT_TOOLS -->

<!-- ROADMAP_APPEND_BEGIN id=RM_20260517_WORKFLOW_RULES_RISK_BASED_COMBINED_RUNS source=chatgpt_inline_user_clarification accepted_by_user=yes -->

## 2026-05-17 — Workflow optimization: risk-based combined runs

The project workflow is updated to reduce unnecessary Codex runs.

Old default:
- separate proof/design before most fixes.

New default:
- docs-only runs remain docs-only;
- narrow ordinary fixes may use combined proof/design/fix in one run;
- high-risk or unclear tasks still require separate design approval.

For the Telegram user_id allowlist line:
- after task-card readiness, prefer a guarded combined proof/design/fix run if scope is narrow;
- if exact affected modules are unclear or high-risk paths are involved, STOP before editing.

<!-- ROADMAP_APPEND_END id=RM_20260517_WORKFLOW_RULES_RISK_BASED_COMBINED_RUNS -->

<!-- ROADMAP_APPEND_BEGIN id=RM_20260517_DEMOTED_TASK_CARDS_FROM_BLOCKING_GATE source=chatgpt_inline_user_clarification accepted_by_user=yes -->

## 2026-05-17 — Workflow optimization: task cards no longer block by themselves

Task cards are now advisory planning/checklist docs, not the primary permission gate.

Primary implementation gate:
- docs gate;
- combined-run guard;
- exact affected modules;
- allowed scope;
- tests/checks.

For Telegram user_id allowlist:
- do not run a separate prompt only to flip task-card readiness;
- rerun as guarded combined proof/design/fix;
- stale `ready_for_fix_run: false` must not block by itself.

<!-- ROADMAP_APPEND_END id=RM_20260517_DEMOTED_TASK_CARDS_FROM_BLOCKING_GATE -->

<!-- ROADMAP_APPEND_BEGIN id=RM_20260517_FIN_INSTRUMENT_FIRST_FINANCIAL_TOOL_DESIGN_PROPOSED source=codex_proof_design accepted_by_user=pending -->

## 2026-05-17 — Priority correction: Fin Instrument first

The active roadmap is corrected:

- do not move directly to a universal Agent Farm / Task Runtime yet;
- first finish the financial agent / “Фин инструмент” line;
- for the current stage, the financial runtime belongs inside the “Фин инструмент” tab;
- after Fin Instrument is progressed, decide whether future runtime is common for all agents, per-tool, or hybrid;
- Financial Tool remains a deterministic business tool: scripts, storage, reports and audit, not direct agent-owned SQL;
- Telegram Post Publisher and YouTube Parser stay later.

<!-- ROADMAP_APPEND_END id=RM_20260517_FIN_INSTRUMENT_FIRST_FINANCIAL_TOOL_DESIGN_PROPOSED -->

<!-- ROADMAP_APPEND_BEGIN id=RM_20260519_CONTEXT_TOOLS_VOICE_STATUS source=chatgpt_inline_project_update accepted_by_user=yes -->

## 2026-05-19 — CONTEXT / TOOLS / VOICE project status update

### Main tasks

The active Telegram-Hermes-Fin work is now tracked through three explicit tasks:

1. **CONTEXT**
   - The next Telegram turn must see the full receipt context:
     `receipt_draft`, `receipt_item_lines`, last action/result, and prior assistant reply.
   - It must not see only the total amount.

2. **TOOLS**
   - Telegram live agent must be Hermes tool-capable.
   - Fin tools must be available to the selected agent.
   - The model must be able to choose tools semantically.
   - Tools read/write DB.
   - Tool result returns to the model/agent.

3. **VOICE**
   - Voice must be a universal transport/tool capability.
   - Voice must not be a separate business-logic branch.
   - Voice must be: audio -> transcript -> canonical text/Hermes agent/tool path.

### Completed

CONTEXT is reported live-ready:
- commit: `8cdba40`
- receipt context hydration now carries:
  - `receipt_draft`
  - `receipt_item_lines`
  - `last_action_result`
  - `prior_assistant_reply`

TOOLS is reported live-ready:
- commit: `fb6f892569dc78db5d24bc8541d297fc9ab22556`
- Telegram Fin-capable path now carries non-empty enabled toolsets.
- `fin.receipt` is Hermes-visible.
- `receipt_current`, `receipt_items`, `receipt_confirm`, `last_receipt` are registered and dispatch in tests.

Docs context for the pending next prompt is saved:
- commit: `ea0bc2b4e03b12f1895c9520ca8ad24fbfd0a1fe`
- context append id: `CTX_20260519_CONTEXT_TOOLS_VOICE_PENDING_PROMPT_V1`

### Current active blocker

VOICE remains unresolved.

Latest voice proof found:
- voice update reaches STT and model request;
- failure is not polling or STT;
- provider rejected tool name `fin.expense_add`;
- provider requires tool names matching `^[a-zA-Z0-9_-]+$`;
- root cause: invalid provider tool-name serialization.

### Next step

Run:

`OPENSCRIPT_AGENT_LAB_VOICE_AS_UNIVERSAL_HERMES_TOOL_CAPABILITY_20260519_01`

This run must:
- make voice a universal transport/tool capability;
- route transcript into the same canonical text/Hermes agent/tool loop as text;
- preserve CONTEXT and TOOLS fixes;
- implement generic provider-safe tool-name mapping if required;
- avoid agent-specific hardcode.

### Not next

Do not continue:
- confirmation-word fixes;
- OCR/item parser work;
- receipt-specific voice branches;
- UI work;
- DB schema work;
- unrelated task-card implementation.

<!-- ROADMAP_APPEND_END id=RM_20260519_CONTEXT_TOOLS_VOICE_STATUS -->

<!-- ROADMAP_APPEND_BEGIN id=RM_20260520_RECEIPT_FULL_EXTRACTION_ACTIVE_BLOCKER source=chatgpt_inline_project_update accepted_by_user=yes -->

## 2026-05-20 — Receipt full extraction becomes active blocker

### Context

Recent Telegram/Hermes/Fin work proved the live routing chain far enough for receipt photos to reach `receipt_photo_draft` through Hermes.

The current active blocker moved from Telegram/auth/routing to receipt extraction quality.

### Proven current facts

- Latest real receipt photo reached the bot.
- It was routed to the selected agent.
- `receipt_photo_draft` was called.
- No stale draft/context was used.
- Hermes replied based on the tool result.
- Telegram delivery worked for the reply.

### Current failure

The visible product receipt contained total and item lines, but the tool result had:

- `amount=null`
- `item_count=0`
- wrong or suspicious date from OCR.

The first failing step was classified as:

`OCR_total_missing`

The selected OCR text did not contain a usable total line, so parser returned `amount=null`.

### Important product correction

The receipt tool must not extract only the final total.

Per project ТЗ, the deterministic business layer must own the full financial facts. For receipts this means extracting, when visible:

- merchant;
- date/time;
- total;
- item names;
- quantities;
- item unit prices;
- item sums;
- tax/payment facts if available;
- truthful missing_fields when OCR cannot recover data.

### Next technical block

Next run should be a shared receipt extraction proof/design/fix:

- retain OCR diagnostics/artifacts safely;
- improve OCR candidate generation/scoring;
- improve amount parsing for values like `1 189.63`;
- improve date/time parsing robustness;
- improve product item-line extraction;
- extract item names, quantities, unit prices and item sums;
- test on multiple product receipt fixtures;
- keep business logic deterministic;
- keep Hermes as language/explanation layer only.

### Not next

- not Telegram pause fix unless new proof says polling is broken;
- not auth fix unless new proof says auth is broken;
- not all-agent routing proof unless new proof says routing is broken;
- not hardcoding one receipt;
- not only final total extraction.

<!-- ROADMAP_APPEND_END id=RM_20260520_RECEIPT_FULL_EXTRACTION_ACTIVE_BLOCKER -->

## 2026-05-21 — “Ютуб” subtitles tool MVP completed and manually accepted

The previous planned YouTube tool direction has now produced a working first MVP.

Completed capability:

- `youtube.subtitles_get`
- YouTube subtitles/transcript extraction with timings by video URL.

Completed layers:

- vendor mechanism selected and documented: `youtube-transcript-api`;
- deterministic executor implemented;
- Hermes-visible tool registration implemented;
- operator UI tab `Ютуб` implemented;
- manual operator subtitle test implemented;
- language fallback implemented: `ru -> en -> any available transcript`;
- UI-based agent attachment implemented;
- Squidward attachment via UI completed;
- manual Telegram proof completed: user confirmed the agent returned subtitles in Telegram.

Current roadmap status for first YouTube capability:

- IMPLEMENTED
- UI_CONNECTED
- AGENT_ATTACHABLE_VIA_UI
- MANUALLY_TELEGRAM_PROVEN

Still not part of this completed MVP:

- video download;
- audio download;
- ASR over YouTube audio;
- YouTube Data API;
- OAuth/API key flow;
- cookies;
- proxies;
- yt-dlp;
- channel parsing;
- playlist parsing;
- mass scraping.

Possible future YouTube extensions:

1. Telegram-safe chunking/continuation for long transcripts.
2. Summary/outline/search modes on top of factual subtitle segments.
3. Explicit transcript export formats.
4. Additional per-agent UI polish.
5. Applying the tool to other agents through UI.
6. Regression proof for new YouTube provider failures.

Next project step:

Do not loop on YouTube implementation unless the user reports a new failure.

Return to the broader active project task list:

- VOICE as universal path;
- TOOLS in voice/text without breakage, including provider-safe names;
- CONTEXT preserved in every turn.

The YouTube subtitles path is now a successful example of a Hermes-visible tool connected through UI and proven through Telegram.

## 2026-05-21 — New roadmap block: Telegram AI/Vibecoding Publisher Agent

After the successful “Ютуб” subtitles MVP, a new product direction was accepted for planning:

Telegram public-channel agent for neural networks, AI tools, coding agents, and vibe coding.

### Roadmap placement

This is a future staged content pipeline.

Do not jump directly to autonomous publishing.

### Next active block

`youtube_research_pipeline`

First technical step:

- evaluate/select the search provider for `youtube.search_candidates`;
- design the database schema/state lifecycle for YouTube research candidates;
- implement search/storage only after provider proof/design.

### Planned staged tools

1. `youtube.search_candidates`
   - search YouTube;
   - store metadata;
   - deduplicate by `video_id` and other keys.

2. `youtube.collect_subtitles_for_candidates`
   - call existing `youtube.subtitles_get`;
   - store transcript segments/full text/status.

3. `youtube.rank_candidates`
   - deterministic sorting/filtering;
   - no LLM required.

4. `youtube.editorial_evaluate`
   - LLM-based editorial evaluation over already collected facts and transcripts.

### Later blocks

Not next:

- Telegram post composer;
- illustration generation;
- Telegram publisher;
- publication status finalization;
- autopost scheduling.

These must be separate future tools/design blocks.

### Acceptance direction for next block

The next block should produce:

- provider choice/proof for YouTube search;
- schema/state design for candidate storage;
- no automatic publishing;
- no monolithic all-in-one tool;
- no hardcoded agent/channel/query/provider.

---
## RM_20260601_POST_YOUTUBE_TG_FIXES_AND_CODEX_RUN_RULES

### Status
The post-20260530 work closed several runtime blockers around YouTube search/readiness, ranking pool consistency, cleanup semantics, and global Telegram/Hermes liveness.

### Completed after previous roadmap append
1. YouTube search now completes the useful workflow to rank-ready candidates:
   - `Запусти поиск` through Telegram/Hermes can produce candidates available for ranking.
   - Search auto-runs the needed readiness/enrichment step when `description_full` is required.
   - Metadata-only storage is not accepted as completed search.

2. Rank pool consistency fixed:
   - `available_to_rank` and the real rank candidate pool use one shared source-of-truth.
   - If available_to_rank is sufficient and target_count is 13, ranking can produce 13.
   - Live proof ranked 13/13 through Telegram/Hermes.

3. Cleanup recent-days fixed:
   - cleanup means candidates collected during the last N calendar days;
   - N=1 means today;
   - cleanup protects approved/rejected/deferred/finalized/carry-forward candidates;
   - dry-run and apply were proven through Telegram/Hermes/tool actions with real Telegram message_ids.

4. Global Telegram no-reply fixed:
   - live poller cursor duplicate logic was corrected;
   - bot replies again to `Кто ты?` and `Запусти модерацию`;
   - root cause was stale cursor handling, not YouTube-specific logic.

### Current roadmap guardrails
Do not reopen as active unless fresh proof shows they are broken:
- YouTube search timeout / metadata-only search;
- YouTube rank target mismatch;
- cleanup recent-days / Hermes-only proof;
- Telegram global no-reply caused by stale poller cursor;
- receipt/OCR route, unless the user explicitly switches back to receipt extraction;
- Kilo/CLI backend exploration, because the user canceled that task.

### Process guardrail for future implementation runs
For runtime/user-flow tasks, source changes plus unit tests are not enough. Codex must also prove the working product chain. For agent/tool tasks, proof must go through:
Telegram/user input -> project handler -> selected agent -> Hermes -> existing tool/facade action -> deterministic business layer -> user-visible reply or equivalent product output.

Direct routes, DB writes, scripts, UI clicks, manual Telegram sends, reply_to_agent-only results, and fallback paths that bypass Hermes/tool architecture are not accepted as live proof.

### Next-step rule
The next technical block must be chosen from current user request plus current docs alignment. Do not answer “next stage” by taking a stale historical roadmap block in isolation.

## 2026-05-22 — YouTube search agent tool visibility fixed

The YouTube Research search/intake pipeline and the agent/Hermes attach path are now proven and the final visibility blocker is resolved.

### Status

The search tool is now attachable to selected agents through the `Ютуб → Поиск видео` UI and the final Hermes visibility blocker was fixed in the search gate/profile detection path.

### Completed in this block

- YouTube search/intake pipeline implemented:
  - saved UI profile;
  - deterministic filters;
  - deduplication;
  - SQLite candidate storage;
  - candidate metadata capture.
- Full-description enrichment implemented as a separate stage over saved candidates.
- Test candidate DB cleaned after proof runs while preserving the search profile.
- `youtube.search_candidates` made attachable to agents via UI/source-package/runtime/Hermes path.
- Hermes wrapper propagation fixed universally on UI startup.
- Final search-tool visibility bug fixed in the search gate/profile detection path.
- Agent began seeing `youtube.search_candidates` after fix and service restart.

### Important resolved blocker

The final blocker was not session refresh, wrapper propagation, runtime apply, Telegram routing, or registry metadata.

The resolved root cause:

`youtube.search_candidates` gate used static `paths.HERMES_HOME.resolve()` instead of live per-profile `hermes_constants.get_hermes_home()`. This made the search gate return `profile_missing` under live per-profile HERMES_HOME and caused the safe registry to filter out the tool before gateway discovery.

Fix commit:

`df3a3b009132ada4ff3ada75178a97e46fd2a686`

### Rejected session fix

A session/tool-context fix was considered but rejected for this issue.

Reason:

The missing search tool was not caused by session lifecycle. It was filtered before session construction by the search gate returning `profile_missing`.

Do not implement session refresh/invalidation for this bug unless a future proof shows a separate real session lifecycle failure.

### Current active next step

Manual user acceptance test:

- In Telegram, ask Squidward:
  `запусти поиск ютуб по сохранённому профилю и покажи результат`.

Expected:

- Squidward sees the tool;
- calls `youtube.search_candidates`;
- uses saved UI profile;
- runs search + enrichment;
- returns a factual summary and candidate preview.

### Next technical phase after manual acceptance

If the Telegram tool execution succeeds:

1. Design metadata pre-evaluation/ranking stage:
   - input: title, channel, URL, description_snippet, description_full, search profile metadata;
   - output: keep/reject/maybe, relevance score, reason;
   - no publication yet.

2. Later stages:
   - subtitle collection for selected candidates;
   - editorial summary/post drafting;
   - image generation;
   - Telegram publication.

### Not next

Do not reopen:

- session reset as a product fix;
- wrapper propagation for this issue;
- runtime apply for this issue;
- Telegram routing for this issue;
- search DB cleanup;
- YouTube subtitles tool implementation.

Do not implement publication/ranking/subtitles until the current search agent tool is manually accepted.

<!-- ROADMAP_APPEND_BEGIN id=RM_20260522_YOUTUBE_SELECT_CANDIDATES_CURATOR_RUNTIME_UI_PROGRESS source=chatgpt_inline_project_update accepted_by_user=yes -->

## RM_20260522_YOUTUBE_SELECT_CANDIDATES_CURATOR_RUNTIME_UI_PROGRESS

### Status

The YouTube Research pipeline has advanced from search/intake and visibility fixes into the selection/curation stage.

Completed layers:

1. `youtube.select_candidates` deterministic response-only contract.
2. Selection lifecycle storage.
3. Protected `youtube_curator` source package.
4. Offline selector-to-curator boundary.
5. `youtube_curator` runtime profile creation.
6. Read-only YouTube Curator UI/status panel.
7. Source-policy editor for `youtube_curator/rules.md`.
8. Apply preview/apply controls in `Ютуб → Сортировка`.

### Current active product block

Current active block:

`youtube_select_candidates_curator_configuration_before_live_hermes`

The user should be able to configure curator policy before any live Hermes-backed curator test.

Current UI flow:

1. open `Ютуб → Сортировка`;
2. edit `youtube_curator/rules.md`;
3. save source policy;
4. run `Предпросмотр apply`;
5. run `Применить правила в runtime`;
6. only after that, proceed toward live Hermes adapter proof/design.

### Next technical block

Next technical block after manual UI/policy/apply verification:

`youtube_select_candidates_live_hermes_curator_adapter_design`

This must be a separate proof/design because it touches live Hermes/profile/provider boundaries.

It must not start by calling provider/model.

It must first prove:

- runtime profile readiness;
- exact Hermes invocation owner;
- candidate snapshot shape;
- curator response schema;
- validation and failure handling;
- no next editing/formatting tool call;
- no Telegram publication;
- no memory write unless separately designed.

### Not next

Not next:

- Telegram router fix;
- YouTube search provider redesign;
- subtitles tool redesign;
- image generation;
- Telegram publishing;
- editing/formatting tool implementation;
- auto-mode;
- memory learning/reset;
- live provider/model call without readiness proof;
- direct DB bypass.

### Acceptance for future live curator work

Future live curator work is acceptable only if:

- policy was saved and applied to runtime;
- `youtube_curator` runtime profile exists and is healthy;
- candidate snapshot contains only stored facts;
- source policy outranks learned memory;
- runtime memory is profile-local;
- `youtube_curator` does not browse YouTube;
- `youtube_curator` does not publish to Telegram;
- `youtube_curator` does not call the next tool;
- `youtube.select_candidates` remains the only writer to selection storage;
- `next_tool_called` remains false.

<!-- ROADMAP_APPEND_BEGIN id=RM_20260528_YOUTUBE_RANKED_MODERATION_LIFECYCLE_FIXED source=chatgpt_dialogue_and_codex_reports -->
## 2026-05-28 — YouTube ranked batch lifecycle fixed; sorting/stack semantics clarified

Roadmap update:
The YouTube moderation active block moved from callback debugging back to sorting/ranked batch lifecycle. The accepted product model is:
1. Search stores candidates.
2. Explicit UI/backend start ranking/selection action creates durable ranked batch.
3. Configured stack size controls how many already-ranked cards are shown per stack.
4. Inline “Следующий стек” shows the next configured stack from the same ranked batch.
5. Curator is not called again while the active batch has pending rows.
6. New ranking is only considered after active batch exhaustion.
7. If no eligible candidates exist after exhaustion, return needs_new_search/no_eligible_candidates.
8. Empty selection / zero persisted rows is structured failure, not ok=true.

Completed implementation report:
- RUN_ID: OPENSCRIPT_AGENT_LAB_FIX_YOUTUBE_RANKED_BATCH_LIFECYCLE_AND_CONFIGURED_STACK_SIZE_20260528_01
- RESULT: SUCCESS
- COMMIT: e21a6874ee864a79ad4f2221b6ee4a8a3d723753
- Changed modules:
  - agent_lab/youtube_agent_moderation_dispatch.py
  - agent_lab/youtube_select_candidates.py
  - agent_lab/youtube_selection_moderation_service.py
  - related unit tests
- Proof:
  - live runner reused active batch select-e9b53dfe41a3;
  - selector/provider were not called;
  - moderation card was sent;
  - zero-row success path blocked.

Not next:
- Do not return to Telegram callback testing unless the user asks after verifying current moderation flow.
- Do not run new search/ranking just to test buttons.
- Do not mix receipt/OCR active blocker with YouTube ranked moderation unless current task explicitly switches domain.

Potential next docs/product task:
Decide whether to extend ТЗ with a separate Telegram bot command for manual “start ranking/selection run”. Current ТЗ documents UI/backend start ranking action, Telegram continue moderation command, and inline next stack; it does not clearly define a separate Telegram command for ranking launch.
<!-- ROADMAP_APPEND_END id=RM_20260528_YOUTUBE_RANKED_MODERATION_LIFECYCLE_FIXED -->
END_ROADMAP_APPEND_TEXT

## RM_20260526_YOUTUBE_RANKED_MODERATION_STACKS_ACCEPTED

### Status
Accepted product design for the next YouTube Research phase.

The current implementation already has:
- stored YouTube candidates in SQLite;
- `youtube.select_candidates`;
- Hermes-backed `youtube_curator`;
- agent/Hermes tool registration for selection;
- policy editor and runtime apply controls.

The current implementation still lacks:
- direct UI launch of selection as a business action;
- durable ranked moderation queue;
- Telegram inline moderation over ranked stacks;
- final approved output persistence for the next script/tool.

### Accepted next product behavior
The YouTube selection stage must become:

stored candidates
→ `youtube.select_candidates`
→ Hermes-backed YouTube Curator ranking
→ durable ranked batch
→ moderation stacks
→ Telegram/UI approve/reject/defer
→ finalize approved result
→ next script/tool consumes approved output

### Key decisions
- Runtime apply is not sorting launch.
- Showing the next moderation stack must not rerun search or ranking.
- Telegram command to continue moderation must only show the next stack from existing ranked state.
- UI and Telegram must share one backend moderation service and one database state.
- The agent must not mutate SQL directly.
- The backend controls target count and stack size.
- Source policy controls ranking preferences.
- Approved result must be stored durably for the next pipeline step.
- Clear/reset must clear ranked moderation/output state, not accidentally delete the whole candidate database.
- `youtube.select_candidates` must not call post editing, formatting, or publishing tools.

### Next technical phase
`youtube_ranked_selection_moderation_queue_design`

This phase must proof/design:
- current selection DB schema;
- ranked batch persistence;
- moderation stack pagination;
- status transitions: pending, approved, rejected/banned, deferred, finalized;
- final approved output shape;
- UI actions;
- Telegram inline callbacks;
- Telegram command to continue moderation;
- clear/reset semantics.

### Not next
Do not implement Telegram publication.
Do not implement post generation.
Do not implement image generation.
Do not call the next editing/formatting tool from `youtube.select_candidates`.
Do not rerun YouTube search or ranking when the operator only asks for the next moderation stack.
Do not add fake/offline/mock paths.

<!-- ROADMAP_APPEND_BEGIN id=RM_20260528_RECEIPT_FULL_EXTRACTION_ACTIVE_BLOCK source=chatgpt_dialogue_and_codex_reports -->
## RM_20260528_RECEIPT_FULL_EXTRACTION_ACTIVE_BLOCK

### Status

The active blocker has moved to full receipt extraction.

This is a Financial Instrument / deterministic business-layer block.

### Completed / proven before this block

The current receipt photo path reached the correct high-level chain:

- Telegram received the photo;
- selected agent received the photo;
- Hermes invoked `receipt_photo_draft`;
- the first proven failure is OCR/parser extraction, not Telegram/Hermes routing.

### Current blocker

Receipt extraction currently fails to extract a full usable structure.

Known failing case:

- visible receipt total: `1 189.63`;
- tool result: `amount=null`;
- tool result: `item_count=0`;
- OCR did not provide a usable total line;
- OCR date candidate was `28.05.2025`, while the visible receipt indicated a different expected date.

### Next technical block

Next technical block:

`receipt_full_extraction_proof_design_fix`

Target fields:

- merchant;
- date;
- time if visible;
- final total;
- item names;
- quantities;
- unit prices;
- line sums;
- payment facts;
- tax facts if visible;
- `missing_fields` for anything not honestly recoverable.

### Required approach

The next run must start with proof of current OCR/preprocessing/parser behavior.

It must locate the current source owner before editing.

Likely source areas:

- `agent_lab/fin_instrument/**`;
- `vendor/hermes-agent/tools/fin_receipt_tool.py`;
- `tools/hermes_vendor_overlay/hermes-agent/tools/fin_receipt_tool.py`;
- receipt OCR/parser tests under `tests/`.

### Not next

Not next unless fresh proof makes them first broken:

- Telegram pause fix;
- Telegram auth fix;
- Hermes auth/provider fix;
- Telegram send fix;
- selected-agent routing fix.

Not acceptable:

- extracting only final total;
- treating one receipt image as a one-off;
- letting Hermes invent financial facts;
- returning no item rows without honest `missing_fields`.

### Acceptance direction

A future receipt fix is accepted only when:

- deterministic business layer returns structured receipt draft;
- total/date/item row extraction is tested;
- missing fields are explicit;
- Hermes/agent only explains/asks confirmation over factual tool output;
- Telegram chain remains functional after the run.
<!-- ROADMAP_APPEND_END id=RM_20260528_RECEIPT_FULL_EXTRACTION_ACTIVE_BLOCK -->

<!-- ROADMAP_APPEND_BEGIN id=RM_20260529_YOUTUBE_RANKED_BATCH_ACTIVE_STATUS_CORRECTION source=chatgpt_dialogue_and_codex_reports -->
## RM_20260529_YOUTUBE_RANKED_BATCH_ACTIVE_STATUS_CORRECTION

### Status

The current active phase is YouTube ranked batch moderation lifecycle and the related product/docs gap.

This correction supersedes the earlier `receipt_full_extraction` active phase for the current working stop-point.

### Current active phase

YouTube ranked batch moderation lifecycle:

- search stores YouTube candidates in DB;
- ranking/selection is a separate UI/backend operator action;
- Curator/Hermes ranks/selects from stored DB facts;
- backend persists a durable ranked batch;
- moderation stack is a slice from the existing ranked batch;
- inline `Следующий стек` reads the next configured stack from the same ranked batch;
- inline `Следующий стек` does not run search, enrichment, Hermes ranking, or `youtube.select_candidates`;
- while an active/resumable ranked batch has pending rows, new Curator ranking is blocked;
- empty selection or zero persisted rows must not be `ok=true`.

### Open product/docs gap

Decide whether documentation should define a separate Telegram command for starting ranking, or keep ranking start as a UI/backend operator action while Telegram only continues moderation and serves inline next stack.

### Not active now

- `receipt_full_extraction`;
- Telegram/auth/Hermes restart work;
- callback debugging;
- unrelated Fin Instrument receipt business-layer work.
<!-- ROADMAP_APPEND_END id=RM_20260529_YOUTUBE_RANKED_BATCH_ACTIVE_STATUS_CORRECTION -->

<!-- ROADMAP_APPEND_BEGIN id=RM_20260530_YOUTUBE_CANDIDATES_BASE_UI_CLEANUP_AND_MODERATION_SEMANTICS source=chatgpt_dialogue_and_codex_reports -->
## RM_20260530_YOUTUBE_CANDIDATES_BASE_UI_CLEANUP_AND_MODERATION_SEMANTICS

### Status

The current active phase remains YouTube ranked batch moderation lifecycle, with a docs-memory refresh for the candidate-base UI cleanup and the ranking/moderation counter semantics.

### Accepted current product state

- `База / кандидаты` now shows only:
  - `Загружено в последнем поиске`
  - `Доступно к ранжированию`
- `Загружено в последнем поиске` is sourced from `latest_search_summary.stored_new_count`.
- Null `latest_search_summary` must render safely as `—` / `нет данных`.
- `Доступно к ранжированию` is sourced from `selection_overview.available_for_selection_count`.
- Candidate table is paginated:
  - page size 10;
  - previous/next controls;
  - replace current page rows rather than accumulating.
- Frontend must not request `limit=50` for the candidates list.
- Frontend must not render or request more than 20 candidate rows in one call.

### Accepted moderation semantics

- `Доступно к отправке на модерацию` is `active_batch.counts.pending_count + active_batch.counts.ranked_count`.
- `Доступно к ранжированию` is still the selection-overview count, not a stack-size count.
- Future active ranked batches supersede previous active batches and archive old rows.
- Contract sanitizer hardening remains accepted:
  - unknown `skipped_video_ids` and `rejected_video_ids` do not abort ranking;
  - unknown `selected_video_ids` still hard-fail;
  - validator remains enabled;
  - no hardcoded video IDs were added.
- `/agent-lab/api/youtube/moderation/batches` keeps the route-specific nginx timeout of 300s for read/send.

### Current stop-point

The open product/docs question remains whether ranking start should become a separate Telegram command or stay a UI/backend operator action while Telegram continues moderation and inline next stack.

### Proven implementation reference

- Latest UI cleanup commit: `1ba686b1d00e6d9dbe71fddbb0df8f3bf2a20092`
- No application code is changed by this roadmap memory block.
<!-- ROADMAP_APPEND_END id=RM_20260530_YOUTUBE_CANDIDATES_BASE_UI_CLEANUP_AND_MODERATION_SEMANTICS -->

<!-- ROADMAP_APPEND_BEGIN id=RM_20260601_YOUTUBE_POST_DRAFT_PREPARATION_TOOL source=chatgpt_inline_product_update -->
## YouTube Post Draft Preparation Tool

### Status

Planned next YouTube pipeline stage after search, ranking, selection and moderation.
This stage is separate from `youtube.select_candidates` and separate from publication.

### Purpose

The new tool `youtube.prepare_post_draft` turns already selected and moderated YouTube videos into durable Telegram post drafts.

The tool must produce:
- coherent Telegram post text from verified source facts and subtitles/transcript;
- image brief and image prompt;
- generated illustration through an explicit image adapter;
- Telegram moderation preview with inline controls;
- approved-for-publication queue item for a future publication tool.

### Architecture boundary

Do not overload `youtube.select_candidates`.
Do not publish posts from this tool.
Do not merge selection, editorial generation, image generation, Telegram moderation and publication into one god module.

Deterministic business/tool code owns:
- post draft storage;
- lifecycle state;
- Telegram dispatch and callback state;
- source snapshot persistence;
- image adapter calls;
- anti-repeat checks;
- queue handoff to publication.

The internal system agent owns editorial reasoning only.

### Internal system agent

Tentative internal agent:

`youtube_post_editor_agent`

This internal agent is not a public Telegram persona.
It should be built as multiple focused skills, one skill per responsibility:

1. `source_fact_reader`
   - reads verified source facts and must not invent facts.
2. `transcript_digest`
   - turns transcript/subtitles into structured digest and key points.
3. `telegram_editorial_writer`
   - writes the Telegram post draft.
4. `telegram_style_guard`
   - validates readability, length, facts and tone.
5. `image_brief_writer`
   - creates image brief, prompt, negative prompt and style tags.
6. `image_generation_requester`
   - prepares structured image generation requests without hidden backend choice.
7. `moderation_packager`
   - prepares Telegram moderation preview payload and durable callback actions.

### Image generation adapter

Add an explicit deterministic adapter, tentative name:

`post_draft_image_adapter`

Supported backend modes:
- `codex_imagegen_cli`
- `openai_image_api`

Contract:
- same prompt contract works for both modes;
- backend choice is explicit via config, policy or operator action;
- if CLI quality is poor or runtime proof fails, the same system may switch to OpenAI API without changing editorial logic;
- adapter records backend mode, prompt, output asset ref, generation status, error and regeneration attempts.

### Storage / lifecycle

Suggested entity:

`youtube_post_drafts`

Suggested lifecycle states:
- candidate_ready_for_draft;
- draft_created;
- text_regeneration_requested;
- image_prompt_created;
- image_generation_requested;
- image_generated;
- image_generation_failed;
- moderation_sent;
- text_regeneration_pending;
- image_regeneration_pending;
- approved_for_publication;
- rejected_or_needs_changes;
- published_later.

Recommended policy:
- source candidates/videos remain in DB forever;
- approved/selected videos are not deleted after drafting or moderation;
- already selected/approved videos must not be selected again;
- draft regeneration creates a revision/version, not a duplicate source candidate.

### Telegram moderation

Preview should include:
- image/media message if available;
- full text draft message;
- inline controls.

Inline actions:
- approve draft;
- regenerate text;
- regenerate image;
- regenerate both;
- reject / needs changes;
- show source;
- next draft.

Callback payloads must reference durable draft ids.

### Publication queue

Publication is a separate future tool.

After approval:
- `moderation_status = approved_for_publication`;
- `published_at = null`;
- `publication_status = ready`.

The publication tool will consume only approved, unpublished drafts.

### Roadmap stages

1. Docs/TЗ import.
2. Proof/design run for current source owners, storage, Telegram callback path, image backend proof.
3. Storage/lifecycle implementation.
4. Internal editor agent package and skills.
5. Draft text generation.
6. Image prompt generation.
7. Image backend adapter with `codex_imagegen_cli` and `openai_image_api`.
8. Telegram moderation preview and inline callbacks.
9. Approved-for-publication queue handoff.
10. Repeat proof from selected candidate to approved draft queue without publishing.

### Acceptance

Do not mark this stage done until:
- anti-repeat is preserved;
- durable drafts are created from approved videos;
- image generation works through a proven backend;
- moderation and regeneration work through durable draft state;
- publication remains separate.
<!-- ROADMAP_APPEND_END id=RM_20260601_YOUTUBE_POST_DRAFT_PREPARATION_TOOL -->

<!-- ROADMAP_APPEND_BEGIN id=RM_20260601_YOUTUBE_POST_DRAFT_UI_OPERATOR_FIRST_ORDER source=chatgpt_inline_product_update -->
## UI-first / operator-first order for `youtube.prepare_post_draft`

### Status
The post-draft tool now has a documented operator-first implementation order.

### Completed
- storage/lifecycle foundation;
- protected internal editor-agent package and skills.

### Next
- UI/operator proof-design for the `Редакторская оценка` tab.

### Then
- UI implementation for draft list, status, and actions;
- draft text generation behind operator controls;
- image prompt and image adapter wiring behind operator controls;
- Telegram moderation preview and callbacks;
- approved-for-publication queue;
- only after those proofs, external/public agent tool exposure.

### Explicitly not next
- external/public agent exposure;
- Telegram command start;
- publication;
- automatic background publishing.

### Tool lifecycle rule
For future tools when applicable:
operator UI first;
durable state and manual controls;
repeat proof;
then optional external-agent exposure.
<!-- ROADMAP_APPEND_END id=RM_20260601_YOUTUBE_POST_DRAFT_UI_OPERATOR_FIRST_ORDER -->

<!-- ROADMAP_APPEND_BEGIN id=RM_20260601_YOUTUBE_POST_DRAFT_EDITOR_LIVE_GATE_SKELETON source=chatgpt_inline_product_update accepted_by_user=yes -->
## 2026-06-01 — YouTube Post Draft Preparation Tool: editor live-gate skeleton

ROADMAP_APPEND_ID: RM_20260601_YOUTUBE_POST_DRAFT_EDITOR_LIVE_GATE_SKELETON

### Current active phase

`youtube_post_draft_editor_live_gate_skeleton`

The YouTube Post Draft Preparation Tool has advanced from UI-first/operator-first design into a staged editor execution pipeline.

### Completed in the current dialogue branch

- Storage/lifecycle foundation for `youtube_post_drafts`.
- Idempotent draft shell creation for selected/approved YouTube candidates.
- Workflow-first operator UI under `Ютуб → Редакторская оценка`.
- Bulk `Создать посты` flow.
- Passive `Готовы к публикации` queue semantics.
- Removal of misleading `Передать в публикацию` action.
- C1 deterministic content harness.
- C2a durable transcript snapshot persistence.
- C2b-1 editor input/output contract and validator.
- Protected internal `youtube_post_editor_agent` source package readiness.
- Runtime profile creation and repeat-proof for `youtube_post_editor_agent`.
- Source policy allowing internal execution while remaining protected/non-public.
- Provider defaults/model mapping readiness for `gpt-5.4-mini`.
- C2b-2A injected fake editor execution adapter.
- Guarded live route skeleton:
  - `POST /api/youtube/post-drafts/editor-execute-live`;
  - explicit `HERMES_EDITOR_LIVE` confirmation;
  - readiness/precondition fail-closed guards;
  - injected runner boundary;
  - no default live runner;
  - no real Hermes/provider/model call.

### Next roadmap block

Next allowed block:

`youtube_post_draft_controlled_live_smoke_proof_design`

This block must be proof/design first and separately user-approved before any live model call.

### Not next

The following are not next unless the user explicitly changes direction and fresh proof supports it:

- Fin Instrument / receipt OCR work.
- Telegram callback debugging.
- image generation.
- Telegram moderation send.
- publication tool implementation.
- external/public agent exposure.
- automatic live model execution.
- direct provider/model call from service code.

### Acceptance criteria for the next live-smoke proof/design

A future live-smoke proof/design must define:

- exact draft/input fixture;
- explicit operator/admin confirmation;
- max one controlled live execution unless otherwise approved;
- no Telegram send;
- no image generation;
- no publication;
- no runtime apply;
- no public exposure;
- validation through the existing C2b-1 validator before persistence;
- safe failure handling;
- report with exact live-call result and whether output was stored.
<!-- ROADMAP_APPEND_END id=RM_20260601_YOUTUBE_POST_DRAFT_EDITOR_LIVE_GATE_SKELETON -->

<!-- ROADMAP_APPEND_BEGIN id=RM_20260602_YOUTUBE_POST_EDITOR_LIVE_SOURCE_INVISIBLE_SUCCESS source=chatgpt_inline_project_update accepted_by_user=yes -->
## 2026-06-02 — YouTube Post Draft Preparation Tool: live source-invisible success and manual review path

ROADMAP_APPEND_ID: RM_20260602_YOUTUBE_POST_EDITOR_LIVE_SOURCE_INVISIBLE_SUCCESS

### Current active phase

`youtube_post_draft_editor_live_source_invisible_success`

The YouTube Post Draft Preparation Tool has advanced from guarded live-gate skeleton into a proven controlled live workflow for the current prepared post draft.

### Completed in the current dialogue branch

- source-invisible editorial/news draft rules are now visible to the live editor context;
- the visible post text is standalone and does not rely on source recap framing;
- `source_facts_used` grounding is canonicalized before validation when the request carries complete grounding;
- the final live editor execution succeeded once and persisted the draft for manual review;
- the draft remains `ready_for_moderation` / `needs_review`;
- `approved_at`, `published_at`, and `publication_status` remain null;
- no Telegram send, image generation, approval, or publication happened in the live step.

### Next roadmap block

Next allowed block:

`youtube_post_draft_manual_review_and_illustration_path_after_live_success`

This block is manual-review first and must keep the saved draft as the primary proof artifact.

### Not next

The following are not next unless the user explicitly changes direction and fresh proof supports it:

- receipt OCR/full extraction;
- Fin Instrument;
- Telegram routing/auth debugging unless fresh proof shows it is first broken;
- runtime apply;
- public/private repo publication changes outside docs sync;
- automatic approval or publication;
- a second live editor execution;
- any visible-source-metadata requirement in the final draft text.

### Acceptance criteria for the next block

A future manual-review / illustration path must define:

- review of the persisted standalone news draft in the UI;
- acceptance or rejection based on visible editorial quality;
- controlled illustration generation only after acceptance;
- no public docs/content drift;
- no reintroduction of recap/source-reference wording into the visible post;
- no validator gate that blocks manual-review drafts solely because the visible text is source-invisible.
<!-- ROADMAP_APPEND_END id=RM_20260602_YOUTUBE_POST_EDITOR_LIVE_SOURCE_INVISIBLE_SUCCESS -->
<!-- ROADMAP_APPEND_BEGIN id=RM_20260604_YOUTUBE_POST_DRAFT_MODERATION_REVISION_FLOWS source=chatgpt_inline_project_update accepted_by_user=yes -->
## 2026-06-04 — YouTube Post Draft Preparation Tool: moderation/editor revision flow after live source-invisible success

ROADMAP_APPEND_ID: RM_20260604_YOUTUBE_POST_DRAFT_MODERATION_REVISION_FLOWS

### Current active phase

`youtube_post_draft_moderation_revision_flows`

The YouTube Post Draft Preparation Tool is now in the post-live moderation/revision stop-point for a non-approved draft.

### Completed in the current dialogue branch

- live source-invisible editor success remains preserved as the previous saved state;
- the current fresh evidence is a text-revision confirmation, not an image-revision confirmation;
- the current moderation draft target is `post-draft-2479cdb8ffb4`;
- the visible moderation card message id is `952`;
- the draft remains non-approved and not published.

### Next roadmap block

Next allowed block:

`youtube_post_draft_text_revision_flow_for_non_approved_posts`

This block must preserve the existing titled image and rewrite only the caption/text for the moderation resend.

### Not next

The following are not next unless the user explicitly changes direction and fresh proof supports it:

- image revision flow, unless the callback/log/screenshot proves the `image` action was clicked;
- publication;
- approval;
- another candidate;
- Telegram auth/Hermes auth;
- receipt OCR/full extraction;
- Fin Instrument work;
- external/public repo exports outside docs sync.

### Acceptance criteria for the next block

A future text-revision block must define:

- caption rewrite only;
- same titled image reused;
- full Telegram photo+caption+buttons moderation card resent or replaced;
- caption remains within Telegram photo caption limits;
- draft remains not approved and not published;
- image revision stays a separate later block unless fresh proof proves the image action;
- prompt/report wording must mention the exact visible Telegram text-revision confirmation before choosing the next step.
<!-- ROADMAP_APPEND_END id=RM_20260604_YOUTUBE_POST_DRAFT_MODERATION_REVISION_FLOWS -->
## RM_20260605_YOUTUBE_POST_DRAFT_REVISION_REPEAT_PROOF_AND_MANUAL_CALLBACK_INTAKE
### Status
The YouTube Post Draft Preparation Tool has advanced beyond the earlier text-revision-only stop-point.

### Completed since RM_20260604
- Text revision for a non-approved post draft now has:
  - real completion path;
  - explicit per-cycle completion markers;
  - stale-state retry;
  - fresh-cycle repeat behavior after completion;
  - strict grounding normalization;
  - readable Telegram caption formatting.
- Repeated text revision was proven with real moderation message transitions.
- Image revision now has:
  - live image regeneration;
  - titled image regeneration;
  - repeated image cycle proof;
  - UI preview support for titled assets.
- Request-stage UX was corrected so request status is sent before long generation work.
- Raw `codex exec failed` from the image backend is sanitized into safe provider-failure text and remains retryable.
- Polling was re-enabled through the official project control path after bot paused/live disabled state was proven.

### Current active phase
`youtube_post_draft_manual_callback_identity_current_card_proof`

### Current blocker
The deployed request-timing/image-failure fix at `ce34fd2b70a10c4a64f9b3180d05637d8a02a67e` could not be manually verified because no real manual `callback_query` was observed during the proof window.

Polling was ready, but callback intake for the user's manual click was not captured.

### Next roadmap block
Run a proof-only current-card callback identity test:
1. prove current source/service/polling state;
2. identify active bot identity if safe;
3. identify current post-draft moderation row;
4. refresh or create one current moderation card through the official project-owned moderation delivery path;
5. record the fresh `moderation_message_id`;
6. ask the user to click exactly that fresh card;
7. prove whether callback arrives for that message id;
8. if no callback arrives, diagnose bot/card/chat/webhook/getUpdates/offset/client mismatch.

### Not next
- no new Telegram listener;
- no text revision business fix unless fresh callback proof reaches that layer and proves it broken;
- no image revision business fix unless fresh callback proof reaches that layer and proves it broken;
- no publication;
- no approval queue implementation;
- no receipt/OCR;
- no Fin Instrument;
- no Hermes/auth/provider work unless fresh proof makes it first broken.

### Acceptance for next block
The next block is complete only when:
- a fresh current moderation card message id is known;
- the user click is tied to that exact message id;
- real callback either arrives and is traced, or its absence is proven for that exact current card;
- no simulated callback is counted as final proof;
- no direct service/business call is counted as proof.
END_ROADMAP_APPEND_TEXT
<!-- ROADMAP_APPEND_BEGIN id=RM_20260605_YOUTUBE_POST_DRAFT_REVISION_REPEAT_PROOF_AND_MANUAL_CALLBACK_INTAKE source=chatgpt_inline_project_update accepted_by_user=yes -->

## RM_20260608_YOUTUBE_PREPARE_POST_DRAFT_ATTACHABLE_TOOL_EDITOR_QUEUE_PROVEN

SOURCE_KIND: chatgpt_dialogue_delta_verified_against_repo_docs
DATE_UTC: 2026-06-08
ACTIVE_PHASE: youtube_prepare_post_draft_attachable_tool_editor_queue_proven
PREVIOUS_PHASE_SUPERSEDED: youtube_post_draft_manual_callback_identity_current_card_proof

### Roadmap status update

The YouTube post-draft branch has advanced beyond the 2026-06-05 manual callback identity/intake stop-point.

The current accepted technical state is:

* `youtube.prepare_post_draft` is now a public attachable Hermes tool.
* The active normal agent `plankton` has the tool connected through source package and runtime apply.
* UI operator attach control exists in `Ютуб → Редакторская оценка`.
* Hermes model tool visibility is fixed for explicit prepare-post-draft requests.
* The model-visible function name is `youtube_prepare_post_draft`.
* The public/source tool id remains `youtube.prepare_post_draft`.
* `list_ready_drafts` returns categorized post-draft lifecycle buckets.
* `list_editor_queue` returns full editor queue:

  * ready-for-creation YouTube candidates;
  * existing post-draft lifecycle buckets.

### Closed roadmap slices

Closed/proven:

1. Post-draft image/text revision and moderation callback work no longer blocks the active line.
2. Approve/return-to-work DB lifecycle is understood:

   * approve = ready for future publication;
   * no immediate publication;
   * published_at remains null;
   * return-to-work does not delete durable rows.
3. Public tool identity is corrected:

   * `youtube.prepare_post_draft` = attachable tool;
   * `youtube_post_editor_agent` = internal/system editor agent inside the tool.
4. Hermes callable wrapper exists.
5. Source attach exists.
6. Runtime apply to `plankton` was performed.
7. Manual UI attach block is visible and reports connected/applied.
8. Hermes tool-call is proven through simulated Telegram chain.
9. `list_ready_drafts` lifecycle buckets are fixed.
10. `list_editor_queue` full editor queue is added and proven.

### Current active blocker / stop-point

No code blocker is currently proven after `list_editor_queue`.

Current human stop-point:

* manual review of the final Telegram response from the `list_editor_queue` proof.

The response should show:

* ready-for-creation candidates: 2
* current drafts: 3
* ready-for-publication drafts: 3
* total work items: 5

### Next technical block after acceptance

If the user accepts the Telegram response, the next technical block must be selected explicitly.

Likely next valid block:
`youtube_prepare_post_draft_ready_candidate_creation_flow`

Scope:

* create durable post drafts from ready-for-creation candidates;
* mutating action;
* must require proof/design and DB lifecycle safety;
* must not publish;
* must not bypass Hermes/tool path if user-facing agent/tool flow is being proven.

Possible later block:
`youtube_post_publication_tool_design`

Scope:

* publication remains separate from `youtube.prepare_post_draft`;
* must not be silently folded into prepare-post-draft actions.

### Not-next blocks unless user explicitly switches

Do not restart by default:

* receipt/OCR/full extraction;
* Fin Instrument;
* Telegram auth;
* Hermes auth;
* provider setup;
* old YouTube search/subtitles/select implementation;
* ranking command docs question;
* publication;
* image timeout tuning;
* 2026-05-05 callback identity proof.

### Acceptance criteria for next mutating post-draft creation block

A future creation flow is acceptable only if:

* it proves current ready candidate source and filters;
* it uses deterministic business layer for DB writes;
* it keeps source candidates durable;
* it creates or reuses post-draft rows idempotently;
* it does not publish;
* it reports exactly what rows were created/reused;
* it uses simulated Telegram/project handler proof if the user flow is agent/tool driven;
* it does not use direct Python/DB/shell as final proof.

### Invalid outcomes

Invalid:

* agent invents draft facts;
* tool publishes posts;
* tool deletes source candidates;
* `youtube_post_editor_agent` is exposed as normal public tool;
* UI-only success without business proof;
* direct DB write as proof;
* fake Telegram message id;
* fallback after Hermes failure;
* old tools modified without fresh proof.

## RM_20260610_TELEGRAM_PUBLICATION_TWO_BOT_AND_ADMIN_TRIGGER_READY
SOURCE_KIND: chatgpt_dialogue_delta_verified_against_repo_docs
DATE_UTC: 2026-06-10
ACTIVE_PHASE: telegram_publication_admin_live_send_trigger_source_ready_pending_main_integration
PREVIOUS_PHASE_SUPERSEDED: youtube_prepare_post_draft_attachable_tool_editor_queue_proven

### Roadmap status update
The active roadmap phase has moved from YouTube prepare_post_draft/editor queue work to Telegram Publication / TG poster controlled live-send enablement.

### Completed since RM_20260608
1. `telegram.publication` became a Hermes-visible safe tool with list/ingest/plan actions only.
2. The old Router bot was restored and later proven through split-token runtime proofs.
3. YouTube no-placeholder/editor continuation was fixed and deployed. The stuck draft resumed from persisted editor output, generated image, and sent moderation.
4. Telegram two-bot token split was implemented and integrated:
   - Router token role separated from Publication token role.
   - Publication no longer falls back to Router/legacy token.
5. Runtime was migrated to three Telegram env keys:
   - `TELEGRAM_BOT_TOKEN`;
   - `TELEGRAM_ROUTER_BOT_TOKEN`;
   - `TELEGRAM_PUBLICATION_BOT_TOKEN`.
6. Post-migration Router proof succeeded with real Telegram reply message id `1063`.
7. Publication token/config visibility was proven redacted.
8. Live-send design found the actual product blocker:
   no normal product/admin live-send trigger existed.
9. Source branch now adds the missing normal admin/product trigger:
   `POST /api/telegram-publication/run-cycle`.
10. The new trigger is preview-by-default, requires explicit `confirm_live_send: true` for live send, caps first proof to one post, and routes through the existing business layer.

### Current active blocker / stop-point
The admin live-send trigger source branch is ready but not integrated into main.

Source branch:
`feature/telegram-publication-admin-live-send-trigger-20260610-agent1`

Source commit:
`481fa4ee4ce862245142144098629dbf7094b91e`

Expected current main before integration:
`c47f2c62be26998c7f1c6de9d3ab0185cd65b49e`

### Next roadmap block
`telegram_publication_admin_live_send_trigger_main_integration`

The next technical run should integrate the source branch into `origin/main`.

### Acceptance criteria for next block
The next source-integration block is complete only if:
- source commit `481fa4ee4ce862245142144098629dbf7094b91e` is integrated into main;
- final main preserves TG poster tool, YouTube continuation fix, and two-bot token split;
- `POST /api/telegram-publication/run-cycle` is present;
- default/no-confirm path does not send;
- explicit live path remains confirmation-gated;
- first proof cap remains one post;
- endpoint uses business-layer run-cycle/send-execution;
- endpoint does not call Telegram API directly;
- Hermes tool remains no-live-send;
- tests pass;
- no runtime deploy;
- no Telegram send;
- no env/token changes.

### Following blocks after integration
After source integration:
1. runtime deploy/proof of the new endpoint without live send;
2. preview/dry-run proof through the admin endpoint;
3. separately approved first live send proof through the normal admin endpoint with exactly one controlled send.

### Not next
- no live publication send in the integration run;
- no direct internal business-layer call as product proof;
- no direct Telegram API;
- no Hermes tool live-send action;
- no token migration redo;
- no YouTube continuation redo;
- no Fin Instrument/receipt/OCR.

## RM_20260614_TELEGRAM_PUBLICATION_ADMIN_TRIGGER_SOURCE_INTEGRATED_PENDING_RUNTIME_PROOF
SOURCE_KIND: chatgpt_dialogue_delta_verified_against_repo_docs
DATE_UTC: 2026-06-14
ACTIVE_PHASE: telegram_publication_admin_trigger_source_integrated_pending_runtime_proof
PREVIOUS_PHASE_SUPERSEDED: telegram_publication_admin_live_send_trigger_source_ready_pending_main_integration

### Roadmap status update
The source integration for the Telegram Publication admin trigger is complete in private `main`.

### Completed since RM_20260610
1. Private source commit `fcde3149e4baa0ba6a01664e1ba029da0e1399f4` was created and pushed to `origin/main`.
2. Only the four expected backend/test files were committed:
   - `agent_lab/admin_server.py`
   - `agent_lab/telegram_publication_run_cycle.py`
   - `tests/test_admin_server.py`
   - `tests/test_telegram_publication_run_cycle.py`
3. The endpoint contract remains in source:
   - `POST /api/telegram-publication/run-cycle` exists;
   - preview/dry-run is default;
   - live send requires `confirm_live_send: true`;
   - first live proof remains capped to `max_posts=1`;
   - endpoint delegates through the business-layer run-cycle/send-execution path;
   - endpoint does not call Telegram API directly;
   - endpoint does not read/print token values;
   - endpoint does not hardcode agent/user/chat/provider/message_id.
4. The Hermes `telegram.publication` tool remains no-live-send.
5. No runtime deploy, restart, live send, or env/token changes were performed.
6. Frontend/auth work is explicitly out of scope for this repo and was not touched.

### Current active blocker / stop-point
Source is integrated, but runtime/product proof is still pending.

### Next roadmap block
`telegram_publication_admin_trigger_runtime_endpoint_proof`

The next technical run should be a proof-only source-vs-runtime / endpoint availability check.

### Acceptance criteria for next block
The next proof block is complete only if:
- the running service exposes `POST /api/telegram-publication/run-cycle`;
- no live send is attempted;
- no Telegram API call is made;
- the proof is strictly read-only unless a later approved deploy run is explicitly created;
- if the endpoint is absent in runtime, stop and propose a separate deploy/restart design/proof.

### Not next
- do not live send;
- do not call Telegram API directly;
- do not call Hermes tool live-send paths;
- do not change source for this docs-only run;
- do not touch frontend/auth work.
