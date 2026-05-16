# Update offset and deduplication

STATUS: verified
CATEGORY: vendor/telegram/updates

SOURCE_URLS:
- https://core.telegram.org/bots/api

SOURCE_PATHS:
- docs/codex_source/vendor/telegram/_raw/bot_api.html
- docs/codex_source/vendor/telegram/_raw/sections/get_updates.md
- docs/codex_source/vendor/telegram/_raw/sections/update.md

APPLIES_TO:
- telegram_user_id_allowlist_ui
- telegram_voice_final_proof
- telegram_delivery_visibility_diagnosis

FACTS:
- `update_id` increases sequentially.
- An update is confirmed when `getUpdates` is called with a higher `offset`.
- Negative offsets can be used to read from the end of the queue.

CONTRACT:
- Use offset handling to avoid duplicate processing.
- Do not use offset handling as a substitute for user allowlist checks.

NON_GOALS:
- queue storage design

FORBIDDEN_MISUSE:
- using `update_id` order as a proxy for user authorization

OPEN_QUESTIONS:
- none

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- project_mapping_checked: yes
- verified_at_utc: 2026-05-16T10:46:58Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_TELEGRAM_DOCS_EXTRACTION_20260516_01
