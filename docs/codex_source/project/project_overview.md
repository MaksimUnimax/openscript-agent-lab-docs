# Project overview

STATUS: IMPORTED_FROM_CHATGPT_UPLOAD

OpenScript Agent Lab is not just a Telegram bot around one LLM. It is an agent lab where:
- agents are first-class product entities;
- agents have source packages and Hermes runtime profiles;
- provider choice is independent from agent identity;
- skills are instructions and requirements, not tool permissions;
- deterministic business logic owns money/date/report facts;
- Telegram is one product path, not the whole architecture.

The first applied scenario is “Расходы с характером”:
- the user sends a receipt or expense through Telegram;
- the system extracts or processes the factual data;
- the user confirms the draft;
- deterministic code stores and reports expenses;
- the chosen agent contributes tone, explanation and dialog quality.

Current source-of-truth split:
- vendor docs live under `docs/codex_source/vendor/**`;
- project docs live under `docs/codex_source/project/**`;
- append-only memory lives under `docs/codex_source/context/**`, `docs/codex_source/roadmap/**`, `docs/codex_source/module_map/**`.

The current technical spec is v0.3, imported from `Тз(2).md`.
v0.2 is historical/original and should not be treated as the current spec.

Missing next imports:
- actual roadmap;
- rules pack;
- module map expansion;
- remaining project architecture docs such as Telegram router, voice pipeline, Hermes reply path and access control.

Expanded product direction:
- Agent Lab is evolving into a universal multi-agent farm, not only a single-agent Telegram scenario.
- The current UI tab named “Телеграмм” should become “Фин инструмент”.
- “Фин инструмент” is the financial tool surface for agents, not merely Telegram settings.
- The financial agent scenario remains the first applied scenario, but it is no longer the only future agent line.
- Planned future tool families include the Financial Agent Business Tool, Telegram post publishing, and YouTube parsing.
