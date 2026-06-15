# PROJECT SNAPSHOT

STATUS: BOUNDED_CODEX_REPO_SNAPSHOT
SOURCE_KIND: bounded_codex_repo_snapshot
SNAPSHOT_ID: PROJECT_SNAPSHOT_20260522_YOUTUBE_SEARCH_AGENT_VISIBILITY_FIXED
DATE_UTC: 2026-05-22T05:59:40Z

## Git State

- private source repo HEAD at snapshot: `df3a3b009132ada4ff3ada75178a97e46fd2a686`
- current branch: `main`
- `origin/main` matched `HEAD` before docs edits
- working tree status: dirty outside docs only
- dirty summary: unrelated tracked/untracked changes exist outside docs; none were staged for this docs run
- docs-only snapshot scope: `docs/codex_source/**` only
- no auth files were read
- no secrets were printed

## Current Project Snapshot

- YouTube subtitles tool: implemented, UI-connected, attachable, Telegram-proven
- YouTube search/intake: implemented and operator-proven
- Full-description enrichment: implemented as separate stage over saved candidates
- Search tool attach: implemented through UI/source-package/runtime/Hermes path
- Hermes wrapper propagation: fixed universally via UI startup restore
- Final search visibility blocker: fixed in gate/profile detection
- Fix commit: `df3a3b009132ada4ff3ada75178a97e46fd2a686`
- Current validation stop point: manual Telegram acceptance test for Squidward
- Next technical block after acceptance: metadata pre-evaluation/ranking
- Session-snapshot confusion was a symptom; the actual first broken layer was the search gate/check_fn path

## Repository Shape

Bounded top-level directories observed:

- `agent-packages/`
- `agent_lab/`
- `docs/`
- `tests/`
- `tool-registry/`
- `tools/`
- `vendor/`

## docs/codex_source Status

Current docs roots:

- `docs/codex_source/project/**`
- `docs/codex_source/roadmap/**`
- `docs/codex_source/module_map/**`
- `docs/codex_source/context/**`
- `docs/codex_source/project_snapshot/**`
- `docs/codex_source/rules/**`
- `docs/codex_source/vendor/**`
- `docs/codex_source/task_cards/**`

Current imported direction:

- current technical spec remains v0.3
- roadmap append-only memory now records the YouTube search agent visibility fix as the current active block
- module map append-only memory now records the gate/profile boundary that caused the visibility bug
- current dialogue context now records the final YouTube search fix and the diagnostic lesson
- public docs repo content rule remains `docs/codex_source/**` only

## Notes

- This snapshot is intentionally lightweight.
- It records the current YouTube Research state and the final proven root cause/fix for the visibility issue.
- It does not replace the full project docs, vendor docs, or append-only memory tails.

# Project Snapshot — 2026-05-22 — YouTube Curator selection UI/runtime configuration

SNAPSHOT_ID: PROJECT_SNAPSHOT_20260522_YOUTUBE_CURATOR_UI_READY

## Current active block

`youtube_select_candidates_curator_configuration_before_live_hermes`

## Completed since previous snapshot

- `youtube.select_candidates` contract implemented.
- Selection lifecycle storage implemented.
- `youtube_curator` package created.
- `youtube_curator` protected as system/internal agent.
- Offline selector-to-curator boundary implemented.
- Runtime profile for `youtube_curator` created through source-managed apply.
- Read-only YouTube Curator UI/status panel implemented.
- Source-policy editor for `youtube_curator/rules.md` implemented.
- Apply preview/apply controls implemented using existing runtime apply endpoints.
- Live UI verification showed apply controls are present and `/api/state` remains sanitized.

## Current stop point

The next user-facing step is manual browser verification:

- hard-refresh browser;
- open `Ютуб → Сортировка`;
- verify status panel, policy editor, and apply controls.

The next technical step after manual policy/apply verification is a separate proof/design for live Hermes-backed curator adapter.

## Current hard boundaries

- No live Hermes-backed curator call yet.
- No provider/model call.
- No Telegram API call.
- No YouTube live search.
- No next editing/formatting tool call.
- No auto-mode.
- Runtime memory remains profile-local and is not editable through current UI.
- `system_filter` remains separate and must not be reused as YouTube curator.

