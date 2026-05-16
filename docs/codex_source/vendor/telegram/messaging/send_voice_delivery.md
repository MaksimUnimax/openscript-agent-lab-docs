# sendVoice delivery

STATUS: verified
CATEGORY: vendor/telegram/messaging

SOURCE_URLS:
- https://core.telegram.org/bots/api

SOURCE_PATHS:
- docs/codex_source/vendor/telegram/_raw/bot_api.html
- docs/codex_source/vendor/telegram/_raw/sections/send_voice.md

APPLIES_TO:
- telegram_voice_final_proof
- telegram_delivery_visibility_diagnosis

FACTS:
- `sendVoice` sends audio as a voice message.
- A successful response returns a `Message`.
- `chat_id` is the target chat or bot/channel username.
- Telegram documents voice-message format limits and a 50 MB size limit.

CONTRACT:
- Use `sendVoice` only as delivery output, not as proof of voice input processing.
- Record success through the returned `Message` and its `message_id`.

NON_GOALS:
- voice recognition

FORBIDDEN_MISUSE:
- mixing `sendVoice` delivery proof with input-STT proof

OPEN_QUESTIONS:
- none

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- project_mapping_checked: yes
- verified_at_utc: 2026-05-16T10:46:58Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_TELEGRAM_DOCS_EXTRACTION_20260516_01
