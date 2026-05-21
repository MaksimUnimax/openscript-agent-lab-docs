TITLE: Technical Spec Extension v0.5 — Hermes-visible Tool “Ютуб”: YouTube subtitles with timings
STATUS: PROPOSED_PRODUCT_SPECIFICATION
SOURCE_KIND: chatgpt_inline_user_clarification
DATE: 2026-05-21
RELATION_TO_TZ_V0_3: extends v0.3, does not replace it
CURRENT_IMPLEMENTATION_STATUS: NOT_IMPLEMENTED
CURRENT_DOC_STATUS: SPECIFIED_FOR_FUTURE_DESIGN
USER_FACING_NAME: Ютуб
INTERNAL_TOOL_FAMILY: youtube
FIRST_TOOL_SCOPE: subtitles_with_timings_by_video_url
ARCHITECTURAL_CLASS: Hermes-visible agent tool

# Technical Spec Extension v0.5 — Tool “Ютуб”

## 1. Why this update exists

The user clarified a future tool family called “Ютуб”.

This update records the product and architecture contract before implementation.

This is documentation only. It is not an implementation request.

## 2. Core product meaning

“Ютуб” is a future deterministic Hermes-visible agent tool family.

The first concrete tool in this family retrieves available YouTube subtitles or transcript segments with timings by a YouTube video URL.

The tool must return factual subtitle data with timestamps. The agent may then explain, format, summarize, search, or analyze the returned subtitle data, but the agent must not invent subtitles or timings.

## 3. Mandatory architecture

“Ютуб” must work through the canonical Agent Lab / Hermes tool path:

1. The operator or user gives a YouTube video URL.
2. The selected agent receives the user request.
3. The selected agent may call the “Ютуб” tool only if this tool is explicitly enabled for that agent.
4. Hermes/runtime invokes the registered tool.
5. The deterministic tool executor validates the URL and retrieves available subtitles.
6. The tool returns a structured factual result to the agent.
7. The agent answers the user using only the returned tool result.

Accepted path:

Agent Lab -> selected agent -> Hermes runtime/profile -> tool call -> deterministic executor -> structured result -> agent answer.

Not accepted:

- standalone script as product;
- app-local shortcut that bypasses Hermes/tool invocation;
- UI-only parser that bypasses the selected agent;
- direct free-form LLM transcript generation;
- hardcoded current agent;
- hardcoded current user;
- hardcoded current provider;
- global uncontrolled availability to all agents.

## 4. Actors

The tool can be used by:

### 4.1 Operator / user

The operator or user manually provides a YouTube video URL and receives subtitles with timings.

### 4.2 Allowed agent

An agent may use the tool only if the tool is explicitly enabled for that agent.

The agent may:

- call the tool when the user asks for YouTube subtitles/transcript;
- ask the user for a valid YouTube video URL if missing;
- summarize or analyze the returned subtitles;
- quote transcript fragments with timestamps;
- search inside the returned subtitle data.

The agent must not:

- fabricate transcript text;
- fabricate timestamps;
- claim extraction succeeded if the tool returned an error;
- bypass the tool with a guessed answer;
- use the tool if not enabled for that agent.

## 5. Input contract

Required input:

- `youtube_url`: string
  - must be a valid YouTube video URL;
  - must resolve to one video;
  - must not be a channel URL, playlist URL, search page, Shorts feed page, or arbitrary website.

Optional future input:

- `language`: string or null
  - examples: `ru`, `en`, `auto`;
  - exact selection behavior requires later vendor/API proof.

- `format`: string or null
  - examples: `json`, `markdown`, `plain_text`;
  - internal result must remain structured even if user-facing output is formatted.

## 6. Output contract

The tool response must be structured.

Required top-level fields:

- `ok`: boolean
- `video_url`: string
- `video_id`: string or null
- `title`: string or null
- `language`: string or null
- `source_type`: string
- `subtitles_available`: boolean
- `segments`: array
- `full_text_with_timestamps`: string or null
- `error`: object or null
- `audit`: object

Conceptual `source_type` values:

- `manual_captions`
- `auto_captions`
- `unavailable`
- `unknown`

Each segment should contain:

- `start_time`: string
- `start_seconds`: number
- `end_time`: string or null
- `end_seconds`: number or null
- `duration_seconds`: number or null
- `text`: string

The tool must preserve segment ordering.

## 7. User-facing answer

If subtitles are available, the user-facing answer should include:

- video title if safely available;
- subtitle language;
- whether captions are manual or auto-generated if known;
- subtitle lines with timestamps.

Example user-facing format:

```text
Видео: <title>
Язык субтитров: <language>
Источник: auto_captions

[00:00:01] ...
[00:00:04] ...
[00:00:08] ...
```

## 8. Implementation gate

This tool is documented only as a planned Hermes-visible agent tool.

Implementation is blocked until vendor/API/legal proof and Hermes tool design are completed.

The next allowed step is documentation proof and design work, not application code.
