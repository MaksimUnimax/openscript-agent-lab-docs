# Sender user id

STATUS: extracted_with_gaps
CATEGORY: vendor/telegram/identity

SOURCE_URLS:
- https://core.telegram.org/bots/api

SOURCE_PATHS:
- docs/codex_source/vendor/telegram/_raw/bot_api.html
- docs/codex_source/vendor/telegram/_raw/sections/update.md
- docs/codex_source/vendor/telegram/_raw/sections/message.md
- docs/codex_source/vendor/telegram/_raw/sections/chat.md
- docs/codex_source/vendor/telegram/_raw/sections/update.md

APPLIES_TO:
- telegram_user_id_allowlist_ui
- telegram_voice_final_proof
- telegram_delivery_visibility_diagnosis

FACTS:
- `message.from` is the sender of a message when present.
- `message.from` may be empty for messages sent to channels.
- `edited_message` is a message update and should be handled through the same update discriminator before identity extraction.
- `callback_query.from` identifies the user who triggered the callback.

CONTRACT:
- Use `from.id` / Telegram `user_id` as the allowlist identity when the update type supports it.
- Fail closed if the protected path depends on sender identity but `from.id` is absent.
- Check the update type first, then extract the correct identity field for that type.

NON_GOALS:
- no channel-post sender emulation
- no chat-based allowlist rule

FORBIDDEN_MISUSE:
- falling back to `chat.id` when `from.id` is available but the user is unknown

OPEN_QUESTIONS:
- whether a future non-message update type needs a separate identity rule

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- project_mapping_checked: yes
- verified_at_utc: 2026-05-16T10:46:58Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_TELEGRAM_DOCS_EXTRACTION_20260516_01