# Project Snapshot — 2026-05-28 — YouTube ranked moderation lifecycle

SNAPSHOT_ID: PROJECT_SNAPSHOT_20260528_YOUTUBE_RANKED_BATCH_LIFECYCLE
DATE_UTC: 2026-05-28
STATUS: current_after_youtube_lifecycle_fix

Current project state:
- OpenScript Agent Lab remains Hermes-first, multi-agent, business-layer-owned deterministic state architecture.
- Latest major accepted implementation block: YouTube ranked moderation lifecycle and configured stack size.
- Sorting/ranking lifecycle now separates:
  - ranking target / selected count;
  - moderation stack size;
  - active ranked batch serving;
  - fresh ranking only after batch exhaustion;
  - structured no eligible / empty selection failures.
- Latest accepted commit for this block:
  `e21a6874ee864a79ad4f2221b6ee4a8a3d723753`.
- Telegram callback debugging should not be resumed automatically.
- Current open product/documentation question:
  Should there be a separate Telegram bot command for manual start ranking/selection run, or should ranking launch remain UI/backend only while Telegram handles continue moderation and inline next stack?

# Project Snapshot — 2026-05-28 — Receipt full extraction active block

SNAPSHOT_ID: PROJECT_SNAPSHOT_20260528_RECEIPT_FULL_EXTRACTION_ACTIVE_BLOCK
DATE_UTC: 2026-05-28T14:06:59Z

## Current active block

`receipt_full_extraction`

## Current proven blocker

- receipt OCR/parser extraction fails to produce full structured receipt data

## Important facts

- receipt photo reaches Telegram and the selected agent;
- Hermes invokes `receipt_photo_draft`;
- the failing step is OCR/parser, not Telegram/Hermes routing;
- visible amount `1 189.63` was missed as a usable total;
- tool output had `amount=null` and `item_count=0`;
- the next work is full receipt extraction, not Telegram/Hermes/auth.

## Next recommended run

`OPENSCRIPT_AGENT_LAB_RECEIPT_FULL_EXTRACTION_PROOF_DESIGN_FIX`

# Project Snapshot — 2026-05-29 — YouTube ranked batch active status correction

SNAPSHOT_ID: PROJECT_SNAPSHOT_20260529_YOUTUBE_RANKED_BATCH_ACTIVE_STATUS_CORRECTION
DATE_UTC: 2026-05-29

## Current active block

`youtube_ranked_batch_moderation_lifecycle`

## Current stop-point

- YouTube ranked batch lifecycle / moderation stack is the current working stop-point.
- `receipt_full_extraction` remains historical context only.
- Inline `Следующий стек` is a UI/control action over the same ranked batch, not a Telegram command.
- The open product/docs question is whether ranking start should be a separate Telegram command or remain a UI/backend operator action.

## No code change required

- This is a documentation pointer correction, not an application behavior change.
- No Telegram API, Hermes/provider, DB, or service-runtime change is needed.

# Project Snapshot — 2026-05-30 — YouTube candidates base UI cleanup and moderation semantics

SNAPSHOT_ID: PROJECT_SNAPSHOT_20260530_YOUTUBE_CANDIDATES_BASE_UI_CLEANUP
DATE_UTC: 2026-05-30

## Current active block

`youtube_ranked_batch_moderation_lifecycle`

## Current stop-point

- The current YouTube work stays in the ranked batch moderation lifecycle.
- The visible `База / кандидаты` tab now uses latest search summary data and paginated candidate pages instead of all-time DB/debug counters.
- `latest_search_summary.stored_new_count` is the source for `Загружено в последнем поиске`.
- `selection_overview.available_for_selection_count` is the source for `Доступно к ранжированию`.
- The candidates list uses 10-row pages with previous/next controls and does not accumulate pages.
- The candidates API still exposes `limit`, `offset`, `has_more`, and `latest_search_summary`.
- Sorting/moderation counters remain semantically separate from the base tab.
- The open product/docs question remains whether ranking start should be a separate Telegram command or stay a UI/backend operator action while Telegram continues moderation and inline next stack.

## Current accepted implementation reference

- Latest UI cleanup commit: `1ba686b1d00e6d9dbe71fddbb0df8f3bf2a20092`
- The candidate-base cleanup is a UI/docs state update, not a new Telegram/Hermes/provider/database block.

