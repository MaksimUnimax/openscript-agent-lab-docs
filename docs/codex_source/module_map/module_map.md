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
