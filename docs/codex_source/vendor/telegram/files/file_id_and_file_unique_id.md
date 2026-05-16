# file_id and file_unique_id

STATUS: verified
CATEGORY: vendor/telegram/files

SOURCE_URLS:
- https://core.telegram.org/bots/api

SOURCE_PATHS:
- docs/codex_source/vendor/telegram/_raw/bot_api.html
- docs/codex_source/vendor/telegram/_raw/sections/file.md

APPLIES_TO:
- telegram_voice_final_proof
- telegram_delivery_visibility_diagnosis

FACTS:
- `file_id` is the reusable Telegram-side identifier for downloading or reusing a file.
- `file_unique_id` is stable but cannot be used to download or reuse the file.

CONTRACT:
- Use `file_id` for operational retrieval.
- Use `file_unique_id` only for stable deduplication or reference.

NON_GOALS:
- storage schema design

FORBIDDEN_MISUSE:
- using `file_unique_id` as a download handle

OPEN_QUESTIONS:
- none

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- project_mapping_checked: yes
- verified_at_utc: 2026-05-16T10:46:58Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_TELEGRAM_DOCS_EXTRACTION_20260516_01
