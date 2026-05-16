# Hermes vendor docs

STATUS: extracted

Это source-of-truth слой Hermes для будущих Codex prompt'ов.

Правила:
- future prompt'ы должны читать exact paths из `docs/codex_source/index.yaml` и task cards.
- raw sources лежат в `_raw/`, а короткие contract docs - в тематических поддиректориях.
- `roadmap`, `continuity/handoff` и `TZ` не являются vendor documentation.
- если required doc имеет `STATUS: STUB`, related fix-run must stop with `STOP_DOCS_MISSING`.
- этот каталог не является application code.

Структура:
- `_raw/` - сохраненные official docs, llms.txt, llms-full.txt, CLI help и source maps.
- `overview/` - карта Hermes docs и базовые пути входа.
- `auth/` - auth store, import/adopt, token invalidation, device-code semantics.
- `providers/` - provider resolution и provider contracts.
- `profiles/` - runtime profiles и layout состояния.
- `runtime/` - gateway, API server и Codex app-server runtime.
- `tools/` - tool registry, toolsets, MCP/tool gateway.
- `skills/` - skills runtime и bundled Codex skill.
- `memory/` - memory/session contracts.
- `platforms/` - messaging adapters such as Telegram.
- `troubleshooting/` - known failure modes and guardrails.
- `source_map/` - local Hermes source files and symbols used for extraction.
