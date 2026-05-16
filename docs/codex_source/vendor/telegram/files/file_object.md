# File object

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
- File contains `file_id`, `file_unique_id`, `file_size`, and optional `file_path`.
- `file_id` can be reused to download or reuse the file.
- `file_unique_id` is stable across time and bots but cannot be used to download.
- `file_path` is used with the download URL.

CONTRACT:
- Use `file_id` for Telegram file retrieval.
- Use `file_path` only as part of the download flow.

NON_GOALS:
- storage abstraction

FORBIDDEN_MISUSE:
- treating `file_unique_id` as a downloadable identifier

OPEN_QUESTIONS:
- none

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- project_mapping_checked: yes
- verified_at_utc: 2026-05-16T10:46:58Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_TELEGRAM_DOCS_EXTRACTION_20260516_01
