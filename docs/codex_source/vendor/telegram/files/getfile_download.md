# getFile download flow

STATUS: verified
CATEGORY: vendor/telegram/files

SOURCE_URLS:
- https://core.telegram.org/bots/api
- https://core.telegram.org/bots/faq

SOURCE_PATHS:
- docs/codex_source/vendor/telegram/_raw/bot_api.html
- docs/codex_source/vendor/telegram/_raw/bots_faq.html
- docs/codex_source/vendor/telegram/_raw/sections/get_file.md

APPLIES_TO:
- telegram_voice_final_proof
- telegram_delivery_visibility_diagnosis

FACTS:
- `getFile` returns a `File` object with download metadata.
- Telegram documents a download URL shape that includes the bot token.
- Telegram documents a 20 MB file limit for bots using `getFile`.
- The download link is documented as valid for at least 1 hour.

CONTRACT:
- Never print or persist the raw token-bearing download URL in reports.
- Deny unknown users before reaching the `getFile` or download step.

NON_GOALS:
- actual file download execution

FORBIDDEN_MISUSE:
- storing token-bearing URLs in logs, docs, or reports

OPEN_QUESTIONS:
- none

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- project_mapping_checked: yes
- verified_at_utc: 2026-05-16T10:46:58Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_TELEGRAM_DOCS_EXTRACTION_20260516_01
