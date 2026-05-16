# Bot API objects map

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
- `Update` is documented in `docs/codex_source/vendor/telegram/_raw/bot_api.html` around lines 228-260.
- `User` is documented in `docs/codex_source/vendor/telegram/_raw/bot_api.html` around lines 550-586.
- `Chat` is documented in `docs/codex_source/vendor/telegram/_raw/bot_api.html` around lines 648-676.
- `Message` is documented in `docs/codex_source/vendor/telegram/_raw/bot_api.html` around lines 969-1040.
- `Voice` is documented in `docs/codex_source/vendor/telegram/_raw/bot_api.html` around lines 2463-2478.
- `File` is documented in `docs/codex_source/vendor/telegram/_raw/bot_api.html` around lines 4536-4554.
- `CallbackQuery` is documented in `docs/codex_source/vendor/telegram/_raw/bot_api.html` around lines 5074-5096.

CONTRACT:
- Future prompts should cite the exact object docs instead of re-deriving object shape from memory.

NON_GOALS:
- exhaustive schema replication

FORBIDDEN_MISUSE:
- using the source-map doc as a substitute for the raw Bot API manual

OPEN_QUESTIONS:
- none

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- project_mapping_checked: yes
- verified_at_utc: 2026-05-16T10:46:58Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_TELEGRAM_DOCS_EXTRACTION_20260516_01
