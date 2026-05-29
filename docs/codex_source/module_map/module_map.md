# Append-only module map

STATUS: INITIAL_FROM_CURRENT_REPO_DOCS

This file is append-only.

Do not rewrite historical blocks destructively.

<!-- MODULE_MAP_APPEND_BEGIN id=MM_20260516_0001 -->
Current high-level module map from repo tree:
- `agent_lab/` - runtime application code and static UI
- `docs/codex_source/` - source-of-truth docs and project memory
- `vendor/hermes-agent/` - local Hermes vendor source checkout
- `agent-packages/` - package workspace with unrelated dirty state
- `tests/` - automated tests
- `tools/` - utility scripts
- `tool-registry/` - registry data
- `.venv-hermes/` - local virtual environment
<!-- MODULE_MAP_APPEND_END id=MM_20260516_0001 -->

<!-- MODULE_MAP_APPEND_BEGIN id=MM_20260516_0002 -->
Current module map snapshot imported from bounded repo inventory and imported docs.

Use these files for the detailed current map and safe boundaries:
- `docs/codex_source/module_map/imported/current_module_map_snapshot.md`
- `docs/codex_source/module_map/imported/safe_boundaries_snapshot.md`

Current status:
- `docs/codex_source/` is the project documentation source-of-truth for ChatGPT and Codex.
- `agent_lab/` is application/backend/UI code and must not be edited in docs-only runs.
- `agent-packages/` is agent package workspace and unrelated dirty state that must not be accidentally staged.
- `vendor/hermes-agent/` is the local Hermes vendor source checkout and was only inventoried at top level in this run.
- `tools/` and `tests/` are supporting code roots used for backend commands and regression checks.
- `tool-registry/` stores tool registry data used by the runtime.

Pending proof:
- exact ownership split inside `agent_lab/` is based on bounded inventory and top-level imports;
- task cards still need re-evaluation after this module map import;
- `agent-templates/` is not present in the current tree snapshot and remains pending proof if introduced later.
<!-- MODULE_MAP_APPEND_END id=MM_20260516_0002 -->

<!-- MODULE_MAP_APPEND_BEGIN id=MM_20260516_EXPAND_TZ_FIN_TOOL_TAB_AGENT_FARM_AND_AGENT_TOOLS source=chatgpt_inline_product_update accepted_by_user=yes -->

## 2026-05-16 — Planned module families: “Фин инструмент”, Agent Farm and Agent Tools

### Context

The user clarified that the financial tool should not be created as a separate new tab.

The current UI tab named “Телеграмм” is already the specialized financial-agent/Telegram/voice surface and should become “Фин инструмент”.

This update adds planned module families and UI placement only.
No implementation is included.

### Planned UI/product surface: “Фин инструмент”

Status:
- PLANNED / NEEDS_TASK_CARD_REEVALUATION / NEEDS_DESIGN / NEEDS_PROOF

Meaning:
- current “Телеграмм” tab becomes “Фин инструмент”;
- financial tool surface for agents;
- place Telegram user_id allowlist here;
- keep financial-agent voice/Telegram settings here;
- future financial business tool controls/status live here.

Boundaries:
- not a separate new tab for the financial tool;
- not generic Telegram publisher;
- not YouTube parsing;
- not general agent farm runtime;
- access-control here is for financial tool/bot resource protection;
- Telegram post publisher must be a separate future tool family.

### Planned module family: Agent Farm / Task Runtime

Status:
- PLANNED / NEEDS_DESIGN / NEEDS_PROOF

Responsibilities:
- task creation;
- task assignment to agents;
- execution target selection;
- task status tracking;
- progress monitoring;
- result artifacts;
- future retry/repair policy.

Boundaries:
- must not be hardcoded to one agent or fixed agent count;
- must not be mixed into unrelated UI files;
- must not become a god module;
- must be designed before implementation.

### Planned module family: Financial Agent Business Tool

Status:
- PLANNED / NEEDS_DESIGN / NEEDS_PROOF

