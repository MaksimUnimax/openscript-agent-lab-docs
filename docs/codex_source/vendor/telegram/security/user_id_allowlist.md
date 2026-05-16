# User ID allowlist

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
- docs/codex_source/vendor/telegram/_raw/sections/update.md
- docs/codex_source/vendor/telegram/_raw/sections/message.md
- docs/codex_source/vendor/telegram/_raw/sections/chat.md

APPLIES_TO:
- telegram_user_id_allowlist_ui
- telegram_voice_final_proof
- telegram_delivery_visibility_diagnosis

FACTS:
- Access identity for this feature is `from.id` / Telegram `user_id`.
- `chat.id` is a delivery/context identifier and must not be used as the allowlist rule.
- Unknown users can appear in private chats, and privacy mode does not block those chats.

CONTRACT:
- Maintain an allowed-user-id list in project state.
- Deny unknown users before route switch, active-agent switch, getFile/download, STT, transcript handoff, provider calls, and generated reply sending.
- Apply the same rule to text, commands, voice, and callback updates when those update types are supported.

NON_GOALS:
- role management
- chat-based ACLs

FORBIDDEN_MISUSE:
- hardcoding an agent slug into the access rule
- using `chat.id` as the access key

OPEN_QUESTIONS:
- whether future platform-specific update types need separate identity handling

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- project_mapping_checked: yes
- verified_at_utc: 2026-05-16T10:46:58Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_TELEGRAM_DOCS_EXTRACTION_20260516_01
