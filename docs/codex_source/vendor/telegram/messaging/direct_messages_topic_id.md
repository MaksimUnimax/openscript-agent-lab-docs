# direct_messages_topic_id

STATUS: verified
CATEGORY: vendor/telegram/messaging

SOURCE_URLS:
- https://core.telegram.org/bots/api

SOURCE_PATHS:
- docs/codex_source/vendor/telegram/_raw/bot_api.html
- docs/codex_source/vendor/telegram/_raw/sections/send_message.md
- docs/codex_source/vendor/telegram/_raw/sections/send_voice.md

APPLIES_TO:
- telegram_voice_final_proof
- telegram_delivery_visibility_diagnosis

FACTS:
- `direct_messages_topic_id` identifies the direct messages topic to which a message will be sent.
- Telegram documents it as required when sending to a direct messages chat.

CONTRACT:
- Preserve direct-message topic routing when the outbound chat is a direct messages chat.

NON_GOALS:
- general chat topology design

FORBIDDEN_MISUSE:
- omitting `direct_messages_topic_id` when Telegram requires it for the chat type

OPEN_QUESTIONS:
- none

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- project_mapping_checked: yes
- verified_at_utc: 2026-05-16T10:46:58Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_TELEGRAM_DOCS_EXTRACTION_20260516_01
