# message_thread_id

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
- `message_thread_id` identifies a target message thread or forum topic.
- Telegram documents it for forum supergroups and private chats with forum topic mode enabled.

CONTRACT:
- Preserve `message_thread_id` when the inbound update is topic-scoped and the outbound reply must stay in the same topic.

NON_GOALS:
- topic routing policy

FORBIDDEN_MISUSE:
- inventing a thread id when the inbound update does not provide one

OPEN_QUESTIONS:
- whether a future flow needs separate direct-message topic handling

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- project_mapping_checked: yes
- verified_at_utc: 2026-05-16T10:46:58Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_TELEGRAM_DOCS_EXTRACTION_20260516_01
