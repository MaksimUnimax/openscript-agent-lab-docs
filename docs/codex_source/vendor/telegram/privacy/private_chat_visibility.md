# Private chat visibility

STATUS: verified
CATEGORY: vendor/telegram/privacy

SOURCE_URLS:
- https://core.telegram.org/bots/features
- https://core.telegram.org/bots/faq

SOURCE_PATHS:
- docs/codex_source/vendor/telegram/_raw/bots_features.html
- docs/codex_source/vendor/telegram/_raw/bots_faq.html

APPLIES_TO:
- telegram_user_id_allowlist_ui
- telegram_delivery_visibility_diagnosis

FACTS:
- Telegram says bots receive all messages from private chats with users.
- Privacy mode does not remove private-chat visibility.

CONTRACT:
- If the bot is intended for private use only, the application must deny unknown users itself.

NON_GOALS:
- group moderation policy

FORBIDDEN_MISUSE:
- assuming private-chat visibility implies authorization

OPEN_QUESTIONS:
- none

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- project_mapping_checked: yes
- verified_at_utc: 2026-05-16T10:46:58Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_TELEGRAM_DOCS_EXTRACTION_20260516_01
