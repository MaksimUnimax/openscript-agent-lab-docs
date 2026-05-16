# Callback query identity

STATUS: verified
CATEGORY: vendor/telegram/identity

SOURCE_URLS:
- https://core.telegram.org/bots/api

SOURCE_PATHS:
- docs/codex_source/vendor/telegram/_raw/bot_api.html
- docs/codex_source/vendor/telegram/_raw/sections/update.md

APPLIES_TO:
- telegram_user_id_allowlist_ui
- telegram_voice_final_proof
- telegram_delivery_visibility_diagnosis

FACTS:
- `callback_query` is an incoming callback query from an inline keyboard button.
- `callback_query.from` is the user who triggered the callback.
- `callback_query.message` may be present when the callback originated from a bot message.
- `callback_query.chat_instance` is a global identifier for the chat context, not the sender identity.

CONTRACT:
- Use `callback_query.from.id` for allowlist checks when callback updates are supported.
- Keep `callback_query.message.chat.id` for reply context only.

NON_GOALS:
- no callback UI design

FORBIDDEN_MISUSE:
- treating `chat_instance` as a user allowlist key

OPEN_QUESTIONS:
- none

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- project_mapping_checked: yes
- verified_at_utc: 2026-05-16T10:46:58Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_TELEGRAM_DOCS_EXTRACTION_20260516_01
