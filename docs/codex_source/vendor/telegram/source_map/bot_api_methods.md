# Bot API methods map

STATUS: extracted
CATEGORY: vendor/telegram/source_map

SOURCE_URLS:
- https://core.telegram.org/bots/api

SOURCE_PATHS:
- docs/codex_source/vendor/telegram/_raw/bot_api.html

APPLIES_TO:
- telegram_user_id_allowlist_ui
- telegram_voice_final_proof
- telegram_delivery_visibility_diagnosis

FACTS:
- `getUpdates` is documented in `docs/codex_source/vendor/telegram/_raw/bot_api.html` around lines 361-395.
- `getFile` is documented in `docs/codex_source/vendor/telegram/_raw/bot_api.html` around lines 11586-11596.
- `sendMessage` is documented in `docs/codex_source/vendor/telegram/_raw/bot_api.html` around lines 8927-8978.
- `sendVoice` is documented in `docs/codex_source/vendor/telegram/_raw/bot_api.html` around lines 10242-10310.

CONTRACT:
- Future prompts should read the exact method docs before implementing Telegram-bound flows.

NON_GOALS:
- API client implementation

FORBIDDEN_MISUSE:
- inventing a method contract from memory when an exact source path exists

OPEN_QUESTIONS:
- none

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- project_mapping_checked: yes
- verified_at_utc: 2026-05-16T10:46:58Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_TELEGRAM_DOCS_EXTRACTION_20260516_01
