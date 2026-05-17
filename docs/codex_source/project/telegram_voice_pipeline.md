# Telegram voice pipeline

STATUS: IMPORTED_PROJECT_CONTRACT

Purpose:
- define the project contract for the Telegram voice path.
- record the access-control gate points before expensive operations.

Required pipeline order for allowed users:
- voice update arrives;
- access control checks `from.id` / `user_id`;
- allowed voice proceeds to download/getFile;
- downloaded file goes to STT/transcription;
- transcript enters the text understanding path;
- selected agent / Hermes / provider handling runs only after access is allowed;
- reply is sent to `chat.id`.

Denied-user contract:
- use deny-before-resource-use for unknown users;
- unknown users must be denied before getFile/download;
- unknown users must be denied before STT;
- unknown users must be denied before transcript handoff;
- unknown users must be denied before Hermes/provider/model call;
- unknown users must be denied before tool execution.

Logging and redaction:
- logs and audit summaries must not reveal tokens;
- logs and audit summaries must not reveal raw auth files;
- public-facing docs/reports should redact sensitive identifiers according to the safe redaction policy.

Project boundary:
- this file is a project contract, not an implementation file.
- the voice pipeline stays compatible with the allowlist placement in “Фин инструмент”.