## Hard boundaries

- No receipt/OCR work is being restarted by this snapshot.
- No live search/ranking is being executed by this docs update.
- No Telegram API, Hermes/provider, DB, or service-runtime change is required for the docs state update itself.

# Project Snapshot — 2026-06-01 — Post YouTube/TG fixes and run rules

SNAPSHOT_ID: PROJECT_SNAPSHOT_20260601_POST_YOUTUBE_TG_FIXES
DATE_UTC: 2026-06-01T02:17:44Z

## Git State

- private source repo HEAD at snapshot: `36d0f6d08c727afc412c9c75e89eac501a14d16e`
- current branch: `main`
- `origin/main` matched `HEAD` before this docs sync
- working tree status: dirty outside docs only
- dirty summary: unrelated tracked/untracked changes exist outside docs; none were staged for this docs run
- docs-only snapshot scope: `docs/codex_source/**` only
- no application code was read or exported for this snapshot
- no auth files were read
- no secrets were printed

## Current Project Snapshot

- Post-20260530 YouTube search/readiness is fixed: search auto-completes readiness/enrichment when needed and can increase `available_to_rank` through Telegram/Hermes proof.
- Rank pool consistency is fixed: `available_to_rank` and the actual rank pool share one source-of-truth, and live proof reached `target_count=13` with `ranked_count=13`.
- Cleanup recent-days is fixed and proven through Telegram/Hermes/tool actions, with `N=1` meaning candidates collected today.
- Global Telegram/Hermes no-reply from stale poller cursor is fixed at commit `36d0f6d08c727afc412c9c75e89eac501a14d16e`.
- Kilo/CLI backend exploration was canceled by the user and is not current active roadmap work.
- Receipt full extraction remains saved as historical/pending context and is not the auto-selected next stage.
- No next product stage is auto-selected by this docs snapshot; the next exact run must follow the next explicit user task and current docs alignment.

## Accepted implementation references

- search/rank-ready/rank-pool: `013deb284a61e2da2cf952060747b8e72b3ede83`
- cleanup recent-days/Hermes-only: `2d95c264da9f0da44b369f8b8cea4022e3af776f`
- Telegram poller liveness: `36d0f6d08c727afc412c9c75e89eac501a14d16e`

## Notes

- This snapshot is docs-only and contains no application code.
- Unrelated dirty files, if any, were not staged.
- No secrets/runtime files were read or exported.
- No next product stage is auto-selected.

## PROJECT_SNAPSHOT_20260615_YOUTUBE_EDITOR_SKILL_SELECTION_EXPERIENCE

Status: append snapshot from ChatGPT dialogue

Current active block:
`youtube_editor_skill_selection_experience_documented_then_fresh_pipeline_restart`

Snapshot summary:
The project has completed a major YouTube post editor skill-selection experiment. The key result is not a final perfect writing style, but a documented set of lessons for future editor-agent work.

Important facts:
- Text regeneration uses source facts and transcript snapshots, not previous draft text as the main input.
- Weak repeated output was therefore caused by editor transformation quality, not source starvation.
- The best current direction is source-to-angle shaping before prose generation.
- Editorial quality diagnostics must remain advisory, not blocking.
- Image/title overlay work is separate from text quality.
- The next immediate task is docs-only memory update.
- The next technical block after docs acceptance is a fresh YouTube pipeline restart using the previous cleanup/full-chain approach.

Safety:
- No application code should be modified during this docs update.
- No provider/model/Telegram/DB actions should run during this docs update.
- Future fresh pipeline run must be separate and explicit.

## PROJECT_SNAPSHOT_20260615_EDITOR_SKILL_DOCS_COMPLETED_FRESH_PIPELINE_NEXT

Status: append snapshot correction from ChatGPT dialogue

Current active block:
`youtube_fresh_pipeline_restart_after_editor_skill_docs_completed`

Snapshot correction:
The YouTube editor skill-selection experience is now documented and no longer blocks the next technical work.

Current next technical block:
A separate safe cleanup + fresh YouTube pipeline restart.

Important guard:
The next run must not start with blind cleanup. It must first prove active/current state and exact rows/items that will be cleared while preserving published/proof history.

