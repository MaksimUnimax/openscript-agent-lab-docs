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
