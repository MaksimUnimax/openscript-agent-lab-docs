# Access control

STATUS: IMPORTED_PROJECT_CONTRACT

Purpose:
- define the universal access-control contract for the project.
- capture the immediate Telegram user_id allowlist use case for “Фин инструмент”.

Identity:
- allowlist identity is Telegram `from.id` / `user_id`.
- not `chat.id`.
- not chat.id.
- `chat.id` is not the identity key.
- `chat.id` is a delivery/context identifier.

Configuration and UI:
- allowlist controls live in “Фин инструмент”.
- the configuration must support one or more allowed `user_id` values.
- the configuration must not expose secret values.

Enforcement:
- deny-before-resource-use is mandatory.
- the deny gate applies before voice download, STT, provider/model calls, tool execution, agent runtime handoff and other expensive paths.
- the same rule applies to text, voice, photo/receipt and future expensive Telegram paths.

Audit and safety:
- denied events should be minimal and safe.
- logs must not print bot tokens, auth files or secrets.
- redacted user IDs are acceptable if the reporting policy allows them.

Universality:
- this contract must not be hardcoded to one agent.
- this contract must not be hardcoded to one user in code.
- allowed IDs are data/config/UI state, not code constants.

Next docs:
- after this doc fill, rerun task-card re-evaluation for `telegram_user_id_allowlist_ui`.
