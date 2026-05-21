# youtube-transcript-api

Imported vendor docs for the planned Hermes-visible tool “Ютуб”.

This vendor package records the concrete transcript mechanism for public YouTube subtitles/transcripts by `video_id`.

Imported upstream docs live in:

- `docs/codex_source/vendor/youtube_transcript_api/upstream/README.md`
- `docs/codex_source/vendor/youtube_transcript_api/upstream/pyproject.toml`
- `docs/codex_source/vendor/youtube_transcript_api/upstream/LICENSE`

Planned use in the “Ютуб” tool:

- extract a YouTube `video_id` from the user-provided URL in deterministic code;
- use `youtube_transcript_api.YouTubeTranscriptApi` to inspect and fetch public subtitles/transcripts;
- keep the first version limited to public transcript retrieval by video id;
- keep YouTube Data API, OAuth, cookies, proxies, yt-dlp, downloads, ASR, and LLM-generated transcript out of the first implementation.
