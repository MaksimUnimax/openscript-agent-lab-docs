TITLE: Technical Spec Extension v0.6 — Telegram AI/Vibecoding Publisher Agent and YouTube Research Pipeline
STATUS: PROPOSED_PRODUCT_SPECIFICATION
SOURCE_KIND: chatgpt_inline_user_clarification
DATE: 2026-05-21
RELATION_TO_TZ_V0_3: extends v0.3, does not replace it
CURRENT_IMPLEMENTATION_STATUS: NOT_IMPLEMENTED
CURRENT_DOC_STATUS: SPECIFIED_FOR_FUTURE_DESIGN
PRODUCT_DIRECTION: telegram_ai_vibecoding_publication_agent
FIRST_TECHNICAL_BLOCK: youtube_research_pipeline

# Technical Spec Extension v0.6 — Telegram AI/Vibecoding Publisher Agent

## 1. Why this update exists

The user defined the next product direction after the first “Ютуб” subtitles tool MVP was completed and manually proven through Telegram.

The new direction is a future agent that helps run a Telegram public channel about:

- neural networks;
- AI tools;
- coding agents;
- vibe coding;
- developer workflows around AI.

This extension records the product concept and staged tool architecture before implementation.

## 2. High-level product goal

The future agent should help prepare Telegram-publication content by:

1. finding relevant YouTube videos;
2. collecting subtitles/transcripts;
3. storing video metadata and transcripts in a database;
4. deduplicating already-known and already-published sources;
5. ranking and sorting candidates;
6. using an LLM/editorial step to evaluate whether a candidate is worth posting;
7. later turning approved candidates into Telegram-ready posts;
8. later generating a suitable illustration;
9. later publishing to a selected social platform, initially Telegram.

This is a staged pipeline. It must not be implemented as one uncontrolled “agent searches and posts by itself” action.

## 3. Current completed dependency

The first completed dependency is:

- `youtube.subtitles_get`

Current accepted status:

- implemented;
- operator UI exists;
- can be attached to an agent through UI;
- manually proven through Telegram with Squidward returning subtitles.

The new YouTube Research pipeline must reuse this completed subtitles capability instead of reimplementing subtitle collection.

## 4. Next technical block

The next technical block is:

`youtube_research_pipeline`

The first implementation focus is not Telegram publishing and not image generation.

The first implementation focus is:

- search for YouTube videos;
- save candidate video metadata to a database;
- collect subtitles using the existing `youtube.subtitles_get` capability;
- store transcripts;
- deduplicate and sort candidates;
- expose candidates for later editorial/posting steps.

## 5. Tool/stage split

The YouTube Research pipeline should be split into separate deterministic tools/stages.

### 5.1 `youtube.search_candidates`

Purpose:

Search YouTube for relevant videos and store candidate metadata in the project database.

Input examples:

- query profile;
- raw query string;
- language/region hints;
- freshness window;
- max results;
- optional channel/source profile.

Output:

- stored candidate count;
- new candidate count;
- duplicate/skipped count;
- normalized candidate metadata;
- search provider audit.

Must store at least:

- video id;
- canonical URL;
- title;
- channel id if available;
- channel name;
- published date/time or best available published text;
- duration if available;
- views if available;
- thumbnail if available;
- search query/profile;
- first seen time;
- last seen time;
- source provider.

### 5.2 `youtube.collect_subtitles_for_candidates`

Purpose:

For stored candidates, collect subtitles using existing `youtube.subtitles_get`.

This stage must not reimplement subtitle logic.

It should store:

- language returned;
- source type;
- timestamped segments;
- full text with timestamps;
- transcript hash;
- collection time;
- normalized error if subtitles are unavailable.

### 5.3 `youtube.rank_candidates`

Purpose:

Deterministically rank/filter stored candidates.

Inputs:

- metadata;
- transcript presence;
- channel/source metadata;
- publication status;
- duplicate indicators;
- topic rules.

Rules should consider:

- not already published;
- transcript available;
- freshness;
- channel trust/blacklist/whitelist;
- title/topic match;
- duration;
- novelty;
- duplicate/published penalties.

This stage should not call an LLM.

### 5.4 `youtube.editorial_evaluate`

Purpose:

LLM-assisted editorial evaluation over already collected factual data.

This stage may use LLM only after candidate metadata and transcript are available.

It must evaluate:

- relevance to AI/neural networks/vibe coding;
- whether the content is worth a Telegram post;
- possible post angle;
- useful summary points;
- risk flags;
- recommended priority.

The LLM must not search YouTube and must not invent source facts. It evaluates already collected data.

### 5.5 `youtube.select_candidates`

### Purpose

`youtube.select_candidates` selects a small number of already stored YouTube candidates for the next pipeline stage.

It is not a search tool.

