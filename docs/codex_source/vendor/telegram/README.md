# Telegram vendor docs

STATUS: extracted

Это Telegram Bot API source-of-truth слой для будущих Codex prompt'ов.

Правила:
- future prompts должны читать exact paths из `docs/codex_source/index.yaml` и task cards.
- raw sources лежат в `_raw/`, короткие contract docs - в тематических поддиректориях.
- `roadmap`, `continuity/handoff` и `TZ` не являются Telegram vendor documentation.
- `chat_id` не является user allowlist identity для этой задачи.
- при extraction нельзя вызывать реальные Telegram Bot API методы или использовать bot token.
- этот каталог не является application code.
- старые root-level Telegram stub-файлы из фундамента не являются текущим source-of-truth; опираться нужно на indexed paths из `docs/codex_source/index.yaml`.

Структура:
- `_raw/` - сохраненные official docs, fetch report, source URLs и section extracts.
- `identity/` - Update, User, Chat, from.id, callback identity.
- `updates/` - getUpdates, offset, allowed_updates, webhook/polling.
- `files/` - File, Voice, getFile/download и redaction rules.
- `messaging/` - sendMessage, sendVoice, thread/topic delivery.
- `privacy/` - privacy mode и ограничения видимости.
- `security/` - user_id allowlist, deny-before-resource-use, audit redaction.
- `source_map/` - exact Bot API objects/methods and project mapping.

Status rules:
- `verified` only when official Telegram docs were actually read and the contract is direct.
- `extracted` when official docs support the contract and the file is a concise contract summary.
- `extracted_with_gaps` when the source is partial, project-specific, or an inference is involved.
- stub docs must not be used for fix-runs.
