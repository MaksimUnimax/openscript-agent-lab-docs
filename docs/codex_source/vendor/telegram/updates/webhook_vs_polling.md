# Webhook vs polling

STATUS: verified
CATEGORY: vendor/telegram/updates

SOURCE_URLS:
- https://core.telegram.org/bots/api

SOURCE_PATHS:
- docs/codex_source/vendor/telegram/_raw/bot_api.html
- docs/codex_source/vendor/telegram/_raw/sections/get_updates.md

APPLIES_TO:
- telegram_user_id_allowlist_ui
- telegram_voice_final_proof
- telegram_delivery_visibility_diagnosis

FACTS:
- Telegram provides two mutually exclusive update delivery modes: `getUpdates` and webhooks.
- While a webhook is configured, `getUpdates` does not work.
- Webhook delivery uses HTTPS POST requests with serialized `Update` payloads.

CONTRACT:
- Treat update transport choice as infrastructure, not as access policy.
- Keep the user allowlist independent from polling or webhook mode.

NON_GOALS:
- deployment configuration

FORBIDDEN_MISUSE:
- assuming webhook mode changes user identity semantics

OPEN_QUESTIONS:
- none

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- project_mapping_checked: yes
- verified_at_utc: 2026-05-16T10:46:58Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_TELEGRAM_DOCS_EXTRACTION_20260516_01
