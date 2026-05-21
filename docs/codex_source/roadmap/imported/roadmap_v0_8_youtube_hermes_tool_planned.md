TITLE: Roadmap Import — Future Hermes-visible Tool “Ютуб”
STATUS: IMPORTED_PRODUCT_DIRECTION_UPDATE
SOURCE_KIND: chatgpt_inline_user_clarification
DATE: 2026-05-21
RELATION_TO_TZ_V0_3: extends v0.3, does not replace it
CURRENT_IMPLEMENTATION_STATUS: NOT_IMPLEMENTED
CURRENT_DOC_STATUS: RECORDED_FOR_FUTURE_DESIGN
USER_FACING_NAME: Ютуб
INTERNAL_TOOL_FAMILY: youtube
FIRST_TOOL_SCOPE: subtitles_with_timings_by_video_url
ARCHITECTURAL_CLASS: Hermes-visible agent tool

## 1. Why this roadmap note exists

The user clarified a future tool family called “Ютуб”.

This roadmap note records the product direction before implementation.

This is documentation only. It is not an implementation request.

## 2. Roadmap meaning

“Ютуб” is a future deterministic Hermes-visible agent tool family.

The first concrete tool in this family retrieves available YouTube subtitles or transcript segments with timings by a YouTube video URL.

The architecture must remain:

Agent Lab -> selected agent -> Hermes runtime/profile -> tool call -> deterministic executor -> structured factual result -> agent answer.

Not accepted:

- standalone script as product;
- app-local shortcut that bypasses Hermes/tool invocation;
- UI-only parser that bypasses the selected agent;
- direct free-form LLM transcript generation;
- hardcoded current agent;
- hardcoded current user;
- hardcoded current provider;
- global uncontrolled availability to all agents.

## 3. Roadmap status

Status now:
- PLANNED / NEEDS_DESIGN / NEEDS_PROOF.

The product direction is recorded for future design and proof work.

Do not implement now.

## 4. Proof and design gate

Implementation is blocked until vendor/API/legal proof and Hermes tool design are completed.

This roadmap note records a planned future Hermes-visible tool only.

The next allowed step is proof and design work, not application code.
