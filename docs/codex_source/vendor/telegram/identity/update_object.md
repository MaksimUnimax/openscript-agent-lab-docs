# Update object

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
- Update is the incoming update envelope from Telegram.
- `update_id` is unique, starts from a positive number, and increases sequentially.
- `message`, `edited_message`, `channel_post`, `edited_channel_post`, `callback_query`, and other typed fields are optional.
- `message` carries a new incoming message.
- `edited_message` carries a new version of a message known to the bot.
- `callback_query` carries an incoming callback query.

CONTRACT:
- Inspect the actual update field before deciding identity or resource usage.
- Treat Update as a typed envelope, not as a single flat payload.
- Do not assume the same identity field exists for every update type.

NON_GOALS:
- no project routing logic
- no token handling

FORBIDDEN_MISUSE:
- deriving allowlist identity from `chat.id` without checking the update type first

OPEN_QUESTIONS:
- none

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- project_mapping_checked: yes
- verified_at_utc: 2026-05-16T10:46:58Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_TELEGRAM_DOCS_EXTRACTION_20260516_01