It is not a publishing tool.

It is not the next editing/formatting tool.

It consumes stored candidate facts and returns selected candidate IDs plus lifecycle/status information.

### Initiation

The tool is called through the Hermes/tool contract.

A future public-manager agent may initiate it.

The system sorting operator inside the tool performs the selection work.

The tool must also remain testable and controllable through product/operator surfaces later, but this must not become a separate direct DB bypass.

### System sorting operator

The selection tool may use a dedicated system Hermes operator / curator profile.

This profile is the internal evaluator for candidate selection.

It has:

- source-managed policy;
- skills;
- profile-local Hermes learned memory;
- learned taste from prior approvals/skips/rejections.

It must evaluate only stored factual candidate snapshots.

It must not browse YouTube.

It must not invent facts.

It must not publish to Telegram.

It must not call the next formatting/editing tool.

### Future public-manager agent

The future public-manager agent is separate from the system sorting operator.

The public-manager agent may call `youtube.select_candidates`, receive selected candidates, and later decide whether to call the next independent editing/formatting tool.

`youtube.select_candidates` must not make that decision itself.

### Optional human review

A human review layer may be added later if review mode is enabled.

In that case, MVP review buttons are exactly:

- `✅ Подходит`
- `⏭ Пропустить`
- `❌ Не подходит`

The MVP must not include:

- `📄 Нужны субтитры`
- `📝 Причина/заметка`

### Status transitions

`✅ Подходит`:

- candidate becomes approved;
- candidate becomes ready for next stage;
- candidate is returned in `selected_candidates`.

`⏭ Пропустить`:

- candidate is skipped for the current batch;
- candidate may enter cooldown/not-in-current-batch state;
- candidate is not permanently rejected.

`❌ Не подходит`:

- candidate is rejected;
- candidate must not be suggested again unless an explicit reset/reopen path is implemented later.

### Memory and policy

Selection uses three separate layers:

1. **DB facts and lifecycle state**

   Objective candidate metadata, anti-repeat, reviewed markers, approved/skipped/rejected state, ready-for-next-stage state, and published markers.

2. **Source-managed policy**

   Current priority topics, hard exclusions, editorial preferences, and auto-mode gates.

   Policy outranks learned memory.

3. **Hermes learned memory**

   Profile-local learned taste of the system sorting operator.

   Learned memory is a soft bias and must never override DB facts, anti-repeat, published markers, hard negative topics, or current source policy.

### Pipeline separation

`youtube.select_candidates` must not call the next editing/formatting tool directly.

The output of this tool is a structured selected-candidates result.

The caller — future public-manager agent or later product control surface — decides when to start the next tool.

### 5.6 Future chain order

The safe implementation order is:

1. search and store candidate metadata;
2. collect subtitles for stored candidates;
3. deterministic rank/filter;
4. editorial evaluation over stored data;
5. selection with operator review;
6. later editing/formatting;
7. later publication.

The selection stage must only return candidates ready for the next stage.
It must not invoke the next stage itself.

## 6. Shared database/state layer

The database is a shared state layer for the YouTube Research pipeline.

It is not a separate arbitrary tool.

It must track candidate lifecycle and prevent repeats.

Minimum conceptual tables/entities:

### `youtube_videos`

Fields:

- `video_id` unique;
- `canonical_url`;
- `title`;
- `channel_id`;
- `channel_name`;
- `published_at`;
- `duration_seconds`;
- `view_count`;
- `thumbnail_url`;
- `first_seen_at`;
- `last_seen_at`;
- `source_provider`;
- `source_query`;
- `source_profile`;
- `status`;
- `published_at`;
- `published_platform`;
- `published_post_id`;
- `reject_reason`.

### `youtube_transcripts`

Fields:

- `video_id`;
- `language`;
- `source_type`;
- `segments_json`;
- `full_text_with_timestamps`;
- `transcript_hash`;
- `collected_at`;
- `error_code`;
- `error_message`.

### `youtube_candidate_scores`

Fields:

- `video_id`;
- `topic_score`;
- `novelty_score`;
- `freshness_score`;
- `channel_score`;
- `duration_score`;
- `final_score`;
- `scoring_reason`;
- `scored_at`.

## 7. Candidate statuses

Candidate status values should include at least:

- `found`;
- `duplicate`;
- `transcript_pending`;
- `transcript_ready`;
- `transcript_failed`;
- `scored`;
- `queued_for_post`;
- `published`;
- `rejected`;
- `expired`.

Published candidates must not be returned for posting again.

## 8. Retention and anti-repeat policy

The user requested approximately three months of storage for video research data.

Recommended policy:

- keep raw transcripts/full text for approximately 3 months by default;
- keep minimal metadata and published markers longer than 3 months;
- do not delete published `video_id` markers too early, otherwise old content may be rediscovered and reposted;
- store enough metadata for duplicate detection even after transcript cleanup.

