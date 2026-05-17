# Telegram router

STATUS: IMPORTED_PROJECT_CONTRACT

Purpose:
- define the project-level Telegram router contract.
- describe where identity extraction and access control belong in the Telegram path.

Router responsibilities:
- receive inbound update/message data;
- extract `user_id` / `from.id`;
- extract `chat_id`;
- extract command/text/voice/photo metadata;
- capture selected or active agent information if applicable;
- normalize the update into a safe internal shape.

Access-control placement:
- apply the access-control gate before expensive resource pipeline work.
- do not confuse identity with delivery target.
- router may perform a cheap pre-check, but it must not spend resources on unknown users.
- agent selection should happen only after access is known to be allowed, or in a safe cheap pre-check that does not spend model/runtime resources.

Universality:
- router should remain universal and not hardcode one agent.
- router should apply to all Telegram-bound agents using the shared bot/resource path unless a later task narrows scope.

UI / product boundary:
- the “Фин инструмент” UI owns the allowlist controls.
- the router enforces the runtime decision.
- Telegram Post Publisher is a separate future tool family and is not this access-control line.

Safety:
- do not use `chat_id` as the user allowlist identity.
- do not read secrets or auth files in docs-only runs.
