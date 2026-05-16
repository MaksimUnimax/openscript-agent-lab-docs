# Group visibility

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
- With privacy mode enabled, bots receive commands explicitly meant for them, some general commands, messages via the bot, and replies meant for the bot.
- With privacy mode disabled, bots or bot admins receive more messages in groups.

CONTRACT:
- Group visibility behavior is not equivalent to user authorization.
- Keep user allowlist separate from group privacy mode.

NON_GOALS:
- group admin management

FORBIDDEN_MISUSE:
- using group visibility rules as a substitute for allowlisting private users

OPEN_QUESTIONS:
- none

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- project_mapping_checked: yes
- verified_at_utc: 2026-05-16T10:46:58Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_TELEGRAM_DOCS_EXTRACTION_20260516_01
