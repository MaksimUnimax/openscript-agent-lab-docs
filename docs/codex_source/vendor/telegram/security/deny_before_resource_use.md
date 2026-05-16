# Deny before resource use

STATUS: extracted_with_gaps
CATEGORY: vendor/telegram/security

SOURCE_URLS:
- https://core.telegram.org/bots/api
- https://core.telegram.org/bots/features
- https://core.telegram.org/bots/faq

SOURCE_PATHS:
- docs/codex_source/vendor/telegram/_raw/bot_api.html
- docs/codex_source/vendor/telegram/_raw/bots_features.html
- docs/codex_source/vendor/telegram/_raw/bots_faq.html

APPLIES_TO:
- telegram_user_id_allowlist_ui
- telegram_voice_final_proof
- telegram_delivery_visibility_diagnosis

FACTS:
- Telegram update handling can lead into routing, file download, delivery, and callback responses.
- The platform docs show that private chats are visible to bots, so app-level denial must happen inside the application.

CONTRACT:
- Deny unknown users at the earliest shared Telegram update-processing point.
- Ensure denial happens before command routing, active-agent switching, getFile/download, STT, transcript handoff, provider calls, and generated replies.
- Silent deny is acceptable if the product chooses it.

NON_GOALS:
- audit retention policy

FORBIDDEN_MISUSE:
- delaying access checks until after an expensive resource call

OPEN_QUESTIONS:
- exact shared hook placement may differ by runtime pipeline

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- project_mapping_checked: yes
- verified_at_utc: 2026-05-16T10:46:58Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_TELEGRAM_DOCS_EXTRACTION_20260516_01
