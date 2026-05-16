# Privacy mode limits

STATUS: verified
CATEGORY: vendor/telegram/privacy

SOURCE_URLS:
- https://core.telegram.org/bots/features
- https://core.telegram.org/bots/faq

SOURCE_PATHS:
- docs/codex_source/vendor/telegram/_raw/bots_features.html
- docs/codex_source/vendor/telegram/_raw/bots_faq.html
- docs/codex_source/vendor/telegram/_raw/sections/privacy_mode.md

APPLIES_TO:
- telegram_user_id_allowlist_ui
- telegram_voice_final_proof
- telegram_delivery_visibility_diagnosis

FACTS:
- In groups, privacy mode limits which messages a bot receives.
- All bots still receive all messages from private chats with users.
- Privacy mode is a bot-platform visibility filter, not an application access-control layer.

CONTRACT:
- Do not rely on privacy mode to block unauthorized private-message access.
- Use application-level allowlist logic for this project.

NON_GOALS:
- BotFather configuration management

FORBIDDEN_MISUSE:
- treating privacy mode as a substitute for user authorization

OPEN_QUESTIONS:
- none

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- project_mapping_checked: yes
- verified_at_utc: 2026-05-16T10:46:58Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_TELEGRAM_DOCS_EXTRACTION_20260516_01
