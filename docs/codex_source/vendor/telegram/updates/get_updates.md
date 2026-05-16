# getUpdates

STATUS: verified
CATEGORY: vendor/telegram/updates

SOURCE_URLS:
- https://core.telegram.org/bots/api
- https://core.telegram.org/bots/faq

SOURCE_PATHS:
- docs/codex_source/vendor/telegram/_raw/bot_api.html
- docs/codex_source/vendor/telegram/_raw/bots_faq.html
- docs/codex_source/vendor/telegram/_raw/sections/get_updates.md
- docs/codex_source/vendor/telegram/_raw/sections/update.md

APPLIES_TO:
- telegram_user_id_allowlist_ui
- telegram_voice_final_proof
- telegram_delivery_visibility_diagnosis

FACTS:
- `getUpdates` is the long-polling method for incoming updates.
- `offset` confirms updates once it is higher than the update id.
- Updates are queued on the server until received.
- `allowed_updates` can limit which update types are returned.
- `getUpdates` and webhooks are mutually exclusive.

CONTRACT:
- Use update polling semantics for deduplication, but do not confuse deduplication with access control.
- Do not make a real `getUpdates` call during docs extraction.

NON_GOALS:
- webhook deployment
- update transport implementation

FORBIDDEN_MISUSE:
- using `offset` as an access-control rule

OPEN_QUESTIONS:
- none

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- project_mapping_checked: yes
- verified_at_utc: 2026-05-16T10:46:58Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_TELEGRAM_DOCS_EXTRACTION_20260516_01