Out of scope for the next docs correction:
- application code changes;
- runtime/profile changes;
- provider/model calls;
- Telegram calls;
- DB mutations.

# Project Snapshot — 2026-06-10 — Telegram Publication two-bot migration and admin live-send trigger ready
SNAPSHOT_ID: PROJECT_SNAPSHOT_20260610_TELEGRAM_PUBLICATION_TWO_BOT_AND_ADMIN_TRIGGER_READY
DATE_UTC: 2026-06-10
STATUS: current_after_telegram_publication_admin_trigger_source_ready

## Current active block

`telegram_publication_admin_live_send_trigger_source_ready_pending_main_integration`

## Current project state

OpenScript Agent Lab remains a multi-agent Hermes-first system with separated:
- Agent layer;
- Provider/Hermes layer;
- deterministic business layer;
- Admin UI/API;
- Telegram Router;
- Telegram Publication.

## Completed since previous saved snapshot
- `telegram.publication` safe Hermes-visible tool is integrated and visible.
- Old Router bot was restored and later proven after split-token migration.
- YouTube editor continuation blocker was closed; the stuck draft resumed from persisted editor output, generated image, and sent moderation.
- Telegram two-bot token source split was integrated into main at `c47f2c62be26998c7f1c6de9d3ab0185cd65b49e`.
- Runtime env was migrated to:
  `TELEGRAM_BOT_TOKEN`,
  `TELEGRAM_ROUTER_BOT_TOKEN`,
  `TELEGRAM_PUBLICATION_BOT_TOKEN`.
- Post-migration Router proof succeeded with real Telegram reply message id `1063`.
- Publication token/config presence was proven redacted.
- First live publication send design found there was no normal product/admin live-send trigger.
- Source branch now adds `POST /api/telegram-publication/run-cycle` as a preview-by-default admin product trigger.

## Current stop-point
Source branch:
`feature/telegram-publication-admin-live-send-trigger-20260610-agent1`

Source commit:
`481fa4ee4ce862245142144098629dbf7094b91e`

The branch is ready and pushed, but not yet integrated into main.

## Next technical run
Integrate source branch into `origin/main`.

Expected main before integration:
`c47f2c62be26998c7f1c6de9d3ab0185cd65b49e`.

The integration run must not deploy runtime, call Telegram, call Hermes, call the endpoint live, edit env, or send publication messages.

## Hard boundaries
- No live publication send before source integration and runtime deploy/proof.
- No direct Telegram API.
- No direct Hermes/tool live-send.
- No internal function call as product proof.
- No token values in docs, logs, UI, reports, or public repo.
- No hardcoded target/chat/message id.
- No YouTube continuation redo without fresh proof.

# Project Snapshot — 2026-06-08 — YouTube prepare_post_draft attachable tool and editor queue proven

SNAPSHOT_ID: PROJECT_SNAPSHOT_20260608_YOUTUBE_PREPARE_POST_DRAFT_ATTACHABLE_TOOL_EDITOR_QUEUE_PROVEN
DATE_UTC: 2026-06-08
ACTIVE_BLOCK: youtube_prepare_post_draft_attachable_tool_editor_queue_proven

## Current project state

The YouTube post-draft preparation tool is now proven as an attachable agent tool.

Current facts:

* public tool id: `youtube.prepare_post_draft`
* model-visible callable: `youtube_prepare_post_draft`
* internal/system editor agent: `youtube_post_editor_agent`
* active recipient agent used in proof: `plankton`
* operator UI surface: `Ютуб → Редакторская оценка`
* deterministic business owner: `agent_lab/youtube_post_draft_service.py`
* Hermes wrapper owner: `tools/hermes_vendor_overlay/hermes-agent/tools/youtube_prepare_post_draft_tool.py`

## Completed since previous snapshot/docs point

* callback/image revision work no longer blocks the active line;
* approve/return-to-work DB lifecycle clarified and verified;
* `youtube.prepare_post_draft` callable wrapper implemented;
* source attach metadata implemented;
* active agent `plankton` received the tool in source package;
* runtime apply synced the tool and skill into `plankton` Hermes profile;
* UI manual attach block added and manually verified in browser;
* Hermes visibility fixed by forced tool choice for explicit prepare-post-draft requests;
* `list_ready_drafts` fixed to return categorized post-draft lifecycle buckets;
* `list_editor_queue` added to return full editor work queue:

  * ready-for-creation candidates;
  * existing draft lifecycle buckets.