Clarification:
- This is not just a database.
- It is a deterministic business tool for financial agents.
- It belongs under the “Фин инструмент” product direction.

Responsibilities:
- database schema/storage;
- safe scripts for writes/reads;
- receipt ingestion/reading;
- validation;
- summaries/reports;
- factual result returned to agent.

Boundaries:
- agent must not write SQL;
- agent must not mutate DB directly;
- agent must not invent totals;
- agent calls tool/scripts;
- tool owns persistence and calculations.

### Planned module family: Telegram Post Publisher Agent/Tool

Status:
- PLANNED / NEEDS_DESIGN / NEEDS_PROOF

Responsibilities:
- future post creation/review/scheduling/publishing to Telegram.

Boundaries:
- separate from “Фин инструмент”;
- separate from Telegram user_id allowlist;
- requires separate vendor/API/safety proof before implementation.

### Planned module family: YouTube Parsing Agent/Tool

Status:
- PLANNED / NEEDS_DESIGN / NEEDS_PROOF

Responsibilities:
- future YouTube parsing for agent tasks.

Boundaries:
- separate from financial tool and Telegram publisher;
- requires vendor/legal/API/source docs proof before implementation.

### Future task tools TBD

Status:
- PLANNED_PLACEHOLDER / NEEDS_SPEC

Boundaries:
- no implementation;
- no module ownership until user specifies concrete task.

### Current active boundary

Immediate active work remains:
- `telegram_user_id_allowlist_ui` task-card re-evaluation;
- include “Фин инструмент” tab placement/rename decision.

Do not start implementation of the planned module families from this docs update.

<!-- MODULE_MAP_APPEND_END id=MM_20260516_EXPAND_TZ_FIN_TOOL_TAB_AGENT_FARM_AND_AGENT_TOOLS -->

<!-- MODULE_MAP_APPEND_BEGIN id=MM_20260519_CONTEXT_TOOLS_VOICE_BOUNDARIES source=chatgpt_inline_project_update accepted_by_user=yes -->

## 2026-05-19 — CONTEXT / TOOLS / VOICE module boundaries

### CONTEXT boundary

Receipt context must be projected into the next Telegram turn as structured context, not as LLM memory.

Owned by source modules around:
- Telegram context envelope;
- receipt context hydration;
- Hermes prompt serialization.

Known live-ready commit:
- `8cdba40`

Context must include:
- `receipt_draft`
- `receipt_item_lines`
- `last_action_result`
- `prior_assistant_reply`

### TOOLS boundary

Fin operations must be exposed as Hermes tools, not only app-local handlers.

Known live-ready commit:
- `fb6f892569dc78db5d24bc8541d297fc9ab22556`

Current Hermes-visible receipt toolset:
- `fin.receipt`
- `receipt_current`
- `receipt_items`
- `receipt_confirm`
- `last_receipt`

The model may decide when a tool is needed.
The tool executor reads/writes DB.
The final answer must be based on tool result.

The LLM must not write DB directly.

### VOICE boundary

Voice must be a universal transport/tool capability.

Voice must do only:
- receive Telegram voice/audio;
- perform STT/transcription;
- produce transcript + safe metadata;
- hand off to canonical text/Hermes agent/tool path.

Voice must not own:
- receipt logic;
- confirmation logic;
- Fin business logic;
- DB write logic;
- agent-specific tool policy.

### Provider-safe tool names

Provider-facing tool names must satisfy provider validation.

Latest failure:
- provider rejected `fin.expense_add`
- accepted regex: `^[a-zA-Z0-9_-]+$`

Therefore a generic provider-safe tool-name mapping may be required:
- internal tool ids may stay dot-named;
- provider request names must be safe;
- provider-safe calls must map back to internal tool ids;
- mapping must be generic, not Fin-only.

### Universality boundary

Do not hardcode:
- `plankton`;
- any selected agent slug;
- chat/user IDs;
- Fin-only voice path;
- receipt-only voice path.

Use:
- selected_agent;
- capability settings;
- agent tool allowlist;
- resolved enabled_toolsets.

