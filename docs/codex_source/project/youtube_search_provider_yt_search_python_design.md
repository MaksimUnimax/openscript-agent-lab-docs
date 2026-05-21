# YouTube Search Provider Design Note: `yt-search-python`

STATUS: PROOF_CANDIDATE
SOURCE_KIND: chatgpt_inline_user_clarification
DATE: 2026-05-21
RELATED_PIPELINE: youtube_research_pipeline
RELATED_TOOL_STAGE: youtube.search_candidates
PRIMARY_PROOF_CANDIDATE: yt-search-python
PRODUCTION_PROVIDER_STATUS: NOT_SELECTED

## 1. Why this note exists

The future YouTube Research pipeline needs a search provider proof candidate before implementation of `youtube.search_candidates`.

`yt-search-python` is the current primary proof candidate for that stage.

It is not production-selected as the final provider.

This note records the search-only behavior that may be used for the first proof/design step.

## 2. What this provider candidate is for

Use `yt-search-python` only for:

- discovering candidate YouTube videos;
- collecting search result metadata;
- paging through results;
- applying search filters and profile hints;
- feeding the database-backed candidate pipeline.

Do not use it here for:

- transcript collection;
- video or audio download;
- stream fetching;
- LLM evaluation;
- Telegram publishing.

## 3. Upstream facts that matter for the first stage

The imported upstream docs indicate:

- package name: `yt-search-python`;
- import namespace examples: `youtubesearchpython`;
- search classes: `VideosSearch`, `CustomSearch`, `ChannelSearch`;
- `language` and `region` search arguments are supported;
- pagination uses `next()`;
- filters include upload date, duration, and sort order;
- the README states search works without YouTube Data API v3 / API keys;
- the README disclaimer says it uses YouTube internal API behavior and may change without notice.

## 4. Search profile model for the `Поиск видео` subtab

The `Поиск видео` subtab should expose editable search profile fields for future operator use.

The current design should keep these as UI-editable profile parameters rather than hardcoding one query:

- profile id;
- topic label;
- raw query string;
- language hint;
- region hint;
- freshness window;
- max results;
- duration preference;
- upload-date filter;
- sort order;
- trusted channels;
- blocked channels;
- negative keywords;
- optional channel/source profile.

There is no separate `Настройки` subtab.
Profile settings belong inside the functional `Поиск видео` subtab.

## 5. Candidate metadata expectations

Search results should be normalized into candidate metadata such as:

- `video_id`;
- canonical URL;
- title;
- channel id if available;
- channel name;
- published time or best available published text;
- duration if available;
- view count if available;
- thumbnail if available;
- description snippet if available;
- search query/profile;
- first seen time;
- last seen time;
- source provider.

## 6. Database/state role

`yt-search-python` is only the search provider candidate.

The actual future pipeline must still store candidate state in the shared YouTube research database so that:

- duplicate discovery is deterministic;
- already-published content stays blocked;
- search can be replayed safely;
- transcript collection can reuse existing candidate state.

## 7. Explicit boundary

This is a proof candidate, not final production selection.

The next step after this import is a separate provider proof/design step for `youtube.search_candidates`.

Do not treat this note as approval for full implementation.
