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