<!-- MODULE_MAP_APPEND_END id=MM_20260519_CONTEXT_TOOLS_VOICE_BOUNDARIES -->

<!-- MODULE_MAP_APPEND_BEGIN id=MM_20260520_RECEIPT_EXTRACTION_BOUNDARY_AND_DOCS_WORKFLOW source=chatgpt_inline_project_update accepted_by_user=yes -->

## 2026-05-20 — Receipt extraction boundary and docs-update workflow clarification

### Context

The current failing product area is receipt extraction inside the Fin/business layer.

The docs-update workflow was also clarified: ChatGPT must synthesize explicit append blocks after checking the last saved repo-docs point; Codex must not invent what to append.

### Receipt extraction boundary

Receipt extraction belongs to the deterministic business layer, not to the agent language layer.

The route is:

Telegram photo
-> selected agent / Hermes
-> `receipt_photo_draft`
-> receipt OCR/preprocessing
-> receipt parser
-> structured tool result
-> Hermes explanation/clarifying question
-> Telegram reply

### Business layer owns

The business layer owns:

- OCR/preprocessing for receipt image;
- extraction of merchant;
- extraction of date/time;
- extraction of total;
- extraction of item lines;
- extraction of quantities;
- extraction of item prices;
- extraction of item sums;
- structured missing_fields;
- draft persistence;
- deterministic confirmation rules.

### Agent/Hermes owns

Agent/Hermes owns:

- deciding to use receipt tool when presented with receipt photo;
- asking the user for missing information;
- explaining what was extracted;
- style and character of the answer.

### Documentation workflow boundary

For future docs updates:

- ChatGPT owns context synthesis.
- ChatGPT must read current public repo-docs first.
- ChatGPT must find the last saved append/snapshot point.
- ChatGPT must use only new dialogue content after that point.
- ChatGPT must write explicit context/roadmap/module-map append blocks inline.
- Codex owns applying those exact blocks to repo docs, checks, commit/push and public docs refresh.
- Codex must not reconstruct history from memory or old prompts.

### Forbidden boundary violations

Do not:

- make the agent invent totals or item lines;
- put receipt parsing in prompt text;
- hardcode one receipt total/date/item list;
- answer from app layer instead of Hermes;
- write final expense without confirmation;
- treat one receipt image as architecture;
- grant receipt tools to non-Fin agents;
- ask Codex to invent docs append content;
- duplicate old already-saved context.

### Current source areas for future receipt extraction work

Future receipt extraction work should focus on the narrow owners:

- `agent_lab/fin_instrument/**`
- `vendor/hermes-agent/tools/fin_receipt_tool.py`
- `tools/hermes_vendor_overlay/hermes-agent/tools/fin_receipt_tool.py`
- receipt OCR/parser tests under `tests/`

Only inspect Telegram/Hermes routing if current proof shows `receipt_photo_draft` is not being called.

<!-- MODULE_MAP_APPEND_END id=MM_20260520_RECEIPT_EXTRACTION_BOUNDARY_AND_DOCS_WORKFLOW -->

## 2026-05-21 — Module map update: YouTube subtitles tool implemented

Implemented module family:

- user-facing tool family: `Ютуб`
- internal tool slug: `youtube.subtitles_get`
- capability: retrieve available YouTube subtitles/transcript segments with timings by video URL.

Current source ownership:

- `agent_lab/youtube_subtitles.py`
  - deterministic executor;
  - YouTube URL validation and `video_id` extraction;
  - `youtube-transcript-api` adapter;
  - transcript selection;
  - timestamped segment normalization;
  - normalized error model.

- `agent_lab/admin_server.py`
  - operator test route;
  - UI attach route for selected agent;
  - source-package update route for agent attachment.

- `agent_lab/static/index.html`
  - top-level `Ютуб` tab;
  - operator test form;
  - agent attachment UI section.

- `agent_lab/static/app.js`
  - operator test UI behavior;
  - language priority payload handling;
  - agent attachment UI behavior.

