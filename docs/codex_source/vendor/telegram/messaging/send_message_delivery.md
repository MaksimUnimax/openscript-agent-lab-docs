# sendMessage delivery

STATUS: verified
CATEGORY: vendor/telegram/messaging

SOURCE_URLS:
- https://core.telegram.org/bots/api

SOURCE_PATHS:
- docs/codex_source/vendor/telegram/_raw/bot_api.html
- docs/codex_source/vendor/telegram/_raw/sections/send_message.md

APPLIES_TO:
- telegram_voice_final_proof
- telegram_delivery_visibility_diagnosis

FACTS:
- `sendMessage` sends text messages.
- `chat_id` is the target chat or bot/channel username.
- A successful response returns a `Message`.
- `message_id` is available in the returned message and can be used as delivery proof.
- `message_thread_id` and `direct_messages_topic_id` exist for topic and direct-message chat routing when relevant.

CONTRACT:
- Use `chat_id` for delivery only.
- Record success proof via returned `message_id`, with sensitive values redacted as needed.

NON_GOALS:
- allowlist policy

FORBIDDEN_MISUSE:
- using `chat_id` as an access-control rule

OPEN_QUESTIONS:
- none

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- project_mapping_checked: yes
- verified_at_utc: 2026-05-16T10:46:58Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_TELEGRAM_DOCS_EXTRACTION_20260516_01
