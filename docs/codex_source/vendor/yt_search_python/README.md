# yt-search-python

Imported vendor docs for the future `youtube.search_candidates` stage.

This package is the current primary proof candidate for YouTube search metadata retrieval.

It is **not** the final production provider yet.

Local upstream docs live in:

- `docs/codex_source/vendor/yt_search_python/upstream/README.md`
- `docs/codex_source/vendor/yt_search_python/upstream/docs.md`
- `docs/codex_source/vendor/yt_search_python/upstream/search_examples.md`
- `docs/codex_source/vendor/yt_search_python/upstream/pyproject.toml`
- `docs/codex_source/vendor/yt_search_python/upstream/LICENSE`
- `docs/codex_source/vendor/yt_search_python/upstream/pypi.json`

Known safe use for the first YouTube Research block:

- No API Key Required;
- search YouTube videos without YouTube Data API v3;
- keep the first stage limited to search metadata and candidate discovery;
- use search profile parameters from the future `Поиск видео` subtab;
- store candidate metadata in the project database;
- deduplicate and rank later in separate stages.

Explicitly out of scope for the first `youtube.search_candidates` path:

- `Transcript`;
- `StreamURLFetcher`;
- stream/download features;
- video/audio download;
- cookies;
- API keys;
- `yt-dlp`;
- `pytubefix`.

Upstream disclaimer to keep in mind:

- the package uses YouTube internal API behavior and may change without notice.

## Search-only proof candidate facts

The upstream docs show:

- package name: `yt-search-python`;
- import namespace examples use `youtubesearchpython`;
- search classes include `VideosSearch`, `CustomSearch`, and `ChannelSearch`;
- search supports `language` and `region` arguments;
- pagination is available through `next()`;
- filters include upload date, duration, and sort order;
- result metadata can include `video_id`, title, published time, duration, view count, channel name/id/link, video link, thumbnails, and description snippet.

This document intentionally summarizes only the search/metadata subset needed for the future search pipeline.