- `tool-registry/tools.json`
  - canonical registry entry for `youtube.subtitles_get`.

- `tools/hermes_vendor_overlay/hermes-agent/tools/youtube_subtitles_tool.py`
  - Hermes-visible tool wrapper/registration.

- `agent-packages/<agent>/skills/youtube-subtitles-tool.md`
  - per-agent skill/doc created when the tool is attached through UI.

- `agent-packages/<agent>/tools.json`
  - per-agent tool binding created/updated through UI source-package flow.

- `tests/test_youtube_subtitles_tool.py`
  - executor, URL parsing, language fallback, output/error behavior.

- `tests/test_admin_server.py`
  - operator route/UI/attachment route coverage.

- `tests/test_runtime_apply.py`
  - runtime apply mirroring for YouTube tool binding and registry snapshot.

Runtime/source boundary:

- source package is updated through UI;
- Hermes runtime is updated through existing apply flow;
- runtime profile is not the source-of-truth;
- agent attachment is per selected agent, not global;
- Squidward was used as a manual proof agent, not hardcoded in product source.

This module family must remain separate from:

- Fin Instrument / receipt OCR;
- Telegram Post Publisher;
- Telegram access control;
- Voice/STT transport;
- Agent Farm / Task Runtime.

Forbidden regressions:

- do not move YouTube transcript logic into Telegram routing;
- do not move transcript logic into agent prompts only;
- do not use LLM-generated transcripts;
- do not introduce video/audio download in this tool path;
- do not globally enable the tool for all agents;
- do not hardcode one agent, one video, one chat, or one provider.

## 2026-05-21 — Module map planning: YouTube Research pipeline and Telegram publisher agent

A new planned module family is introduced:

- product direction: Telegram AI/Vibecoding Publisher Agent
- first technical module family: YouTube Research pipeline

### Planned source ownership

No source files are implemented yet for this block.

Expected future ownership should be narrow and separated:

- future YouTube search/provider module for `youtube.search_candidates`:
  - responsible for video search metadata only;
  - must not collect subtitles directly unless routed through the subtitle stage.

- existing `agent_lab/youtube_subtitles.py`:
  - remains the subtitle extraction executor;
  - should be reused by `youtube.collect_subtitles_for_candidates`.

- future YouTube research storage module:
  - responsible for video metadata, transcript storage, candidate status, duplicate/published state, retention.

- future ranking module:
  - deterministic scoring/filtering.

- future editorial evaluation module/tool:
  - LLM-assisted evaluation over stored facts/transcripts only.

### Boundary decisions

Do not mix in this first research block:

- Telegram publishing;
- image generation;
- voice/STT;
- Fin Instrument/receipt OCR;
- Agent Farm task runtime;
- Telegram access control.

### Required future boundary

The database/state layer must be shared by the YouTube research tools.

Individual tools must not each invent their own storage/status model.

### Important anti-repeat boundary

Published content state must be stored and checked before returning candidates for post creation.

Published videos must not re-enter the posting queue.

## 2026-05-22 — Module map boundary update: YouTube search agent tool gate fix

### Module ownership update

This block clarifies the module boundaries for YouTube Research agent tools and Hermes visibility.

### YouTube search/intake owner

Primary source area:

- `agent_lab/youtube_search_candidates.py`

Responsibilities:

- saved profile handling;
- YouTube search candidate collection;
- deterministic filtering;
- deduplication;
- candidate DB writes;
- metadata enrichment over saved candidates;
- `youtube.search_candidates` gate/check function;
- active Hermes profile detection for the search tool.

Critical rule:

The search tool gate must resolve the live per-profile Hermes home through the same pattern as working Hermes tools:

- use `hermes_constants.get_hermes_home()`;
- do not use static `paths.HERMES_HOME` when determining the active runtime profile.

### YouTube subtitles baseline

Primary source area:

- `agent_lab/youtube_subtitles.py`

This remains the known-good baseline for live per-profile HERMES_HOME resolution and gate/check_fn behavior.

