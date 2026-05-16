# chat.id vs user.id

STATUS: extracted_with_gaps
CATEGORY: vendor/telegram/identity

SOURCE_URLS:
- https://core.telegram.org/bots/api

SOURCE_PATHS:
- docs/codex_source/vendor/telegram/_raw/bot_api.html
- docs/codex_source/vendor/telegram/_raw/sections/chat.md
- docs/codex_source/vendor/telegram/_raw/sections/user.md

APPLIES_TO:
- telegram_user_id_allowlist_ui
- telegram_voice_final_proof
- telegram_delivery_visibility_diagnosis

FACTS:
- `User.id` identifies the Telegram user or bot.
- `Chat.id` identifies the chat context.
- `Chat.type` determines whether the context is private, group, supergroup, or channel.

CONTRACT:
- For this project’s user-only access control, use `from.id` / `User.id`.
- Use `chat.id` only as a delivery target or context identifier.
- In private chats `chat.id` may appear close to a user identity, but that must not be relied on as an allowlist rule.

NON_GOALS:
- no transport routing changes
- no bot token handling

FORBIDDEN_MISUSE:
- assuming `chat.id` is a stable substitute for `User.id`

OPEN_QUESTIONS:
- whether future business or channel flows need a separate access model

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- project_mapping_checked: yes
- verified_at_utc: 2026-05-16T10:46:58Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_TELEGRAM_DOCS_EXTRACTION_20260516_01
