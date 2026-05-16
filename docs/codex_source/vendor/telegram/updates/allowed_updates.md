# allowed_updates

STATUS: verified
CATEGORY: vendor/telegram/updates

SOURCE_URLS:
- https://core.telegram.org/bots/api

SOURCE_PATHS:
- docs/codex_source/vendor/telegram/_raw/bot_api.html
- docs/codex_source/vendor/telegram/_raw/sections/get_updates.md

APPLIES_TO:
- telegram_user_id_allowlist_ui
- telegram_voice_final_proof
- telegram_delivery_visibility_diagnosis

FACTS:
- `allowed_updates` limits which update types are returned by `getUpdates`.
- The same concept exists for webhook configuration.
- The parameter does not retroactively change already queued updates.

CONTRACT:
- Use `allowed_updates` as transport filtering only.
- Do not confuse update-type filtering with access control.

NON_GOALS:
- auth policy

FORBIDDEN_MISUSE:
- treating `allowed_updates` as a user allowlist

OPEN_QUESTIONS:
- none

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- project_mapping_checked: yes
- verified_at_utc: 2026-05-16T10:46:58Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_TELEGRAM_DOCS_EXTRACTION_20260516_01
