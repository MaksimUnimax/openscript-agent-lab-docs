# Техническое задание v0.3 — OpenScript Agent Lab + «Расходы с характером»

STATUS: IMPORTED_FROM_CHATGPT_UPLOAD
SOURCE_DOCUMENT: Тз(2).md
SOURCE_DATE: 2026-05-07
PROJECT: OpenScript Agent Lab
STATUS_NOTE: рабочее ТЗ после разворота к Hermes-first архитектуре
CURRENT_TZ_VERSION: v0.3
CURRENT_TZ_RULE: v0.3 supersedes v0.2 as the current project technical spec
HISTORICAL_NOTE: v0.2 remains the historical/original product draft if referenced anywhere

## 1. Назначение проекта

Создать учебно-практический продукт OpenScript, через который пользователь:

1. создаёт и настраивает собственных агентов;
2. управляет их документами, правилами, навыками и провайдерами;
3. видит каждого агента отдельно в интерфейсе;
4. может подключать разные источники LLM-ресурса;
5. получает прикладной результат на первом навыке, учёт расходов через Telegram;
6. учится агентной архитектуре на реальном рабочем примере.

Проект не должен быть просто Telegram-ботом вокруг одной LLM. Это должен быть Agent Lab, система, где отдельно существуют:
- агент;
- провайдер;
- навыки;
- бизнес-слой;
- интерфейс управления;
- Telegram Router.

## 2. Главный продуктовый результат

MVP должен позволить:

1. создать агента через UI или backend-команду;
2. задать агенту документы и правила;
3. выбрать provider branch для конкретного агента;
4. применить package агента в Hermes runtime profile;
5. позже выбрать агента в Telegram;
6. отправить сообщение или расход;
7. получить ответ в стиле выбранного агента;
8. при этом суммы, даты, отчёты и сохранение данных выполняет детерминированный код, а не LLM.

## 3. Термины

### Agent

Агент — отдельная сущность продукта.

У агента есть:
- slug;
- display_name;
- source package;
- Hermes runtime profile;
- документы;
- правила;
- skills;
- provider defaults;
- собственная память и история в runtime.

Количество агентов не ограничено архитектурно.

### Agent Package

Source-of-truth директория агента:

`/opt/openscript-agent-lab/agent-packages/<agent_slug>/`

Содержит:
- `manifest.json`
- `SOUL.md`
- `rules.md`
- `examples.md`
- `provider.defaults.json`
- `skills/`
- `README.md`

Эта директория является управляемым через git источником документов агента.

### Hermes Runtime Profile

Runtime-директория Hermes:

`/var/lib/openscript-agent-lab/hermes/profiles/<agent_slug>/`

Содержит runtime state:
- `config.yaml`
- `.env`
- `auth.json`
- `SOUL.md`
- `memories/`
- `skills/`
- `sessions/`
- `logs/`
- `cron/`
- state db files if enabled
- gateway state if enabled

Runtime state не должен редактироваться UI напрямую как source of truth. UI редактирует package, затем `agentctl apply` применяет изменения.

### Provider Branch

Способ подключения LLM-ресурса:
- `offline_template`
- `codex_resource`
- `api_runtime`

Provider branch независим от агента.

### Business Layer

Детерминированный слой Python/SQLite/scripts, который:
- читает и пишет БД;
- считает суммы;
- формирует отчёты;
- обрабатывает чек или черновик;
- возвращает компактный factual result агенту.

## 4. Обязательные архитектурные требования

### Универсальное количество агентов

Запрещено:
- проектировать только одного агента;
- проектировать только 4 агентов;
- hardcode списка агентов;
- требовать изменения кода для добавления нового агента.

Обязательно:
- поддерживать произвольное количество агентов;
- каждый агент отдельной строкой или карточкой в UI;
- каждый агент имеет отдельную директорию package;
- каждый агент имеет отдельный Hermes profile;
- каждый агент может иметь собственный provider default.

### Независимость агента и провайдера

Агент и провайдер должны переключаться независимо.

Пример:
- `agent=bookkeeper provider=api_runtime`
- `agent=bookkeeper provider=codex_resource`
- `agent=coach_bot provider=offline_template`

Переключение provider не должно менять `SOUL.md`.
Переключение агента не должно принудительно переписывать provider, кроме случая, когда продуктовая политика явно применяет default provider агента.

### Source package ≠ runtime profile

Source package:
- хранится в git;
- редактируется через UI;
- содержит документы, правила, defaults без секретов.

Runtime profile:
- хранится в `/var/lib`;
- содержит memory, sessions, runtime state;
- может содержать secret files;
- не должен попадать в git.

