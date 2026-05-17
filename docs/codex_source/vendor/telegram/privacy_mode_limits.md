# Telegram privacy mode limits

STATUS: IMPORTED_CONTRACT

Purpose:
- explain what Telegram privacy mode does and does not do.
- prevent privacy mode from being mistaken for app-level access control.

Privacy mode limits:
- privacy mode controls which updates a bot may receive in some group contexts.
- privacy mode is not access control.
- privacy mode does not guarantee that unwanted users cannot consume bot resources.
- privacy mode does not replace a user_id allowlist.

Project contract:
- app-level allowlist remains required.
- deny-before-resource-use remains required.
- the same access-control rule applies in private chats and group contexts as appropriate for the bot flow.
- do not rely on BotFather privacy mode as the security boundary.

Operational rule:
- unknown users must still be denied before STT, download, provider/model calls, tool execution or other expensive paths.

UI placement:
- allowlist controls belong in “Фин инструмент”, not in a separate tab.
