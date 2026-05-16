# Token-bearing URL redaction

STATUS: extracted_with_gaps
CATEGORY: vendor/telegram/files

SOURCE_URLS:
- https://core.telegram.org/bots/api

SOURCE_PATHS:
- docs/codex_source/vendor/telegram/_raw/bot_api.html
- docs/codex_source/vendor/telegram/_raw/sections/get_file.md
- docs/codex_source/vendor/telegram/_raw/sections/file.md

APPLIES_TO:
- telegram_voice_final_proof
- telegram_delivery_visibility_diagnosis

FACTS:
- Telegram file download URLs include the bot token.
- Bot API method URLs may also include the bot token.

CONTRACT:
- Redact token-bearing URLs in all public docs and runtime reports.
- Never store a raw bot-token URL in repo documentation.

NON_GOALS:
- secret management

FORBIDDEN_MISUSE:
- echoing a full `https://api.telegram.org/file/bot<token>/...` URL in any report

OPEN_QUESTIONS:
- whether any runtime debug path needs a dedicated redaction helper

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- project_mapping_checked: yes
- verified_at_utc: 2026-05-16T10:46:58Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_TELEGRAM_DOCS_EXTRACTION_20260516_01