### No symlinks for SOUL.md/config.yaml

Запрещено связывать source и runtime через symlink для:
- `SOUL.md`;
- `config.yaml`.

Причина: Hermes использует atomic writes, которые могут заменить symlink обычным файлом и оторвать source of truth.

Правильный механизм:
UI edits source package → `agentctl apply` → copy/sync into runtime profile.

### Агент не владеет бизнес-логикой

Агенту запрещено:
- писать SQL;
- считать деньги;
- напрямую читать DB;
- сохранять расходы;
- выполнять shell по пользовательским сообщениям;
- видеть секреты;
- подтверждать чек без пользователя;
- выдумывать факты.

Агенту разрешено:
- помогать понять текст;
- задавать уточняющие вопросы;
- формулировать ответ;
- добавлять характер и тон;
- объяснять результат, полученный от business scripts.

## 5. Требования к Hermes integration

Установленная база на момент ТЗ:
- Hermes установлен вручную в sandbox;
- версия Hermes Agent v0.12.0 (2026.4.30);
- binary: `/opt/openscript-agent-lab/.venv-hermes/bin/hermes`;
- source: `/opt/openscript-agent-lab/vendor/hermes-agent`;
- `HERMES_HOME`: `/var/lib/openscript-agent-lab/hermes`;
- установка локальная, не глобальная;
- auth не делался;
- provider calls не делались.

Доказано:
- `hermes profile create <profile_name>` работает offline-safe;
- профиль создаётся в `/var/lib/openscript-agent-lab/hermes/profiles/<slug>/`;
- slug regex: `^[a-z0-9][a-z0-9_-]{0,63}$`;
- `default` reserved;
- нельзя slash, dots, spaces.

Provider per profile:
- `config.yaml`, `.env`, `auth.json`, `SOUL.md`, `memory/sessions/skills/logs` profile-local;
- provider/model config is per-profile;
- auth может иметь read-only global fallback, если локальных credentials нет.

Требование:
- продукт не должен зависеть от implicit global auth fallback;
- для строгой изоляции provider credentials должны быть явно понятны на уровне конкретного агента/profile.

## 6. Требования к agentctl

`agentctl` — backend/control layer, который будущий UI будет вызывать.

Расположение:
- `/opt/openscript-agent-lab/tools/agentctl`

Возможная реализация:
- `/opt/openscript-agent-lab/agent_lab/agentctl.py`

На начальных фазах — только Python stdlib.

Минимальный набор команд:
- `agentctl list`
- `agentctl create <slug> --display-name "<name>" --template blank`
- `agentctl validate <slug>`
- `agentctl show <slug>`
- `agentctl apply <slug> --dry-run`
- `agentctl set-provider <slug> <provider_mode> [--model <model_id>]`
- `agentctl get-provider <slug>`
- `agentctl diff <slug>`
- `agentctl clone <source_slug> <new_slug>`
- `agentctl delete <slug> --package-only --yes`

Будущие provider/auth команды:
- `agentctl provider list`
- `agentctl provider get <agent_slug>`
- `agentctl provider set <agent_slug> <provider_mode> [--provider <name>] [--model <model_id>] [--base-url <url>]`
- `agentctl provider auth-status <agent_slug>`
- `agentctl provider set-secret <agent_slug> <KEY_NAME>`
- `agentctl provider remove-secret <agent_slug> <KEY_NAME>`
- `agentctl provider codex-auth-instructions <agent_slug>`
- `agentctl provider validate <agent_slug>`
- `agentctl provider test-config <agent_slug> --no-model-call`

Slug validation:
- must match `^[a-z0-9][a-z0-9_-]{0,63}$`
- forbidden: `default`, `proof_profile_tmp`, slash, dot-dot, spaces, uppercase, non-ascii, path traversal.

`agentctl create`:
- creates source package;
- no secrets;
- no provider calls;
- no Hermes gateway;
- no production runtime profile without separate stage;
- no fixed agent count.

`agentctl apply`:
- first stage: `apply --dry-run` shows what would be copied;
- future stage: creates or updates Hermes runtime profile;
- copies `SOUL.md`, skills, relevant config;
- does not touch memories or sessions;
- creates backup and audit;
- idempotent;
- no symlinks.

`agentctl set-provider`:
- updates provider defaults source package;
- does not call provider;
- does not check API key with model call unless separately allowed;
- does not change `SOUL.md`.

## 7. Требования к Admin UI

UI должен стать интерфейсом управления агентами и провайдерами.
Он не должен быть просто редактором одного агента.

