# YouTube Transcript API Design Baseline for “Ютуб”

STATUS: PLANNED_DESIGN_BASELINE
SOURCE_KIND: docs_import_from_upstream_vendor_readme
DATE: 2026-05-21

## 1. Purpose

This note records the concrete implementation mechanism for the planned Hermes-visible tool “Ютуб”.

The mechanism is not a tool implementation. It is the design baseline for future deterministic executor work.

## 2. Imported upstream vendor baseline

The imported upstream package is `youtube-transcript-api`.

Its documented purpose is public transcript/subtitle retrieval for a given YouTube video, including automatically generated subtitles.

The upstream package also documents:

- retrieval by `video_id`, not by YouTube Data API request flow;
- transcript selection by language priority;
- listing available transcripts for a video;
- selecting manually created versus automatically generated transcripts;
- fetching transcript data as structured snippet objects with timing metadata;
- no headless browser requirement.

The upstream package metadata imported into repo docs states:

- package name: `youtube-transcript-api`
- version: `1.2.4`
- license: MIT
- Python support: 3.8 through 3.14

## 3. Concrete mechanism for “Ютуб”

The planned Hermes-visible tool should work like this:

1. Deterministic executor receives a YouTube video URL from the selected agent.
2. Deterministic executor validates the URL and extracts a single `video_id`.
3. Deterministic executor creates `YouTubeTranscriptApi`.
4. Deterministic executor uses `list(video_id)` when it needs to inspect available transcript languages/types.
5. Deterministic executor chooses the transcript deterministically by the default language priority `ru -> en`, then any operator hints, then any remaining available transcript, while still preferring manual transcripts over generated transcripts when both are available.
6. Deterministic executor fetches the transcript data with `fetch()` on the selected transcript.
7. Deterministic executor converts the returned transcript snippets into structured factual result data with timings.
8. Selected agent answers the user only from the structured tool result.

Recommended transcript selection policy:

- prefer a direct public transcript/subtitle for the default priority `ru -> en`;
- treat operator-provided languages as hints, not strict filters;
- when multiple transcripts are available, select deterministically by the effective priority order and transcript type;
- if both manual and generated transcripts are available, prefer manual unless the prompt or caller says otherwise;
- if no transcript is available, return an unavailable/error result instead of guessing or translating;
- if the default priority has no match, fall back to any available transcript.

## 4. Explicit exclusions for the first version

The first implementation version must not use:

- YouTube Data API;
- OAuth;
- cookies;
- proxies;
- yt-dlp;
- video download;
- audio download;
- ASR;
- LLM-generated transcript;
- app-local shortcut that bypasses Hermes;
- global enablement for all agents.

## 5. Relation to “Ютуб” docs

This design note is the concrete mechanism behind:

- `docs/codex_source/project/technical_spec_extensions/youtube_subtitles_tool_v0_5.md`
- `docs/codex_source/roadmap/imported/roadmap_v0_8_youtube_hermes_tool_planned.md`

Those documents define the product and roadmap contract.
This note defines the imported vendor mechanism that future implementation work should follow.
