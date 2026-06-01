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

## 19. Technical Spec Extension v0.5 — YouTube Post Draft Preparation Tool

Status: imported as an extension, not a replacement for v0.3.

This extension records the next YouTube pipeline stage after search, ranking, selection and moderation.
It defines a new post-draft preparation tool and keeps it separate from selection and from publication.

### 19.1. Назначение инструмента

`youtube.prepare_post_draft` takes YouTube videos that already passed ranking, selection and moderation and turns them into durable Telegram post drafts.

The tool must produce:
- coherent Telegram post text from verified source facts and subtitles/transcript;
- image brief and image prompt;
- generated illustration through an explicit image adapter;
- Telegram moderation preview with inline controls;
- approved-for-publication queue item for a future publication tool.

The tool is not the selection tool and is not the publication tool.

### 19.2. Product scenario

Typical flow:
1. A video has already been selected and approved by the existing YouTube selection/moderation line.
2. The operator starts `youtube.prepare_post_draft`.
3. The tool collects immutable source facts, transcript/subtitle material and selection notes.
4. The internal system editor agent drafts a post.
5. The tool creates an image brief and image prompt.
6. The image adapter generates or regenerates the illustration.
7. Telegram moderation receives the draft with inline actions.
8. If approved, the draft moves to an approved-for-publication queue.
9. Publication itself remains a separate future tool.

### 19.3. Architecture boundary

This stage must keep the Agent Lab separation of responsibilities:
- agent;
- provider;
- skills/tools;
- deterministic business layer;
- UI;
- Telegram Router.

The new tool must not become a god module.
It must not overload `youtube.select_candidates`.
It must not publish posts.
It must not collapse editorial reasoning, storage, Telegram callbacks and image backend control into a single free-form agent path.

Deterministic tool/business code owns:
- post draft storage;
- lifecycle state;
- Telegram dispatch and callback state;
- source snapshot persistence;
- image adapter calls;
- anti-repeat checks;
- queue handoff to publication.

The internal system agent owns:
- editorial reasoning;
- source summarization;
- draft wording;
- image brief writing;
- moderation-pack preparation.

### 19.4. Internal system agent

Tentative internal system agent name:

`youtube_post_editor_agent`

This is an internal system agent, not a public Telegram persona.
It must remain editor-only and must not be used as a general public chat persona.

The internal agent should have multiple skills, one skill per responsibility:

1. `source_fact_reader`
   - reads verified source facts: title, channel, URL, description, transcript/subtitles, selection reason, moderation notes;
   - must not invent facts.

2. `transcript_digest`
   - turns transcript/subtitles into structured digest, key points, useful insight, and audience relevance.

3. `telegram_editorial_writer`
   - writes the Telegram post draft;
   - target length: 900-1600 chars for normal text;
   - soft max: 1800 chars;
   - if used as a media caption, cap near 950 chars;
   - prefer 5-7 short paragraphs;
   - moderate emoji usage, roughly 3-6 emoji per post;
   - 0-3 hashtags max;
   - structure: hook, why it matters, key ideas, who it helps, link/CTA.

4. `telegram_style_guard`
   - validates readability, length, facts, no spam tone, no hallucinated claims.

5. `image_brief_writer`
   - creates image brief, image prompt, negative prompt, style tags, aspect ratio, and safety notes;
   - prefer no text inside the image unless explicitly required.

6. `image_generation_requester`
   - prepares a structured image generation request;
   - does not choose backend by hidden improvisation;
   - backend is selected by policy/config/operator action.

7. `moderation_packager`
   - prepares Telegram moderation preview payload and durable callback actions.

The tool may add more skills later, but each responsibility must stay separated.

### 19.5. Image generation adapter

Add an explicit deterministic adapter, tentative name:

`post_draft_image_adapter`

It supports two backend modes:
- `codex_imagegen_cli`
- `openai_image_api`

Contract:
- the same draft/image prompt contract must work with both backend modes;
- backend choice must be explicit via config, policy or operator action;
- if CLI quality is poor or runtime proof fails, the same system may switch to OpenAI API without changing the editorial agent logic;
- the adapter records backend mode, prompt, output asset ref, generation status, error, and regeneration attempts.

The adapter is a business/tool boundary, not an editorial personality.

### 19.6. Storage and lifecycle

Use a durable post-draft state separated from source candidates.

Suggested entity:

`youtube_post_drafts`

Suggested fields:
- id;
- candidate_id;
- video_id;
- source_url;
- source_title;
- source_channel;
- source_facts_snapshot_json;
- transcript_snapshot_ref;
- editor_agent_id;
- editor_skill_versions_json;
- draft_text;
- draft_text_length;
- image_brief;
- image_prompt;
- image_negative_prompt;
- image_backend_mode;
- image_asset_ref;
- image_generation_status;
- moderation_status;
- publication_status;
- created_at;
- updated_at;
- approved_at;
- published_at;
- rejected_at;
- last_error.

Suggested lifecycle states:
- candidate_ready_for_draft;
- draft_created;
- text_regeneration_requested;
- image_prompt_created;
- image_generation_requested;
- image_generated;
- image_generation_failed;
- moderation_sent;
- text_regeneration_pending;
- image_regeneration_pending;
- approved_for_publication;
- rejected_or_needs_changes;
- published_later.

Recommended lifecycle rules:
- source candidates/videos remain immutable and persistent;
- approved/selected videos are never deleted after drafting or moderation;
- the draft gets revisions, not source-candidate duplication;
- if a candidate already has an active or approved draft, a new draft must not auto-create unless explicitly requested as a revision;
- regeneration creates a revision/version of the post draft, not a duplicate source candidate.

### 19.7. Anti-repeat rules

- Source candidates/videos must remain in DB forever.
- Approved/selected videos must not be deleted after drafting or moderation.
- Already selected/approved videos must not be selected again.
- Draft generation must not auto-repeat on the same approved source unless a revision is explicitly requested.
- A revision should update draft version state, not create a new source record.

### 19.8. Telegram moderation flow

Moderation preview should not rely only on a media caption because a caption is shorter than a normal text message.

Recommended moderation preview:
- image/media message if available;
- text message with the full post draft;
- control message or markup with inline buttons.

Inline actions:
- approve draft;
- regenerate text;
- regenerate image;
- regenerate both;
- reject / needs changes;
- show source;
- next draft.

Callback payloads must reference durable draft ids, not raw post text or hardcoded message ids.

### 19.9. Publication queue handoff

Publication is a future separate tool.

After moderation approval:
- `moderation_status = approved_for_publication`;
- `published_at = null`;
- `publication_status = ready`.

The future publication tool consumes only approved, unpublished drafts.

This tool does not publish to a Telegram channel.

### 19.10. Acceptance criteria

The future implementation is accepted only if:
1. selected/approved videos remain stored and are not deleted;
2. anti-repeat prevents repeated selection and drafting by default;
3. every approved video can produce a durable draft;
4. draft text is Telegram-ready and fact-grounded;
5. image prompt is created;
6. image generation works through at least one proven backend;
7. the adapter supports both `codex_imagegen_cli` and `openai_image_api` modes by contract;
8. Telegram moderation has inline controls;
9. regeneration works through durable draft state;
10. approval moves the draft to an approved-for-publication queue;
11. publication is not performed by this tool;
12. tests and proof cover the lifecycle, not just isolated functions.

### 19.11. Universal boundaries

The design must not hardcode:
- one agent;
- one user;
- one Telegram chat/channel;
- one provider;
- one image backend;
- one video;
- one language;
- one message id;
- one test case.

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