Минимальные будущие экраны:
1. Agent List
2. Agent Editor
3. Documents Editor
4. Skills Editor
5. Provider Tab
6. Runtime Status
7. Diff/Apply
8. Validation
9. Rollback/Version history
10. Audit log

Agent list columns:
- slug;
- display_name;
- package exists yes/no;
- runtime profile exists yes/no;
- provider_mode;
- provider/model summary;
- auth configured yes/no, без секрета;
- last applied version/time;
- docs valid/invalid;
- runtime divergence warning;
- safe memory/session counts if allowed.

Создание агента:
1. нажать “Создать агента”;
2. ввести slug;
3. ввести display_name;
4. выбрать blank или template, если templates есть;
5. создать source package;
6. показать документы в редакторе;
7. validate;
8. apply to runtime later.

UI должен редактировать:
- `SOUL.md`;
- `rules.md`;
- `examples.md`;
- `provider.defaults.json`;
- files under `skills/`.

UI не должен редактировать:
- secret files;
- runtime `auth.json`;
- runtime `.env` напрямую в обычном редакторе;
- memories/sessions без отдельного режима.

Provider UI должен быть per-agent.

Modes:
- `offline_template`
- `codex_resource`
- `api_runtime`

Для `api_runtime`:
- provider: DeepSeek, OpenRouter, custom OpenAI-compatible endpoint;
- API key input: write-only;
- base URL;
- model ID;
- auth-status без secret value.

Для `codex_resource`:
- показать статус;
- дать instruction/handoff;
- если OAuth/device-code нельзя сделать UI-only, честно показать terminal/browser flow;
- не читать и не показывать credentials.

Hermes Dashboard:
- не использовать как публичный продуктовый UI напрямую;
- dashboard может работать с config/API keys;
- открывать его наружу небезопасно;
- нужен наш UI с ограниченными действиями, audit и secret redaction.

## 8. Требования к Provider/Auth

Provider modes:
- `offline_template`
- `codex_resource`
- `api_runtime`

`offline_template`:
- всегда доступен;
- не требует auth;
- не делает model calls;
- emergency/demo fallback.

`api_runtime`:
- providers: DeepSeek, OpenRouter, custom OpenAI-compatible endpoint;
- API key хранится только в runtime profile secret path;
- key не попадает в git;
- UI не показывает saved value;
- auth-status показывает только presence/absence;
- validation по умолчанию не делает model call.

`codex_resource`:
- исследовать, возможен ли UI-only auth;
- если только device-code/terminal — заложить handoff;
- не импортировать Codex auth без отдельного proof;
- не полагаться на global fallback credentials.

## 9. Требования к Telegram Router

Не сейчас:
Telegram Router не реализуется, пока не готовы:
- `agentctl`;
- provider/auth design;
- source packages;
- runtime apply;
- хотя бы один provider proof.

Будущая архитектура:
- один Telegram bot.

Команды:
- `/agent`
- `/provider`
- `/status`
- `/skills`

Позже:
- `/llm_list`
- `/llm_active`
- `/llm_today`

Router хранит:
- `user_id -> active_agent`;
- `user_id -> provider override`;
- preferences;
- last activity;
- queue/timeout.

Input types:
- MVP: typed text.
- Later: voice transcript, photo receipt, MAX messenger.

Voice canonical rule:
voice → transcription → same text understanding layer as typed text.

## 10. Требования к Business Layer

Можно позже переиспользовать старый `/opt/openscript-expense-bot`, но только после отдельного extraction/refactor design.

Минимальный набор tools:
- `expense_add`
- `expense_recent`
- `expense_month_summary`
- `receipt_photo_draft`
- `receipt_manual_complete`
- `cancel_pending`

JSON request contract:

```json
{
  "request_id": "...",
  "user_id": "...",
  "agent_slug": "...",
  "provider_mode": "...",
  "tool": "expense_month_summary",
  "args": {
    "month": "2026-05"
  },
  "audit": {
    "source": "telegram_router"
  }
}
```

JSON response contract:

```json
{
  "request_id": "...",
  "ok": true,
  "data": {
    "total_minor": 124800,
    "currency": "RUB",
    "count": 18
  },
  "error": null,
  "audit": {
    "tool": "expense_month_summary",
    "duration_ms": 42
  }
}
```

Safety:
- agent must not write SQL;
- agent must not get raw DB;
- agent must not get secrets;
- agent must not mutate storage uncontrolled.

## 11. Безопасность и секреты

Do not store in git:
- Telegram token;
- OpenRouter key;
- DeepSeek key;
- Codex auth;
- Hermes auth.json;
- `.env`;
- credentials.

