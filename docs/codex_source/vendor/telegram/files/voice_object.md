# Voice object

STATUS: verified
CATEGORY: vendor/telegram/files

SOURCE_URLS:
- https://core.telegram.org/bots/api

SOURCE_PATHS:
- docs/codex_source/vendor/telegram/_raw/bot_api.html
- docs/codex_source/vendor/telegram/_raw/sections/voice.md

APPLIES_TO:
- telegram_voice_final_proof
- telegram_delivery_visibility_diagnosis

FACTS:
- Voice represents a voice note.
- Relevant fields include `file_id`, `file_unique_id`, `duration`, `mime_type`, and `file_size`.

CONTRACT:
- Treat `file_id` as an operational identifier, not as public proof.
- Redact file identifiers in public reports when necessary.

NON_GOALS:
- voice transcription logic

FORBIDDEN_MISUSE:
- exposing raw `file_id` values in public proof reports

OPEN_QUESTIONS:
- none

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- project_mapping_checked: yes
- verified_at_utc: 2026-05-16T10:46:58Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_TELEGRAM_DOCS_EXTRACTION_20260516_01
