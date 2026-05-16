# Project mapping

STATUS: extracted_with_gaps
CATEGORY: vendor/telegram/source_map

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
- Identity docs map to access-control tasks.
- Voice/file docs map to voice pipeline tasks.
- sendMessage docs map to outbound delivery proof tasks.
- Privacy docs explain why privacy mode is not enough for application authorization.

CONTRACT:
- Future Codex prompts should read the exact Telegram docs for the task instead of using roadmap/continuity/TZ as substitutes.

NON_GOALS:
- project architecture ownership

FORBIDDEN_MISUSE:
- treating this map as a replacement for the underlying Telegram docs

OPEN_QUESTIONS:
- which future project docs will become the authoritative implementation map

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- project_mapping_checked: yes
- verified_at_utc: 2026-05-16T10:46:58Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_TELEGRAM_DOCS_EXTRACTION_20260516_01