Minimum anti-repeat keys:

- `video_id`;
- canonical URL;
- transcript hash when available;
- normalized title hash;
- channel id + normalized title hash.

## 9. Search logic concept

Search must not be a single free-form query chosen by the LLM at runtime.

The pipeline should support query profiles.

Example query profile fields:

- profile id;
- topic label;
- query strings;
- preferred language/region;
- freshness window;
- max results;
- duration preference;
- negative keywords;
- trusted channels;
- blocked channels;
- topic tags.

The initial target content area is:

- neural networks;
- AI coding tools;
- coding agents;
- vibe coding;
- OpenAI/Codex/Cursor/Claude Code style workflows;
- practical AI automation for developers.

## 10. Search provider direction

The first search provider is not selected by this document.

Search provider selection must happen in a separate vendor/docs/proof step.

Candidate provider classes to evaluate later:

- Python YouTube search packages without API keys;
- public frontend APIs such as Invidious or Piped if suitable;
- self-hosted search gateway if needed.

The project should avoid starting with downloader ecosystems such as `yt-dlp` or `pytubefix` unless later proof/design explicitly approves a metadata-only mode.

## 11. Future publication pipeline

The following are future stages, not the next immediate technical block:

- `content.compose_telegram_post`;
- `image.generate_social_visual`;
- `telegram.publish_post`;
- `content.mark_published`.

Publication must not happen automatically until the publishing workflow, safety, approval, and rollback rules are designed.

## 12. Boundaries

The YouTube Research pipeline must remain separate from:

- Fin Instrument / receipt OCR;
- Telegram access control;
- Telegram voice transport;
- Telegram Post Publisher;
- Agent Farm / Task Runtime, unless later explicitly connected.

## 13. Forbidden shortcuts

Do not:

- make one monolithic “search and publish” tool;
- let the LLM freely browse/search YouTube without deterministic storage;
- publish automatically before the publication stage is designed;
- skip deduplication;
- skip published markers;
- store only raw text without video/channel metadata;
- re-fetch subtitles if a transcript is already stored and still fresh;
- return already published candidates for posting;
- hardcode one channel, one query, one agent, one provider, or one Telegram chat;
- mix image generation or Telegram publishing into the YouTube search MVP.

## 14. Current status

Status now:

- Product direction: accepted in chat.
- Technical spec: this extension records the staged concept.
- Implementation: not started.
- Next technical step: evaluate/select YouTube search provider and design `youtube.search_candidates`.

## 2026-05-26 — Accepted design: ranked moderation stacks for YouTube candidate selection

Title:
Accepted design — YouTube ranked moderation stacks

Status:
ACCEPTED_PRODUCT_DESIGN / NOT_IMPLEMENTED_AS_FULL_PIPELINE_YET

Context:
The current `youtube.select_candidates` implementation already reads stored YouTube candidates from SQLite and calls `youtube_curator` through Hermes. The current selector result is planned-only and does not yet persist a full ranked moderation queue or final approved output. The UI currently has policy editing and runtime apply controls, but runtime apply is not the sorting launch.

Accepted product behavior:
The YouTube candidate selection stage must become a ranked moderation pipeline, not just a one-shot selector response.

The pipeline has these stages:

1. Candidate source
Stored YouTube candidates are the source of truth for sorting input.
The selection pipeline must not search YouTube again when showing moderation stacks.
The selection pipeline must not fill the candidate database again when the operator only wants to continue moderation.
The candidate source is the stored candidate pool, currently represented by SQLite candidate storage.

2. Ranking / selection run
A selection run starts by reading stored candidates from the candidate database.
The backend invokes `youtube.select_candidates`.
`youtube.select_candidates` calls YouTube Curator through Hermes.
YouTube Curator ranks/selects candidates according to source-managed policy:
- AI tools;
- LLMs;
- coding agents;
- vibe coding;
- developer automation;
- agentic workflows;
- practical demos and releases.

The exact number of candidates that proceed must be controlled by backend settings or launch parameters, not only by natural-language policy.
The policy explains how to prioritize.
The backend controls how many items are taken.

3. Ranked batch persistence
The ranked output must be saved as a durable selection batch.
A batch must keep enough state to resume moderation without rerunning search or reranking.
The batch should include:
- batch_id / selection_run_id;
- video_id;
- rank/order;
- score/confidence if available;
- curator reason;
- moderation status;
- lifecycle status;
- timestamps.

The batch state must allow:
- pending moderation;
- approved;
- rejected/banned;
- deferred/keep for later;
- finalized/ready for next pipeline step.