When a new YouTube/Hermes tool is invisible, compare it against the subtitles tool before assuming session/runtime issues.

### Hermes wrapper propagation owner

Primary source areas:

- `tools/hermes_vendor_overlay/hermes-agent/tools/`
- `tools/restore_hermes_vendor.py`
- `tools/agentctl`

Responsibilities:

- tracked overlay wrappers;
- copying/restoring wrappers into actual vendor checkout;
- ensuring UI startup restores Hermes vendor wrappers.

Resolved issue:

`youtube_search_candidates_tool.py` initially existed only in overlay and not actual vendor path. Universal startup restore fixed this; do not manually copy wrappers for a single agent.

### Agent source package / runtime apply boundary

Primary source areas:

- `agent_lab/storage.py`
- `agent_lab/admin_server.py`
- `agent_lab/runtime_apply.py`
- `agent-packages/<slug>/tools.json`
- `agent-packages/<slug>/skills/*.md`
- `/var/lib/openscript-agent-lab/hermes/profiles/<slug>/.agent-lab/**`

Boundary:

- UI attach writes source package for selected agent.
- Runtime apply copies package/skills/registry snapshot into runtime profile.
- Codex must not connect tools to real agents as a normal implementation method.
- User performs manual attach/runtime apply/Telegram tests.

### Hermes safe registry / gateway discovery boundary

Primary source areas:

- `vendor/hermes-agent/tools/_provider_safe_registry.py`
- `vendor/hermes-agent/model_tools.py`
- `vendor/hermes-agent/gateway/run.py`

Responsibilities:

- tool wrapper registration;
- check_fn/gate filtering;
- provider-safe name mapping from dotted ids to underscore tool names;
- gateway discovered tool definitions.

Debug rule:

If a tool is attached but invisible to the agent, inspect in this order:

1. runtime profile binding;
2. wrapper import;
3. gate/check_fn result;
4. `registry.get_definitions(...)`;
5. gateway discovered tool names;
6. only then inspect session artifacts.

Do not start from session reset.

### Session layer diagnostic boundary

`session_meta.tools` can show where a tool is absent, but it is not automatically the root cause.

Before modifying session lifecycle code, always prove whether the tool passed:

- wrapper import;
- check_fn/gate;
- safe registry filtering;
- gateway discovery;
- `agent.tools`.

For the YouTube search visibility bug, session code was not the owner. The owner was `agent_lab/youtube_search_candidates.py` gate/profile detection.

### Explicit non-owner modules for this issue

Do not modify for this class of bug unless fresh proof says they are first broken:

- Telegram router;
- Telegram delivery/send path;
- YouTube search provider logic;
- subtitles extraction logic;
- DB cleanup/migrations;
- model/provider auth;
- session deletion/reset code.

## 2026-05-22 — Module map boundary update: YouTube select_candidates contract

### New planned tool boundary

`youtube.select_candidates` is the next planned YouTube Research pipeline tool.

It is an independent selection/sorting stage between stored YouTube search candidates and the future editing/formatting stage.

### Manual-first but Hermes-mediated

The tool must be manual-first: the operator must be able to start selection and review results manually before a future public-manager agent uses it.

Manual-first does not mean direct backend bypass.

The manual operator path must use the same Hermes/tool contract that future agents will use.

### Owner boundary

The selection tool owns:

- reading stored YouTube candidates;
- deterministic pre-filter/pre-rank;
- optional internal curator/evaluator Hermes profile call;
- operator review batch creation;
- candidate lifecycle status updates;
- structured selected-candidates result.

The selection tool does not own:

- YouTube search collection;
- transcript collection;
- editing/formatting next-stage content;
- image generation;
- public Telegram publishing;
- system_filter behavior;
- global agent orchestration.

### Role boundary

Do not confuse:

- human operator;
- manual selection tool;
- internal curator/evaluator Hermes profile;
- future public-manager agent;
- future editing/formatting tool.

The future public-manager agent may initiate `youtube.select_candidates`, but the selection tool must not initiate the next formatting/editing tool.

### State boundary