UI secret policy:
- write-only secret input;
- no saved secret display;
- only configured yes/no;
- no secret values in audit/logs.

Runtime paths:
- `/var/lib/openscript-agent-lab/hermes/...`
- `/var/log/openscript-agent-lab/...`

Source paths:
- `/opt/openscript-agent-lab/...`

## 12. Нефункциональные требования

1. Изоляция от старых проектов.
2. Минимальные изменения за run.
3. Proof-first.
4. Нет глобальных установок без отдельного design.
5. Нет systemd/nginx/firewall без отдельного design.
6. No hardcoded agent count.
7. No secrets in logs/git.
8. No model calls in unit tests.
9. No runtime profile modifications in source-only phases.
10. Rollback на каждом этапе.

## 13. Текущие опорные пути

Current paths:
- `/opt/openscript-agent-lab`
- `/var/lib/openscript-agent-lab`
- `/var/log/openscript-agent-lab`
- `/var/lib/openscript-agent-lab/hermes`
- `/opt/openscript-agent-lab/.venv-hermes/bin/hermes`
- `/opt/openscript-agent-lab/vendor/hermes-agent`

Old projects not to touch:
- `/opt/openscript-expense-bot`
- `/opt/ai-starter-community`
- `/opt/autopostmanager`

## 14. Acceptance criteria ближайших этапов

Provider Auth UI Proof accepted if:
- clear which auth flows can be handled through UI;
- clear what Codex requires and does not require terminal/device-code;
- clear if API keys can be written per-profile;
- Hermes Dashboard is not proposed as public UI;
- docs updated;
- no auth/model calls.

Agent Package Skeleton accepted if:
- `agent-packages/` exists;
- `agent-templates/blank/` exists;
- `agentctl` can create/list/show/validate/set-provider/get-provider/apply --dry-run;
- tests pass;
- no fixed agent count;
- no secrets/model calls.

Runtime Apply accepted if:
- `agentctl apply <slug>` creates/updates runtime profile;
- memories/sessions preserved;
- no symlinks;
- backup/audit exists;
- no secrets unless explicitly configured.

## 15. Current next step from original ТЗ

The historical next step in the original ТЗ was:
`OPENSCRIPT_AGENT_LAB_HERMES_PROVIDER_AUTH_UI_PROOF_20260507_01`

But before using this as current active next step, compare it with newer repo context, current roadmap, and completed work. Do not blindly rewind to 2026-05-07.

## 16. What not to do now

Do not do:
- production Telegram Router;
- admin UI implementation;
- Codex auth;
- API key setup;
- OpenRouter cleanup старого бота;
- OCR;
- voice;
- systemd;
- nginx;
- firewall;
- global installs;
- direct Hermes dashboard exposure;
- fixed four-agent templates.

## 17. Closed decisions

1. OpenRouter Free Pool не принимается как основа продукта.
2. Hermes-first линия принята.
3. Agent Lab создан отдельно.
4. Hermes установлен в sandbox.
5. Unlimited multi-agent architecture принята.
6. Per-profile provider config доказана.
7. Agent/provider switching independent.
8. UI должен управлять агентами, а не одним fixed persona.
9. Provider auth через UI нужно исследовать следующим шагом in the original context, but newer context may supersede this.
10. Старый expense-bot пока не удалять unless separate decommission/extraction task says otherwise.

## 18. Open questions from original ТЗ

1. Можно ли Codex auth сделать через UI полностью?
2. Или нужен terminal/device-code handoff?
3. Какой safest way хранить per-agent API keys?
4. Нужно ли использовать Hermes Dashboard API внутренне или писать config directly?
5. Когда делать `agentctl apply` real runtime?
6. Когда чистить OpenRouter tails из старого expense-bot?
7. Когда начинать Telegram Router?
8. Какой provider первым smoke-test после auth design: Codex or DeepSeek/custom API?

## Technical Spec Extension v0.4 — Fin Instrument Tab, Agent Farm, and Agent Tools

Status: imported as an extension, not a replacement for v0.3.

This extension records the user’s updated product direction:
- the current UI tab named “Телеграмм” should be treated/renamed as “Фин инструмент”;
- Telegram user_id allowlist/access control belongs in this “Фин инструмент” tab;
- future financial business tool work also belongs in this product surface;
- after access control, build a universal multi-agent farm with task runtime and monitoring;
- then add agent tools, starting with the Financial Agent Business Tool;
- later add Telegram Post Publisher and YouTube Parsing tool families.

Full extension:
- docs/codex_source/project/technical_spec_extensions/fin_tool_tab_agent_farm_and_agent_tools_v0_4.md