## Final proven queue counts from dialogue

* ready-for-creation candidates: 2
* current post drafts: 3
* ready-for-publication drafts: 3
* total work items: 5

## Safety and boundaries

* no publication happened;
* no production DB mutation happened during final read-only proofs;
* old YouTube tools were not modified;
* runtime profile was not edited directly;
* provider/model calls were used only where explicitly required for live Hermes/tool proof;
* unit tests did not use provider/model calls;
* final proof used simulated Telegram message through project handler, active agent, Hermes tool call, deterministic service layer, and Telegram delivery.

## Current stop-point

Manual review of the final Telegram response is the only natural acceptance check.

If accepted, the next technical block should be explicitly chosen by the user. The most likely next block is a controlled mutating flow for creating post drafts from ready-for-creation candidates, not publication.

## Not next by default

Do not automatically resume:

* receipt/OCR;
* Fin Instrument;
* Telegram auth;
* Hermes auth;
* old YouTube search/subtitles/select implementation;
* publication;
* 2026-05-05 callback identity proof.

# Project Snapshot — 2026-06-05 — YouTube post draft revision repeat proof and callback intake status

SNAPSHOT_ID: PROJECT_SNAPSHOT_20260605_YOUTUBE_POST_DRAFT_REVISION_AND_CALLBACK_INTAKE
DATE_UTC: 2026-06-05T07:22:51Z

## Current active block

`youtube_post_draft_manual_callback_identity_current_card_proof`

## Current project state

The YouTube Post Draft Preparation Tool is past the earlier text-revision and illustration-revision repeat proof stop-points.

Accepted state now includes:
- repeated text revision cycles with preserved image refs on text-only changes;
- caption grounding normalization and readable paragraph formatting;
- repeated illustration regeneration with fresh `image_asset_ref` and `image_titled_asset_ref`;
- titled image preview support in the operator UI;
- request-status timing fixed so request feedback is sent before the long generation work;
- image backend `codex exec failed` surfacing sanitized into a safe retryable provider-failure state.

Current runtime/proof stop-point:
- the current unresolved blocker is real manual `callback_query` identity/intake for a current moderation card;
- the deployed runtime fix at `ce34fd2b70a10c4a64f9b3180d05637d8a02a67e` was restarted and healthz was OK;
- polling was re-enabled through the official control route;
- subsequent proof windows still did not capture a real manual callback for the current card;
- the next proof must create or refresh one current moderation card, record its `moderation_message_id`, and ask the user to click exactly that card.

## Accepted implementation references

- request timing and image failure surfacing fix: `ce34fd2b70a10c4a64f9b3180d05637d8a02a67e`
- repeated text revision proof and grounding normalization: `9ac59e9c7358f5f530f3732d021bc94d12b69aaa`
- titled image preview support: `de40b115e141870292710171446c69b515b88a2e`
- Telegram connector control audit logging: `a76371c6f867ece52474d2b8d10defd292fd610f`

## Notes

- This snapshot is docs-only and contains no application code.
- Unrelated dirty files, if any, were not staged.
- No secrets/runtime files were read or exported.
- The next technical run is proof-only current-card callback identity/intake, not a text/image source fix by default.

# Project Snapshot — 2026-06-04 — YouTube post draft moderation/editor revision flows

SNAPSHOT_ID: PROJECT_SNAPSHOT_20260604_YOUTUBE_POST_DRAFT_MODERATION_REVISION_FLOWS
DATE_UTC: 2026-06-04T04:07:53Z

## Git State

- private source repo HEAD at snapshot: `6beadd03e56de2dcf49bd9724fc36e7ae77fceb8`
- current branch: `main`
- `origin/main` matched `HEAD` before this docs sync
- working tree status: dirty outside docs only
- dirty summary: unrelated tracked/untracked changes exist outside docs; none were staged for this docs run
- docs-only snapshot scope: `docs/codex_source/**` only
- no application code was read or exported for this snapshot
- no auth files were read
- no secrets were printed

## Current Project Snapshot

- The YouTube post draft moderation/editor pipeline is now the active stop-point after the live source-invisible success state.
- The latest dialogue evidence showed the explicit text-revision confirmation:
  - `✏️ Запрошены правки текста. Черновик поставлен на текстовую доработку.`