DB state is objective and lifecycle-oriented.

Hermes memory is learned curator taste.

Source policy is current editorial priority.

Policy and DB facts outrank learned memory.

### Forbidden coupling

Do not hardcode:

- Squidward;
- Plankton;
- one Telegram chat;
- one operator;
- one provider;
- one query;
- one channel;
- one current video.

Do not couple `youtube.select_candidates` directly to editing, formatting, image generation, or Telegram publishing.

<!-- MODULE_MAP_APPEND_BEGIN id=MM_20260522_YOUTUBE_SELECT_CANDIDATES_SYSTEM_OPERATOR_CORRECTION source=chatgpt_inline_project_update accepted_by_user=yes -->

## MM_20260522_YOUTUBE_SELECT_CANDIDATES_SYSTEM_OPERATOR_CORRECTION

### Boundary correction

`youtube.select_candidates` must not be described as a direct human/manual backend path.

The tool is Hermes-mediated.

The sorting/evaluation actor is a system Hermes operator / curator profile inside the tool.

### Correct owner boundary

`youtube.select_candidates` owns:

- reading stored YouTube candidate facts;
- deterministic pre-filter/pre-rank;
- invoking the system Hermes operator / curator profile for selection when enabled;
- returning selected candidate IDs and status information;
- recording candidate lifecycle statuses.

It does not own:

- direct manual DB bypass;
- future public-manager orchestration;
- next editing/formatting tool execution;
- image generation;
- Telegram publishing;
- system_filter behavior.

### Correct actor boundary

Do not confuse:

- future public-manager agent that initiates the tool;
- `youtube.select_candidates` as the tool/business contract;
- system Hermes operator / curator profile inside the tool;
- optional human reviewer through Telegram buttons;
- future editing/formatting tool.

### Forbidden coupling

The system sorting operator must not call the next editing/formatting tool directly.

The selection tool returns structured selected candidates only.

<!-- MODULE_MAP_APPEND_END id=MM_20260522_YOUTUBE_SELECT_CANDIDATES_SYSTEM_OPERATOR_CORRECTION -->

<!-- MODULE_MAP_APPEND_BEGIN id=MM_20260522_YOUTUBE_CURATOR_SELECT_CANDIDATES_RUNTIME_UI_BOUNDARY source=chatgpt_inline_project_update accepted_by_user=yes -->

## MM_20260522_YOUTUBE_CURATOR_SELECT_CANDIDATES_RUNTIME_UI_BOUNDARY

### Implemented module boundary

The `youtube.select_candidates` / `youtube_curator` stack now spans these owners.

### Selection tool owner

Owner:

- `agent_lab/youtube_select_candidates.py`

Responsibilities:

- read saved YouTube candidate facts;
- deterministic pre-filter/pre-rank;
- build compact curator snapshots;
- validate curator responses;
- return planned selection actions;
- own writes to `youtube_selection_batches` and `youtube_candidate_selection_state`;
- keep `next_tool_called: false`.

Non-responsibilities:

- live Telegram publication;
- next editing/formatting tool call;
- image generation;
- YouTube provider search;
- runtime memory editing;
- `system_filter` behavior.

### Candidate fact owner

Owner:

- `agent_lab/youtube_search_candidates.py`

Responsibilities:

- YouTube search/intake facts;
- metadata enrichment facts;
- saved candidate rows;
- base candidate statuses such as `found`, `duplicate`, `rejected`, `published`, `expired`.

Selection-specific lifecycle states must not be forced into the old base status enum.

### Selection storage owner

Tables:

- `youtube_selection_batches`
- `youtube_candidate_selection_state`

Responsibilities:

- selection batch state;
- selected/approved/skipped/ready/rejected state;
- cooldown for skipped candidates;
- handoff marker for future next stage.

`rejected` remains the hard-block state and updates the base candidate row too.

### Curator source package owner

Source package:

- `agent-packages/youtube_curator/**`

Important files:

