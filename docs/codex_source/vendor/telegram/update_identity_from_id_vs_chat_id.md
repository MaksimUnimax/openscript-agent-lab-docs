# Telegram update identity: from.id vs chat.id

STATUS: IMPORTED_CONTRACT

Purpose:
- distinguish Telegram `from.id` / `user_id` from `chat.id`.
- define the identity field used for the allowlist.
- define the delivery field used for replies and sends.

Correct contract:
- `from.id` / `user_id` is the user identity for allowlist decisions.
- `chat.id` is the delivery / conversation target.
- `chat.id` must not be used as a user allowlist identity.
- reply/send operations may continue to use `chat.id` as the target context.

Applies to:
- message updates;
- edited message updates;
- callback query updates;
- any update type where the bot must decide whether a user may consume protected resources.

Allowlist rule:
- keep the allowlist keyed by Telegram `from.id` / `user_id`.
- deny unknown users before expensive resource usage.
- do not fall back to `chat.id` when `from.id` is available.

Acceptance facts for future code:
- inbound safe_update should expose `user_id` / `from.id` separately from `chat.id`.
- deny decisions must be based on `user_id` / `from.id`.
- send target remains `chat.id`.

UI placement:
- allowlist controls belong in the current “Телеграмм” tab that project docs now treat as “Фин инструмент”.

False shortcut:
- `chat_id` allowlist.

Safety:
- do not print bot tokens or auth files.
- do not treat delivery identity as access identity.
