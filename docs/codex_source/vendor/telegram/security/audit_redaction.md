# Audit redaction

STATUS: extracted_with_gaps
CATEGORY: vendor/telegram/security

SOURCE_URLS:
- https://core.telegram.org/bots/api

SOURCE_PATHS:
- docs/codex_source/vendor/telegram/_raw/bot_api.html
- docs/codex_source/vendor/telegram/_raw/sections/get_file.md

APPLIES_TO:
- telegram_user_id_allowlist_ui
- telegram_voice_final_proof
- telegram_delivery_visibility_diagnosis

FACTS:
- Telegram file download URLs include the bot token.
- Voice file identifiers, message ids, and user ids may be operationally useful but should be handled carefully in public reports.

CONTRACT:
- Mask user IDs and chat IDs where public reporting needs it.
- Do not print bot tokens, raw token-bearing URLs, or full transcripts.
- Do not print a full generated answer if the report only needs proof metadata.

NON_GOALS:
- secret vault implementation

FORBIDDEN_MISUSE:
- storing raw token URLs or secrets in docs or reports

OPEN_QUESTIONS:
- whether some internal-only logs need a different redaction policy

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- project_mapping_checked: yes
- verified_at_utc: 2026-05-16T10:46:58Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_TELEGRAM_DOCS_EXTRACTION_20260516_01