- `SOUL.md` — identity and boundaries;
- `rules.md` — primary human-editable source policy;
- `skills/youtube-selection-policy.md` — operational policy guidance;
- `examples.md`;
- `provider.defaults.json`;
- `manifest.json`.

The source package is protected/internal/system.

Protected slugs currently include:

- `system_filter`
- `youtube_curator`

Protection authority is source-owned code, not manifest-only user-editable metadata.

### Runtime profile owner

Runtime profile:

- `/var/lib/openscript-agent-lab/hermes/profiles/youtube_curator`

Created through:

- `agent_lab/runtime_apply.py::apply_agent`
- `agent_lab/agentctl_core.py::apply_agent`
- admin runtime apply endpoints.

Runtime profile stores runtime state, sessions, logs, and future profile-local memory.

Runtime memory must not be edited by the YouTube Curator settings UI.

### Admin API/UI owners

Backend owner:

- `agent_lab/admin_server.py`

UI owners:

- `agent_lab/static/index.html`
- `agent_lab/static/app.js`

Current UI location:

- `Ютуб → Сортировка`

Current UI capabilities:

- read-only `youtube_curator_status` panel;
- source-policy editor for `agent-packages/youtube_curator/rules.md`;
- apply dry-run control;
- explicit runtime apply control.

Current UI non-capabilities:

- no live curator test button;
- no Telegram button;
- no YouTube search call from curator panel;
- no memory reset;
- no auto-mode;
- no next editing/formatting tool call.

### Runtime apply boundary

Existing endpoints reused:

- `POST /api/agents/youtube_curator/runtime/apply-dry-run`
- `POST /api/agents/youtube_curator/runtime/apply`

No custom apply endpoint was added.

Apply copies source package state into runtime and preserves runtime-owned files such as:

- `.env`
- `auth.json`
- `memories/`
- `sessions/`
- `logs/`

Apply must not call provider/model, Telegram API, YouTube live search, or DB mutation.

### Telegram routing boundary

The Telegram “Бот-роутер” UI confusion was resolved.

Current accepted model:

- the selected router agent shown in UI is active/default/fallback routing target;
- it is not proof of a separate LLM router brain;
- Telegram agents answer and switching works;
- no Telegram/router fix is active for this YouTube curator block.

Do not create a `telegram_router` system agent as part of YouTube curator work unless a later explicit architecture design approves it.

<!-- MODULE_MAP_APPEND_BEGIN id=MM_20260528_YOUTUBE_RANKED_BATCH_LIFECYCLE_MODULE_BOUNDARY source=chatgpt_dialogue_and_codex_reports -->
## 2026-05-28 — YouTube ranked moderation lifecycle boundaries

Module boundary update:
YouTube ranked moderation lifecycle is owned by backend business modules, not Telegram connector and not Hermes alone.

Relevant source ownership:
- agent_lab/youtube_select_candidates.py
  - candidate snapshot and Curator selection boundary;
  - ranking target handling;
  - Curator contract validation.
- agent_lab/youtube_selection_moderation_service.py
  - durable ranked batch state;
  - active/resumable batch lookup;
  - current stack / next stack cursor;
  - moderation_status lifecycle;
  - zero-row/no-eligible structured states.
- agent_lab/youtube_agent_moderation_dispatch.py
  - orchestration between ranked batch lifecycle and Telegram card dispatch;
  - must check active non-empty batch before fresh ranking;
  - must not call Curator when pending ranked rows are available;
  - must not report ok=true for zero rows.

