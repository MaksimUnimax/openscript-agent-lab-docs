# User object

STATUS: verified
CATEGORY: vendor/telegram/identity

SOURCE_URLS:
- https://core.telegram.org/bots/api

SOURCE_PATHS:
- docs/codex_source/vendor/telegram/_raw/bot_api.html
- docs/codex_source/vendor/telegram/_raw/sections/user.md

APPLIES_TO:
- telegram_user_id_allowlist_ui
- telegram_voice_final_proof
- telegram_delivery_visibility_diagnosis

FACTS:
- User represents a Telegram user or bot.
- `id` is the unique identifier for that user or bot.
- `id` is large enough that 64-bit storage is safe.

CONTRACT:
- Use `User.id` as the identity primitive when implementing a user-based allowlist.
- Mask or redact the value in public reports if needed, but do not change its semantic meaning.

NON_GOALS:
- no chat delivery logic
- no provider auth logic

FORBIDDEN_MISUSE:
- using `chat.id` as a substitute for `User.id`

OPEN_QUESTIONS:
- none

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- project_mapping_checked: yes
- verified_at_utc: 2026-05-16T10:46:58Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_TELEGRAM_DOCS_EXTRACTION_20260516_01
