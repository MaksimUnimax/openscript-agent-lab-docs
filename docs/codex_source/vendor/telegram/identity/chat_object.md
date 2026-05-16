# Chat object

STATUS: verified
CATEGORY: vendor/telegram/identity

SOURCE_URLS:
- https://core.telegram.org/bots/api

SOURCE_PATHS:
- docs/codex_source/vendor/telegram/_raw/bot_api.html
- docs/codex_source/vendor/telegram/_raw/sections/chat.md

APPLIES_TO:
- telegram_user_id_allowlist_ui
- telegram_voice_final_proof
- telegram_delivery_visibility_diagnosis

FACTS:
- Chat represents a chat context.
- `id` is the unique identifier of the chat.
- `type` can be `private`, `group`, `supergroup`, or `channel`.
- Chat IDs identify the delivery context for outgoing messages and not the sender identity by themselves.

CONTRACT:
- Keep `chat.id` for reply delivery and context routing.
- Do not use `chat.id` as the allowlist rule for this feature.

NON_GOALS:
- no allowlist state
- no user identity inference beyond the documented chat fields

FORBIDDEN_MISUSE:
- treating `chat.id` as a universal user identifier

OPEN_QUESTIONS:
- none

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- project_mapping_checked: yes
- verified_at_utc: 2026-05-16T10:46:58Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_TELEGRAM_DOCS_EXTRACTION_20260516_01