4. Moderation stack
Moderation must happen in stacks.
A stack is a slice of the already-ranked batch.
The stack size is controlled by settings or launch parameters.
Example:
- rank 1-5 first stack;
- rank 6-10 next stack;
- rank 11-15 next stack.

Showing the next stack must not rerun:
- YouTube search;
- candidate enrichment;
- Hermes ranking;
- `youtube.select_candidates`.

Showing the next stack only reads the existing ranked batch and returns the next not-finalized, not-banned candidates.

5. Telegram moderation
The moderation flow must support Telegram inline buttons.

Each candidate card should include:
- title;
- channel;
- URL;
- Russian summary/description;
- curator reason;
- rank/priority;
- basic metadata if useful.

The Russian card text can be prepared by the agent/Hermes from stored facts, but the agent must not change the deterministic moderation state directly.

Inline moderation actions:
- Approve;
- Reject / ban;
- Defer / keep for next time;
- Show next stack;
- Return/finalize result.

Meanings:
- Approve: include this video in the approved output for the current batch.
- Reject / ban: do not use this video; mark it as rejected/banned so it does not appear again as a candidate unless explicitly reset.
- Defer / keep for next time: do not include now, but do not ban; allow it to appear in a later stack or later run according to lifecycle rules.
- Show next stack: show the next stack from the same ranked batch without rerunning ranking.
- Return/finalize result: stop waiting for more moderation and produce the final approved output from all approved videos in the batch so far.

6. UI operator moderation
The same moderation operations must be available from the UI:
- start ranking/selection run;
- set target selected count and moderation stack size;
- show current stack;
- show next stack;
- approve/reject/defer candidates;
- finalize/return result;
- clear ranked batch state.

UI and Telegram must use the same backend moderation service and the same database state.
There must not be separate UI-only or Telegram-only business logic.

7. Telegram command to continue moderation
A Telegram bot command must allow continuing moderation without rerunning search or sorting.

Command behavior:
- do not search YouTube;
- do not call ranking again;
- do not refill the candidate database;
- find the active ranked batch or the latest resumable batch;
- show the next stack of not-finalized, not-banned candidates;
- use the configured stack size.

Purpose:
This lets the operator resume moderation later when the ranked batch already contains candidates.

8. Final approved output
When the operator presses Return/finalize result, the system must:
- stop waiting for more moderation commands for that batch;
- collect all approved videos in that batch;
- mark them as ready for the next pipeline step;
- make them available to the next script/tool.

The next script/tool must read the finalized approved output from durable state, not from a transient UI response.

9. Clear ranked batch state
The UI and Telegram moderation surface must provide a clear/reset action for ranked selection state.

Purpose:
Allow the operator to discard old ranked batches and start the full chain again from fresh candidate search/ranking.

Clear/reset must be scoped carefully:
- it should clear ranked selection/moderation/output state;
- it should not accidentally delete the full candidate database unless a separate destructive action is explicitly designed and confirmed.

10. Runtime apply distinction
`Применить правила в runtime` is not a sorting launch.
It only syncs source package policy/docs/skills into the Hermes runtime profile.
The business launch is a separate selection/ranking/moderation action.

Correct operator sequence after editing policy:
1. Save source policy.
2. Apply policy to runtime.
3. Start ranking/selection run.
4. Moderate stack(s).
5. Finalize/return approved result.

11. Agent/tool boundary
The agent must not own SQL or database mutation directly.
The agent may call tools and generate human-readable moderation text.
The deterministic backend layer owns:
- reading candidates;
- persisting ranked batches;
- updating moderation statuses;
- finalizing approved output;
- clearing ranked state.

The same backend service must be callable from:
- UI;
- Telegram inline buttons;
- Telegram commands;
- Hermes/tool path where applicable.

12. Hard prohibitions
The design must not introduce:
- fake/offline/mock sorting paths;
- UI-only selection logic;
- Telegram-only state mutation logic;
- direct SQL controlled by agent text;
- automatic publication from `youtube.select_candidates`;
- automatic call to the next editing/formatting/publishing tool inside `youtube.select_candidates`;
- reranking when only the next moderation stack is requested;
- YouTube search when only continuing moderation is requested.

13. Implementation direction
The next technical phase should design and implement a durable moderation queue/state layer around the existing `youtube.select_candidates` result.

The implementation should likely use or extend existing selection tables:
- `youtube_selection_batches`;
- `youtube_candidate_selection_state`;

or create narrowly-scoped additional tables only if the existing schema is insufficient.

The next phase must start with proof/design of:
- current selection DB schema;
- exact persistence model;
- stack pagination rules;
- moderation status transitions;
- final approved output shape;
- UI actions;
- Telegram inline callback commands;
- Telegram resume command;
- reset/clear semantics.

Do not jump directly to publication.
Do not connect the next post-generation script until approved output persistence is designed and proven.