- That evidence proves the next technical block is text revision, not image revision.
- Current moderation draft target:
  - `draft_id`: `post-draft-2479cdb8ffb4`
  - `telegram_message_id`: `952`
- The next technical run should rewrite the caption only, keep the same titled image, and resend or replace the full Telegram photo+caption+buttons moderation card.
- The draft remains non-approved and not published.
- Image revision remains a separate later block unless fresh proof shows the image action was clicked.
- Receipt extraction, Fin Instrument, Telegram auth, and Hermes auth are not the current active block.

## Accepted implementation references

- current live-source-invisible editor success baseline: `6beadd03e56de2dcf49bd9724fc36e7ae77fceb8`

## Notes

- This snapshot is docs-only and contains no application code.
- Unrelated dirty files, if any, were not staged.
- No secrets/runtime files were read or exported.
- No next product stage is auto-selected.

# Project Snapshot — 2026-06-01 — YouTube post draft editor live-gate skeleton

SNAPSHOT_ID: PROJECT_SNAPSHOT_20260601_YOUTUBE_POST_DRAFT_EDITOR_LIVE_GATE_SKELETON
DATE_UTC: 2026-06-01T10:52:51Z

## Current active block

`youtube_post_draft_editor_live_gate_skeleton`

## Current project state

The YouTube Post Draft Preparation Tool is the active branch.

The tool now has:
- workflow-first operator UI under `Редакторская оценка`;
- idempotent draft shell creation from selected/approved videos;
- durable transcript snapshot storage;
- editor input/output contract and validator;
- protected internal `youtube_post_editor_agent`;
- runtime profile created and repeat-proven;
- source policy and provider defaults/model mapping ready;
- fake editor execution adapter repeat-proven;
- guarded live editor route skeleton repeat-proven.

## Current stop-point

The guarded live route skeleton is complete and repeat-proven.

No live Hermes/provider/model call has been made.

The next step is only a separately approved live-smoke proof/design run.

## Hard boundaries

- No live model call without explicit user approval.
- No Telegram send.
- No image generation.
- No publication.
- No external/public agent exposure.
- No Fin Instrument / receipt OCR work in this active block.

# Project Snapshot — 2026-06-02 — YouTube post draft editor live source-invisible success

SNAPSHOT_ID: PROJECT_SNAPSHOT_20260602_YOUTUBE_POST_EDITOR_LIVE_SOURCE_INVISIBLE_SUCCESS
DATE_UTC: 2026-06-02T13:21:38Z

## Git State

- private source repo HEAD at snapshot: `3047fb23c403428057466c44929a6f92dd74feac`
- current branch: `main`
- `origin/main` matched `HEAD` before this docs sync
- working tree status: dirty outside docs only
- dirty summary: unrelated tracked/untracked changes exist outside docs; none were staged for this docs run
- docs-only snapshot scope: `docs/codex_source/**` only
- no application code was read or exported for this snapshot
- no auth files were read
- no secrets were printed

## Current Project Snapshot

- The YouTube post draft editor has moved from guarded live-gate skeleton into a proven controlled live workflow.
- The final successful live editor run validated a standalone editorial/news draft and persisted it for manual review.
- Current draft target:
  - `draft_id`: `post-draft-6af43220e9bb`
  - `video_id`: `D67SfjYSMok`
- The saved draft remains `ready_for_moderation` / `needs_review`.
- `approved_at`, `published_at`, and `publication_status` remain null.
- Visible draft text is source-invisible and does not rely on source recap wording.
- Source grounding is preserved through machine-readable `source_facts_used` and snapshots, not visible source metadata in `draft_text`.
- The next step is manual UI review of the persisted draft text, followed only if accepted by the normal illustration path that uses the saved image fields.
- Temporary Hermes timeout/session-correlation diagnostics remain cleanup debt.

## Accepted implementation references

- live editor success / source facts used canonicalization fix: `3047fb23c403428057466c44929a6f92dd74feac`

## Notes

- This snapshot is docs-only and contains no application code.
- Unrelated dirty files, if any, were not staged.
- No secrets/runtime files were read or exported.
- No next product stage is auto-selected.
