# BotFather privacy settings

STATUS: extracted_with_gaps
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
- Telegram references privacy mode as a bot setting handled through BotFather-controlled bot configuration.
- The official docs captured here describe the effect of privacy mode more directly than the exact BotFather UI flow.

CONTRACT:
- Use this file only as a reminder that privacy mode is a platform setting, not app authorization.

NON_GOALS:
- exact BotFather UI instructions

FORBIDDEN_MISUSE:
- assuming BotFather privacy settings are sufficient to gate private-user access

OPEN_QUESTIONS:
- exact BotFather UI wording may change over time

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- project_mapping_checked: yes
- verified_at_utc: 2026-05-16T10:46:58Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_TELEGRAM_DOCS_EXTRACTION_20260516_01