Out of scope for ranked batch lifecycle fixes:
- agent_lab/telegram_connector.py
- agent_lab/telegram_polling.py
- agent_lab/telegram_bindings.py
- agent-packages/**
- Fin/receipt modules
- Hermes auth/provider configuration
- YouTube search implementation, unless a future proof shows candidate ingestion/search is the actual blocker.

Key boundary rule:
Telegram inline next stack is a UI/control surface for requesting the next configured slice from the same ranked batch. It must not own ranking, DB state, search, or Curator selection logic.
<!-- MODULE_MAP_APPEND_END id=MM_20260528_YOUTUBE_RANKED_BATCH_LIFECYCLE_MODULE_BOUNDARY -->

<!-- MODULE_MAP_APPEND_BEGIN id=MM_20260528_RECEIPT_FULL_EXTRACTION_BOUNDARY source=chatgpt_dialogue_and_codex_reports -->
## MM_20260528_RECEIPT_FULL_EXTRACTION_BOUNDARY

### Boundary update

Receipt full extraction belongs to deterministic business layer.

It is not owned by Telegram routing, Hermes auth, Telegram send delivery, or the agent personality layer.

### Business-layer owner boundary

Future receipt extraction work should inspect the deterministic receipt business/tool path first.

Likely source areas:

- `agent_lab/fin_instrument/**`;
- `vendor/hermes-agent/tools/fin_receipt_tool.py`;
- `tools/hermes_vendor_overlay/hermes-agent/tools/fin_receipt_tool.py`;
- receipt OCR/parser tests under `tests/`.

Responsibilities:

- image preprocessing;
- OCR invocation;
- OCR candidate normalization;
- merchant extraction;
- date/time extraction;
- total extraction;
- item row extraction;
- quantity/unit-price/line-total extraction;
- payment/tax facts if visible;
- `missing_fields` reporting;
- returning factual draft data to the agent.

### Agent/Hermes boundary

Hermes/agent responsibilities:

- receive compact factual tool result;
- ask user for confirmation or missing details;
- explain the result in character/style;
- never invent receipt facts.

Hermes/agent non-responsibilities:

- no direct SQL;
- no uncontrolled DB mutation;
- no invented totals/dates/items;
- no OCR correction by imagination;
- no replacing deterministic parser output with guessed data.

### Telegram boundary

Telegram routing and send path should be inspected only if fresh proof shows:

- receipt photo does not reach selected agent;
- `receipt_photo_draft` is not called;
- tool result is produced but not delivered;
- Telegram send fails after deterministic extraction succeeded.

Current proof does not make Telegram the first broken layer.

### Future technical boundary

The next technical run should target OCR/preprocessing/parser extraction.

It must not start by changing:

- Telegram Router;
- Hermes auth/provider;
- Telegram delivery/send;
- agent source package;
- unrelated YouTube pipeline;
- unrelated UI tabs.

### Acceptance boundary

A receipt extraction fix is incomplete if it only returns a final total.

The business layer must attempt full useful extraction and return `missing_fields` for fields it cannot honestly recover.
<!-- MODULE_MAP_APPEND_END id=MM_20260528_RECEIPT_FULL_EXTRACTION_BOUNDARY -->

<!-- MODULE_MAP_APPEND_BEGIN id=MM_20260529_YOUTUBE_RANKED_BATCH_ACTIVE_STATUS_CORRECTION source=chatgpt_dialogue_and_codex_reports -->
## MM_20260529_YOUTUBE_RANKED_BATCH_ACTIVE_STATUS_CORRECTION

### Boundary update

The current active block belongs to the YouTube research pipeline and its selection/moderation modules, not the Fin/receipt modules.

### Ownership

Owned by YouTube research pipeline / selection / moderation modules:

- candidate storage and ranking selection lifecycle;
- durable ranked batch state;
- current stack / next stack slicing;
- moderation-state transitions;
- structured no-eligible / empty-selection handling.

Telegram boundary:

- Telegram `Следующий стек` is an inline moderation control over an already-ranked batch;
- it must not own search, ranking, database state, or Curator selection logic;
- it is not a Telegram command in this correction state.

Not current active block from this correction:

- receipt / Fin Instrument module ownership;
- Telegram router/auth recovery;
- callback debugging.

### Acceptance boundary

The active/current module-map pointer must now describe the YouTube ranked batch lifecycle stop-point and leave the earlier receipt block as historical context only.
<!-- MODULE_MAP_APPEND_END id=MM_20260529_YOUTUBE_RANKED_BATCH_ACTIVE_STATUS_CORRECTION -->
END_MODULE_MAP_APPEND_TEXT
