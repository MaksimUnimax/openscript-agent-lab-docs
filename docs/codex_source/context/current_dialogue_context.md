# Current dialogue context

STATUS: INITIAL_FROM_CURRENT_REPO_DOCS

This file is append-only.

Do not rewrite historical blocks destructively.

<!-- CONTEXT_APPEND_BEGIN id=CTX_20260516_0001 source=chatgpt -->
Project memory / docs foundation created:
- `docs/codex_source/**` exists as the repo source-of-truth layer
- Hermes vendor docs have been extracted into `docs/codex_source/vendor/hermes/**`
- Telegram vendor docs have been extracted into `docs/codex_source/vendor/telegram/**`
- a project docs / memory layer is now being created

Current next step:
- import project docs, roadmap, rules, and module-map content into append-only files
- set up GitHub push visibility before resuming any further main ТЗ work

Known repo state:
- unrelated `agent-packages/**` dirty/untracked work exists and must not be staged
- the docs layer must stay separate from application code and vendor source
<!-- CONTEXT_APPEND_END id=CTX_20260516_0001 -->

<!-- CONTEXT_APPEND_BEGIN id=CTX_20260516_GITHUB_DOCS_VISIBILITY source=codex_sync -->
## 2026-05-16 — Public docs repo visibility verified

Facts:
- Private source repo was pushed successfully to `git@github.com:MaksimUnimax/openscript-agent-lab.git`.
- Public docs repo was created at `https://github.com/MaksimUnimax/openscript-agent-lab-docs`.
- Public docs export contains only `docs/codex_source/**`.
- ChatGPT verified public web access to `ENTRYPOINT_FOR_CHATGPT.md`.
- A stale HEAD reference in the entrypoint was detected and corrected by this run.

Next:
- Import real ТЗ, roadmap, rules, context/handoff, and module map into append-only project docs.
- Then continue main ТЗ work using repo entrypoint and exact docs paths.

<!-- CONTEXT_APPEND_END id=CTX_20260516_GITHUB_DOCS_VISIBILITY -->

<!-- CONTEXT_APPEND_BEGIN id=CTX_20260516_IMPORTED_WORKING_CONTEXT_V1 source=chatgpt_uploaded_context accepted_by_user=yes -->

## 2026-05-16 — Imported working context from uploaded ChatGPT handoff files

### 1. Why this context exists

This block imports the working project context from the user-provided ChatGPT handoff/context files into the repo-based project memory.

The purpose is not to rewrite the full history and not to replace roadmap/TZ/module-map imports. The purpose is to give future ChatGPT and Codex runs a stable continuation point, so they do not rely on assistant memory or old chat fragments.

This context was normalized from the uploaded files:
- `openscript_expense_bot_tz_v0_2(1).md`
- `openscript_agent_lab_dialogue_context_2026-05-07(1).md`
- `openscript_agent_lab_current_dialog_context_2026-05-12(1).md`
- `openscript_agent_lab_working_context_2026-05-14(1).md`
- `openscript_agent_lab_voice_stt_context_20260515(1).md`
- `current_dialogue_working_context_2026-05-16(4).md`

Full source import of ТЗ, roadmap, rules and module map is still a separate later step.

### 2. Product origin: “Расходы с характером”

The initial product idea was the first practical OpenScript project: a Telegram expense bot.

The user sends a receipt photo to Telegram. The bot extracts draft data such as date, merchant, total, items and category, asks for confirmation, then stores the confirmed expense in SQLite.

The user can later ask natural-language questions:
- “Сколько я потратил в мае?”
- “Что я покупал 22 мая?”
- “На что ушло больше всего денег?”
- “Покажи последние расходы”
- “Сколько я потратил на продукты?”

The bot must answer from deterministic data, but in a selected character/personality.

The first product was intended to show a beginner how Telegram input, photo/OCR, SQLite, AI-style text, business logic and deploy fit together.

### 3. Pivot: from isolated Expense Bot to OpenScript Agent Lab / Hermes-first

The work pivoted away from a single-purpose Telegram bot into OpenScript Agent Lab.

The canonical architecture became:

- Agent is a product entity.
- Agent has a source package.
- Agent has a separate Hermes runtime profile.
- Provider/model/auth are separate from the agent.
- Skills are instructions/requirements, not tool permissions.
- Business layer remains deterministic.
- Telegram Router is a product path, not a simulation-response diagnostic.
- Agent switching and provider switching are independent axes.
- The system must support arbitrary future agents, not a fixed set.

Old separate Expense Bot remains historical/reference only unless a separate extraction/refactor design says otherwise.

### 4. Core product boundaries

Deterministic business layer owns:
- SQL/database access;
- expense_add;
- expense_recent;
- expense_month_summary;
- receipt_photo_draft;
- receipt_manual_complete;
- cancel_pending;
- exact money/date/report calculations;
- persistence and confirmation rules.

Agent/LLM owns:
- language;
- character/personality;
- explanation;
- clarification questions;
- formatting;
- text understanding support where safe.

Agent/LLM must not:
- write SQL;
- read raw DB directly;
- mutate storage uncontrolled;
- confirm receipt without user confirmation;
- access secrets;
- execute shell from user text.

### 5. Agent Lab source/runtime split

Important paths:

Private source repo:
- `/opt/openscript-agent-lab`

Runtime:
- `/var/lib/openscript-agent-lab`

Logs:
- `/var/log/openscript-agent-lab`

Hermes runtime root:
- `/var/lib/openscript-agent-lab/hermes`

Hermes binary:
- `/opt/openscript-agent-lab/.venv-hermes/bin/hermes`

Agent source package:
- `/opt/openscript-agent-lab/agent-packages/<agent_slug>/`

Hermes runtime profile:
- `/var/lib/openscript-agent-lab/hermes/profiles/<agent_slug>/`

Canonical rule:
- source package is source-of-truth for agent docs/skills/config metadata;
- runtime profile is runtime state;
- runtime is not source-of-truth for project docs;
- project docs source-of-truth is now `docs/codex_source/**`.

### 6. LLM binding and provider model line

Important evolution:

- Agent Lab initially had provider/defaults and UI/API state that did not consistently drive execution.
- This was corrected toward `agent -> LLM connection` as the single source of truth.
- `provider.defaults.json` remains compatibility fallback only through the shared resolver.
- Codex CLI catalog/model selection needed proof and not hardcoded assumptions.
- Model selection must not be inferred from agent names.
- Direct config/default values must not override explicit agent binding.

Important rule:
- Agent Lab must never write `/root/.codex/auth.json`.

### 7. Telegram product line

The correct Telegram product mode is:

- disabled: worker does not run `getUpdates`;
- enabled: worker polls, routes updates, calls selected agent/business layer, sends response;
- paused: offset/state preserved, active processing paused.

The old manual one-shot UI path was rejected:
- “Проверить Telegram один раз” is not the product path.
- Telegram Router should not be simulation-response.
- User should not have to send a Telegram message and manually click a test button.

Canonical Telegram flow:
- Telegram update;
- normalize update;
- direct/router select agent;
- selected agent / Hermes / business layer;
- sendMessage response.

### 8. Voice/STT line

Voice work was developed proof-first.

Correct voice input architecture:

Telegram voice/audio
→ selected Telegram-bound agent
→ check per-agent voice gate
→ controlled getFile/download
→ controlled local STT
→ transcript object
→ transcript handoff to same text path
→ selected agent universal Hermes reply path
→ Telegram text send

Important decisions:
- voice setting is per Telegram-bound agent;
- default for future agents is voice disabled;
- no global voice switch;
- System Filter is not the owner of STT/transcription;
- tool binding is not the owner of Telegram voice setting;
- no hardcode for `/crabs`, `/squidward`, `/plankton`;
- voice after STT must go to the same selected-agent path as text.

Important proven pieces:
- local persistence for voice/audio metadata was added;
- internal raw `file_id` is retained privately;
- public reports mask file_id;
- controlled getFile/download proof succeeded;
- faster-whisper tiny/local STT was proven;
- `.oga -> .ogg` internal STT normalization fixed a real failure;
- transcript preview was redacted;
- transcript handoff gate was introduced;
- voice receive gate and transcript handoff gate were later unified in UI readiness.

### 9. Telegram voice final acceptance line

The final acceptance criterion for voice is:

User sends voice in Telegram
→ selected agent answers in Telegram text
→ report/state contains `telegram_message_id`.

Important final result from this dialogue:
- After Hermes/openai-codex auth was fixed via official import/adopt path, a fresh voice chain completed end-to-end in persisted runtime state.
- Proof included:
  - auth-check before voice was live_ok;
  - fresh_voice_seen=yes;
  - selected_agent_slug=runtime_apply_smoke_20260507;
  - voice_receive_enabled=true;
  - transcript_handoff_enabled=true;
  - internal_file_id_available=yes;
  - recognized=yes;
  - provider_call_success=yes;
  - answer_created=yes;
  - telegram_send_success=yes;
  - telegram_message_id=155.
- Delivery proof showed outbound send to the same inbound chat id; if user does not see it, the discrepancy is outside local server pipeline.

### 10. Plankton agent line

A new agent “Планктон” was created manually by the user through the UI using assistant-provided documents/skills.

Plankton intended character:
- original Russian-speaking small evil genius archetype;
- sarcastic, ambitious, suspicious, theatrical;
- useful for expense control;
- must not copy literal SpongeBob phrases;
- must preserve facts and deterministic business boundaries.

Plankton issues found:
1. UI refresh auto-selected the wrong agent.
2. Plankton showed `LLM: inherited`.
3. `/plankton + voice` did not reply.

Proof/fix found:
- route `/plankton` existed;
- Plankton runtime/profile/package existed;
- LLM inherited fallback resolved to openai-codex and was not the blocker;
- UI selection persistence root cause was router mode snapshot preferring `direct_agent_slug` over `router_active_agent_slug`;
- voice first blocker for Plankton was `telegram_transcript_handoff_enabled=false` while UI showed voice enabled.

Universal voice gate mismatch fix:
- before fix, UI checkbox read/wrote only `telegram_voice_enabled`;
- runtime needed both `telegram_voice_enabled` and `telegram_transcript_handoff_enabled`;
- fix made visible voice toggle update both gates together;
- badge now means effective voice readiness;
- partial states are labeled honestly;
- fix was universal for all Telegram-bound agents, not Plankton-specific.

### 11. Hermes/openai-codex auth line

Several false starts happened around auth.

Critical lessons:
- `metadata found` is not active auth.
- token shape is not active auth.
- auth file exists is not active auth.
- old runtime marker is not active auth.
- Codex CLI auth alone is not Hermes active.
- `401 token_invalidated` means not active.
- Live active means the same Hermes/openai-codex path used by live reply succeeds without 401.

Correct solution:
- Server-side device-code flow hit Cloudflare 403 and could not be browser-recovered automatically.
- Official Hermes import/adopt path exists:
  - read Codex CLI auth store;
  - import/adopt into Hermes-owned auth store;
  - save Hermes auth;
  - run live readiness probe.
- Correct path:
  `/root/.codex/auth.json`
  → official Hermes import/adopt
  → `/root/.hermes/auth.json`
  → same Hermes/openai-codex live readiness probe.
- After this, auth-recover returned imported_from_codex_cli=true and live_auth_ok=true.
- auth-check returned live_ok / “Авторизация активна”.

### 12. Documentation/source-of-truth process fix

The user repeatedly identified the main process failure:
- assistant hallucinated;
- assistant forgot context;
- assistant did not send required vendor documentation to Codex;
- assistant substituted roadmap/TZ for vendor docs;
- Codex then patched symptoms and produced “костыли”.

The chosen solution was not another assistant self-check rule.

The chosen solution:
- use GitHub/repo as a shared source-of-truth for assistant and Codex;
- create `docs/codex_source/**`;
- split vendor docs, project docs, task cards, templates, context, roadmap, module map and rules;
- Codex gets exact repo paths in prompts;
- assistant reads public docs repo entrypoint before future technical work;
- Codex appends context/roadmap/module_map only from assistant-provided append blocks;
- Codex must not rewrite or re-interpret large context files.

Completed docs/source work:
- `docs/codex_source/**` foundation created;
- Hermes vendor docs extracted;
- Telegram Bot API vendor docs extracted;
- project memory entrypoint and append-only files created;
- private repo pushed;
- public docs-only repo created;
- public docs repo contains only `docs/codex_source/**`;
- ChatGPT verified public web access to `ENTRYPOINT_FOR_CHATGPT.md`.

Public docs repo:
- `https://github.com/MaksimUnimax/openscript-agent-lab-docs`

Private source repo:
- `git@github.com:MaksimUnimax/openscript-agent-lab.git`

### 13. Current repo memory state

Current public docs memory already contains:
- `docs/codex_source/ENTRYPOINT_FOR_CHATGPT.md`
- `docs/codex_source/index.yaml`
- `docs/codex_source/vendor/hermes/**`
- `docs/codex_source/vendor/telegram/**`
- `docs/codex_source/context/current_dialogue_context.md`
- `docs/codex_source/context/context_manifest.yaml`
- `docs/codex_source/roadmap/roadmap.md`
- `docs/codex_source/roadmap/roadmap_manifest.yaml`
- `docs/codex_source/module_map/module_map.md`
- `docs/codex_source/module_map/module_map_manifest.yaml`
- `docs/codex_source/project_snapshot/PROJECT_SNAPSHOT.md`
- `docs/codex_source/rules/**`

But actual user-provided documents still need separate imports:
- current ТЗ;
- actual roadmap;
- latest rules pack;
- current/historical context;
- module map/safe boundaries;
- runtime-git canon;
- prompt templates.

This block is only the first normalized context import.

### 14. Rules for future assistant/Codex work

Future technical work must start by reading:
1. public docs repo entrypoint;
2. index;
3. current status;
4. manifests;
5. latest append blocks;
6. active task card;
7. exact vendor/project docs required by task card.

No future prompt should rely only on assistant memory.

Codex prompts must provide exact paths, not “go find docs”.

For vendor/runtime/API/auth/provider/CLI/Telegram/Hermes tasks:
- use vendor docs under `docs/codex_source/vendor/**`;
- do not use roadmap/context as vendor docs.

For project architecture tasks:
- use project docs under `docs/codex_source/project/**`;
- if still stub/missing, import project docs first.

For context/roadmap/module_map updates:
- assistant provides ready append block;
- Codex reads manifest + tail only;
- Codex appends exact block;
- Codex updates manifest/index;
- Codex commits and pushes;
- Codex refreshes public docs repo if needed.

### 15. Immediate next phase after this context import

Do not continue main ТЗ feature work yet.

Next imports should happen in order:
1. Import actual ТЗ into project docs.
2. Import actual roadmap into append-only roadmap/project roadmap docs.
3. Import actual rules pack into rules docs.
4. Import actual module map/safe boundaries into module_map/project docs.
5. Refresh project snapshot if necessary.
6. Only then return to main feature work, including Telegram user_id allowlist UI.

Telegram user_id allowlist remains intended, but must wait until required project docs are imported/non-stub.

<!-- CONTEXT_APPEND_END id=CTX_20260516_IMPORTED_WORKING_CONTEXT_V1 -->

<!-- CONTEXT_APPEND_BEGIN id=CTX_20260516_IMPORTED_TZ_V0_3 source=chatgpt_uploaded_tz accepted_by_user=yes -->

## 2026-05-16 — Imported current ТЗ v0.3 “OpenScript Agent Lab + Расходы с характером”

Facts:
- Imported the current working technical spec v0.3 from `Тз(2).md`.
- v0.3 supersedes the earlier v0.2 expense-bot-only draft as the current project technical spec.
- The project is OpenScript Agent Lab, not just a single Telegram expense bot.
- First applied scenario remains “Расходы с характером”.
- Key principle: universal agent creation + independent provider branch + deterministic business layer.
- Agent, provider, skills, business layer, management UI and Telegram Router are separate parts.
- Agent source package lives in `/opt/openscript-agent-lab/agent-packages/<agent_slug>/`.
- Hermes runtime profile lives in `/var/lib/openscript-agent-lab/hermes/profiles/<agent_slug>/`.
- Source package is git-tracked source-of-truth; runtime profile is runtime state and may contain secrets.
- No symlinks for `SOUL.md` or `config.yaml`.
- UI edits source package; `agentctl apply` syncs to runtime.
- Provider branches: `offline_template`, `codex_resource`, `api_runtime`.
- Provider branch is independent from agent.
- Business layer owns SQLite, money, date and report facts.
- Agent/Hermes owns language, character, explanation and safe text understanding.
- Telegram Router is not “now”; it comes after `agentctl`, provider/auth design, source packages, runtime apply and at least one provider proof.
- Voice canonical rule: voice → transcription → same text understanding layer as typed text.
- Hermes Dashboard must not be exposed as public product UI.
- Secrets must not be stored in git or shown in UI/logs.

Not imported in this run:
- actual roadmap
- full rules pack
- module map/safe boundaries as independent append-only module map
- prompt templates

Next:
- Import actual roadmap.
- Import rules pack.
- Import module map/safe boundaries.
- Then re-evaluate task cards before main feature work.

<!-- CONTEXT_APPEND_END id=CTX_20260516_IMPORTED_TZ_V0_3 -->

<!-- CONTEXT_APPEND_BEGIN id=CTX_20260516_IMPORTED_ROADMAP_V0_7 source=chatgpt_inline_roadmap accepted_by_user=yes -->

## 2026-05-16 — Imported actual roadmap v0.7

Facts:
- Actual roadmap v0.7 was provided inline to Codex by ChatGPT.
- v0.7 is the current roadmap state.
- v0.7 records final Telegram voice / universal Hermes path server-side success.
- Telegram voice proof includes recognized=yes, provider_call_success=yes, answer_created=yes, telegram_send_success=yes, telegram_message_id=155.
- Delivery to same inbound chat_id was proven.
- Auth/voice/send block is no longer the active blocker unless new proof shows a new issue.
- v0.6 remains useful for documentation-baseline/auth/process rules, but its active auth blocker is superseded by v0.7.
- v0.5 Slice B getFile/download gate is historical/superseded.
- v0.2 is historical product origin only.

Next:
- Import rules pack.
- Import module map/safe boundaries.
- Then re-evaluate task cards before main feature work.

<!-- CONTEXT_APPEND_END id=CTX_20260516_IMPORTED_ROADMAP_V0_7 -->

<!-- CONTEXT_APPEND_BEGIN id=CTX_20260516_IMPORTED_RULES_REPO_DOCS_ACCESS_V2 source=chatgpt_inline_rules accepted_by_user=yes -->

## 2026-05-16 — Imported rules update: repo documentation access model v2

Facts:
- The old general assumption that Codex lacks all documentation is no longer the normal workflow.
- Project documentation is now available to Codex in the private repo under `/opt/openscript-agent-lab/docs/codex_source/**`.
- Public documentation mirror is available to ChatGPT at `https://github.com/MaksimUnimax/openscript-agent-lab-docs`.
- Future Codex prompts must include exact `DOCS_TO_READ` paths.
- Codex must read only the listed docs unless a proof/inventory task explicitly permits broader reading.
- Every proof/design/fix must rely on relevant project/vendor/rules/task-card docs.
- If required docs are missing, stub, contradictory, or not listed, Codex must STOP instead of guessing.
- Uploaded ChatGPT file names may be provenance metadata only; content must be imported into repo docs or pasted inline before Codex can use it.
- Vendor/API/CLI/auth/runtime docs remain separate from project docs; roadmap/context cannot replace vendor docs.

Still pending:
- module map / safe boundaries import as independent module-map canon.
- task card readiness re-evaluation after module map import.

<!-- CONTEXT_APPEND_END id=CTX_20260516_IMPORTED_RULES_REPO_DOCS_ACCESS_V2 -->

<!-- CONTEXT_APPEND_BEGIN id=CTX_20260516_IMPORTED_MODULE_MAP_SNAPSHOT source=codex_repo_inventory accepted_by_user=yes -->

## 2026-05-16 — Imported module map / safe boundaries snapshot

Facts:
- No separate user-provided module map document existed.
- Codex generated a bounded current module map snapshot from repo inventory and imported project docs.
- The snapshot is docs-only and does not change application code.
- The module map records source/runtime/public/private boundaries.
- The module map records that `docs/codex_source/**` is the project documentation source-of-truth for ChatGPT/Codex.
- The public docs repo mirrors only `docs/codex_source/**`.
- `agent_lab/**` is application/backend/UI code and must not be touched in docs import runs.
- `agent-packages/**` are source packages for agents and must not be accidentally staged in unrelated runs.
- Hermes runtime under `/var/lib/openscript-agent-lab/hermes/**` is runtime state, not source-of-truth.
- Secrets/auth/runtime state must not go to git or public docs.
- Future feature/fix prompts must name affected modules and use module map/safe boundaries before changing code.

Next:
- Re-evaluate task cards using imported ТЗ v0.3, roadmap v0.7, rules pack and module map.
- Then decide whether Telegram user_id allowlist UI is ready for proof/design/fix.

<!-- CONTEXT_APPEND_END id=CTX_20260516_IMPORTED_MODULE_MAP_SNAPSHOT -->

<!-- CONTEXT_APPEND_BEGIN id=CTX_20260516_EXPAND_TZ_FIN_TOOL_TAB_AGENT_FARM_AND_AGENT_TOOLS source=chatgpt_inline_product_update accepted_by_user=yes -->

## 2026-05-16 — Product direction expanded: “Фин инструмент”, Agent Farm and Agent Tools

Facts:
- The user clarified that the financial tool should not be a separate new tab.
- The current UI tab named “Телеграмм” is already specialized for the financial agent with Telegram and voice.
- This tab should be renamed/treated as “Фин инструмент”.
- Telegram user_id allowlist/access control belongs in the “Фин инструмент” tab.
- Future financial tool work also belongs in the “Фин инструмент” product surface.
- First, close access to the Telegram bot through user_id allowlist/access control.
- Then build a universal agent farm where many agents can live, receive tasks, run with their own instructions/tools, and have execution monitored.
- The next major tool after access control should be the Financial Agent Business Tool.
- The financial tool is not just a database. It is database + scripts + receipt reading/ingestion + reports + safe contracts.
- Financial agents must call scripts/tools; they must not write SQL or mutate the DB directly.
- Planned future tool families also include Telegram post publishing and YouTube parsing.
- Several other future tasks remain unspecified and must stay placeholders until the user defines them.
- This update is documentation only. No implementation was requested.

Next:
- Still re-evaluate `telegram_user_id_allowlist_ui` task card.
- The re-evaluation must include placement in the “Фин инструмент” tab.
- After access control, design/proof Agent Farm / Task Runtime.
- After that, design/proof Financial Agent Business Tool.

<!-- CONTEXT_APPEND_END id=CTX_20260516_EXPAND_TZ_FIN_TOOL_TAB_AGENT_FARM_AND_AGENT_TOOLS -->

<!-- CONTEXT_APPEND_BEGIN id=CTX_20260517_FILLED_TELEGRAM_ACCESS_CONTROL_STUB_DOCS source=codex_docs_update accepted_by_user=yes -->

## 2026-05-17 — Filled Telegram identity/privacy/access-control STUB docs

Facts:
- The previous task-card re-evaluation for `telegram_user_id_allowlist_ui` stopped because required Telegram identity/privacy and project access-control docs were STUB.
- This run filled the STUB docs needed to unblock the next task-card re-evaluation.
- The contract is: allowlist identity is Telegram `from.id` / `user_id`, not `chat.id`.
- `chat.id` remains delivery / conversation target for replies.
- Telegram privacy mode is not sufficient access control.
- Unknown users must be denied before voice download/STT, provider/model/Hermes calls, tool execution or other resource-spending operations.
- Allowlist controls belong in the “Фин инструмент” UI surface.
- This run is docs-only and does not implement allowlist.

Next:
- Re-run task-card re-evaluation for `telegram_user_id_allowlist_ui`.
- Do not start implementation until the task card is promoted beyond proof/design readiness.

<!-- CONTEXT_APPEND_END id=CTX_20260517_FILLED_TELEGRAM_ACCESS_CONTROL_STUB_DOCS -->

<!-- CONTEXT_APPEND_BEGIN id=CTX_20260517_WORKFLOW_RULES_RISK_BASED_COMBINED_RUNS source=chatgpt_inline_user_clarification accepted_by_user=yes -->

## 2026-05-17 — Workflow rules updated: risk-based combined runs

Facts:
- The user clarified that the old mandatory separate design-run before almost every fix is no longer efficient.
- That rule was created when models were weaker and both ChatGPT and Codex needed to separately inspect most designs.
- Current observed workflow: most Codex designs are accepted, so mandatory separate design runs create too many prompts and circular work.
- New priority rule: use risk-based workflow.
- Narrow ordinary fixes may use `combined_proof_design_fix`: proof -> design summary -> minimal fix -> tests/checks -> git push -> report in one run.
- Codex may edit in a combined run only if docs gate passes, exact affected modules are found, scope matches allowed scope, and no high-risk/unclear condition appears.
- If combined-run guard fails, Codex must STOP before editing.
- Separate design approval remains mandatory for high-risk/unclear tasks: auth, secrets, provider, Telegram delivery/send, systemd/nginx/deploy, runtime storage migrations, DB schema, paid-resource paths, large UI refactors, new architecture such as Agent Farm/task runtime, external APIs like YouTube/Twitch, broad multi-module changes, or docs/code contradictions.
- Docs/import/task-card re-evaluation runs remain docs-only.

<!-- CONTEXT_APPEND_END id=CTX_20260517_WORKFLOW_RULES_RISK_BASED_COMBINED_RUNS -->

<!-- CONTEXT_APPEND_BEGIN id=CTX_20260517_DEMOTED_TASK_CARDS_FROM_BLOCKING_GATE source=chatgpt_inline_user_clarification accepted_by_user=yes -->

## 2026-05-17 — Task cards demoted from blocking gate

Facts:
- The user rejected the remaining task-card permission gate as unnecessary overhead.
- The previous combined allowlist run stopped only because `telegram_user_id_allowlist_ui.yaml` still had `ready_for_fix_run: false`, despite required docs being filled.
- This showed that task cards had become an outdated blocking layer.
- New rule: task cards remain useful as summaries/checklists, but they are not the primary permission gate.
- The primary gate is now docs gate + combined-run guard + exact affected modules + allowed scope + tests/checks.
- A stale task-card readiness flag must not force a separate run just to flip metadata.
- If a task card contradicts current docs in a safety-relevant way, Codex must report/STOP.
- If a task card only has stale readiness metadata, Codex may update/report it and continue if combined guard passes.

Next:
- Re-run Telegram user_id allowlist as guarded combined proof/design/fix.
- Do not let stale task-card `ready_for_fix_run: false` block the run by itself.

<!-- CONTEXT_APPEND_END id=CTX_20260517_DEMOTED_TASK_CARDS_FROM_BLOCKING_GATE -->

<!-- CONTEXT_APPEND_BEGIN id=CTX_20260517_TELEGRAM_USER_ID_ALLOWLIST_FIN_TOOL_IMPLEMENTED_AFTER_GATE_DEMOTION source=codex_combined_fix accepted_by_user=yes -->

## 2026-05-17 — Implemented Telegram user_id allowlist for “Фин инструмент” after task-card gate demotion

Facts:
- Telegram bot access control by Telegram `from.id` / `user_id` was implemented.
- `chat.id` remains delivery/conversation target and is not allowlist identity.
- Unknown users are denied before resource use, including covered voice/download/STT/provider/model/Hermes/tool/agent handoff paths.
- Allowlist configuration lives in the current Telegram/“Фин инструмент” UI surface.
- The implementation is universal for Telegram-bound agents using the shared path and does not hardcode a specific agent or user in source code.
- Tests were added/updated for allowed and denied users.

<!-- CONTEXT_APPEND_END id=CTX_20260517_TELEGRAM_USER_ID_ALLOWLIST_FIN_TOOL_IMPLEMENTED_AFTER_GATE_DEMOTION -->

<!-- CONTEXT_APPEND_BEGIN id=CTX_20260517_FIN_TOOL_LABEL_AND_TELEGRAM_NO_REPLY_FIXED source=codex_combined_fix accepted_by_user=yes -->

## 2026-05-17 — Fixed “Фин инструмент” label and Telegram no-reply after allowlist

Facts:
- The visible Telegram UI tab/section was updated to “Фин инструмент”.
- The user had already configured Telegram user_id `286579139` as allowed, and the live runtime state now reads that allowlist correctly.
- I did not hardcode `286579139` in source code; it was used only as runtime/manual proof input.
- The live UI service was restarted so the current bundle and runtime process are active.
- The narrow regression fix added normalization coverage so string and integer `user_id` values both match inbound `from.id`.
- Allowlist identity remains Telegram `from.id` / `user_id`; `chat_id` remains delivery target only.
- Unknown users remain denied before resource use.
- Tests were updated and passed for the fixed path.
- Controlled manual Telegram proof is still required after the fix.

<!-- CONTEXT_APPEND_END id=CTX_20260517_FIN_TOOL_LABEL_AND_TELEGRAM_NO_REPLY_FIXED -->

<!-- CONTEXT_APPEND_BEGIN id=CTX_20260517_TELEGRAM_POLLING_STAGE_INSTRUMENTED_OR_FIXED source=codex_live_polling_stage_fix accepted_by_user=yes -->

## 2026-05-17 — Telegram polling stage instrumentation added; reply-path blocker diagnosed

Facts:
- Safe runtime-stage diagnostics were added to the canonical Telegram polling path.
- `/api/telegram/status` now exposes `runtime_loop` and `polling_cycle` stage fields without leaking secrets.
- Live proof on the canonical service shows the polling loop is active and holding `polling.lock` from PID `313491`.
- The current live cycle stage is `before_reply`, meaning Telegram updates are being consumed and the blocker is downstream of inbound polling.
- The last completed cycle failed with `reply_failed` and the live runtime error `Hermes runtime did not return a reply`.
- This narrows the remaining blocker to the reply/Hermes path rather than allowlist, webhook, or inbound update ingestion.
- No token/auth/webhook/send-delivery rewrite was performed in this run.
- Manual allowed-user Telegram proof is still required after any follow-up reply-path fix.

<!-- CONTEXT_APPEND_END id=CTX_20260517_TELEGRAM_POLLING_STAGE_INSTRUMENTED_OR_FIXED -->

<!-- CONTEXT_APPEND_BEGIN id=CTX_20260517_HERMES_PRE_REPLY_AUTH_GATE_IMPLEMENTED source=codex_auth_readiness_gate_fix accepted_by_user=yes -->

## 2026-05-17 — Hermes pre-reply auth readiness gate implemented

Facts:
- Telegram input, polling and allowlist were already working, but Hermes/provider auth degradation could still produce a silent Telegram no-reply.
- The root cause had been narrowed to missing Hermes profile auth for the active agent while Codex CLI auth was available and recoverable through the existing UI flow.
- A pre-reply readiness gate is now implemented so the Telegram reply path does not call Hermes blindly when auth/provider readiness is false.
- Auth-not-ready and empty-Hermes-reply states now produce safe explicit status/reason instead of silent no-reply.
- The existing Codex-CLI recovery/check authorization flow remains intact and is still the approved way to restore Hermes readiness.
- No provider credentials, Hermes auth store, Codex auth, or Telegram token were changed.

Manual proof still required:
- with auth ready, allowed Telegram user_id `286579139` should receive replies;
- if auth degrades again, Telegram/user/operator should see an explicit safe auth-not-ready signal instead of silence.

<!-- CONTEXT_APPEND_END id=CTX_20260517_HERMES_PRE_REPLY_AUTH_GATE_IMPLEMENTED -->

<!-- CONTEXT_APPEND_BEGIN id=CTX_20260517_FIN_INSTRUMENT_FIRST_FINANCIAL_TOOL_DESIGN_PROPOSED source=codex_proof_design accepted_by_user=pending -->

## 2026-05-17 — Priority correction: finish Fin Instrument / Financial Tool before Agent Farm

Facts:
- The user corrected the direction after the assistant proposed moving directly to Agent Farm / Task Runtime.
- Current priority is to finish the financial agent / “Фин инструмент” first.
- For the current stage, financial runtime/settings/status live inside the “Фин инструмент” tab.
- The future architecture question remains open: common runtime for all agents, per-tool runtime tabs, or hybrid.
- Agent Farm is deferred until after the Fin Instrument / Financial Tool line is reviewed and progressed.
- Financial Tool is a business tool package for financial agents, not just a raw database.
- Agents must not write SQL directly or mutate storage uncontrolled; deterministic scripts own reads/writes/calculations.
- This run created docs-only design and did not implement application code.

Next:
- review the Fin Instrument / Financial Tool design docs;
- then choose the first minimal implementation slice inside “Фин инструмент”;
- do not implement Agent Farm until the Fin Instrument priority is accepted/progressed.

<!-- CONTEXT_APPEND_END id=CTX_20260517_FIN_INSTRUMENT_FIRST_FINANCIAL_TOOL_DESIGN_PROPOSED -->

<!-- CONTEXT_APPEND_BEGIN id=CTX_20260517_FIN_INSTRUMENT_TOOL_CONTRACTS_SKELETON_IMPLEMENTED source=codex_combined_fix accepted_by_user=yes -->

## 2026-05-17 — Fin Instrument financial tool contracts skeleton implemented

Facts:
- The first implementation slice for the Financial Tool was added inside the Fin Instrument line.
- This slice created source-owned financial tool contracts and deterministic no-op/skeleton handlers.
- No SQLite schema, migration, runtime storage write, Telegram integration, voice integration, UI integration or Agent Farm implementation was added.
- Tool contracts now exist for `expense_add`, `expense_recent`, `expense_month_summary`, `receipt_photo_draft`, `receipt_manual_complete`, `cancel_pending`, and `tool_status`.
- The skeleton enforces the rule that agents must not write SQL directly and that financial writes will later be owned by deterministic scripts/storage.
- Tests cover JSON-serializable responses, validation, storage-not-initialized behavior, and no runtime file writes.
- Next slice should be reviewed separately: SQLite schema design or runtime storage initializer, not both blindly.

<!-- CONTEXT_APPEND_END id=CTX_20260517_FIN_INSTRUMENT_TOOL_CONTRACTS_SKELETON_IMPLEMENTED -->

<!-- CONTEXT_APPEND_BEGIN id=CTX_20260517_FIN_INSTRUMENT_SQLITE_SCHEMA_DESIGN_PROPOSED source=codex_proof_design accepted_by_user=pending -->

## 2026-05-17 — Fin Instrument SQLite schema design proposed

Facts:
- The Financial Tool contracts skeleton exists and remains source-only.
- No DB or runtime storage has been created yet.
- A SQLite schema for the Fin Instrument runtime has now been proposed under `/var/lib/openscript-agent-lab/fin-instrument/`.
- The schema design covers expenses, receipt drafts, categories, payment sources, operation/audit logs and versioning.
- Agents still must not write SQL directly; deterministic scripts/storage functions will own all reads and writes.
- This was docs-only design and does not create a database or migration file.
- The next step is user/ChatGPT review and then a minimal runtime storage initializer proof/design or a source SQL migration skeleton.

<!-- CONTEXT_APPEND_END id=CTX_20260517_FIN_INSTRUMENT_SQLITE_SCHEMA_DESIGN_PROPOSED -->

<!-- CONTEXT_APPEND_BEGIN id=CTX_20260517_FIN_INSTRUMENT_RUNTIME_STORAGE_INITIALIZER_DESIGN_PROPOSED source=codex_proof_design accepted_by_user=pending -->

## 2026-05-17 — Fin Instrument runtime storage initializer design proposed

Facts:
- The Financial Tool contracts skeleton exists.
- SQLite schema design exists.
- No DB or runtime storage has been created yet.
- A runtime storage initializer for the Fin Instrument runtime has now been proposed under `/var/lib/openscript-agent-lab/fin-instrument/finance.sqlite3`.
- The initializer design covers runtime root creation, SQLite bootstrap, schema versioning, migration tracking, readiness states, permissions, failure modes and tests.
- This was docs-only design and does not create a database, runtime directory, migration files or application code.
- Agents still must not write SQL directly; deterministic scripts/storage functions will own all reads and writes.
- The next step is user/ChatGPT review and then a minimal implementation slice for the initializer using temp-dir tests and no production auto-init.

<!-- CONTEXT_APPEND_END id=CTX_20260517_FIN_INSTRUMENT_RUNTIME_STORAGE_INITIALIZER_DESIGN_PROPOSED -->

<!-- CONTEXT_APPEND_BEGIN id=CTX_20260517_FIN_INSTRUMENT_RUNTIME_STORAGE_INITIALIZER_IMPLEMENTED source=codex_combined_fix accepted_by_user=yes -->

## 2026-05-17 — Fin Instrument runtime storage initializer implemented

Facts:
- The Fin Instrument runtime storage initializer was implemented as source code with temp-dir tests.
- The implementation can create and validate a SQLite database using the designed schema when explicitly called with a configured root.
- Production runtime storage `/var/lib/openscript-agent-lab/fin-instrument/` was not created in this run.
- The initializer is not wired into UI, Telegram, service startup or Agent Farm.
- The initializer is idempotent and records schema version and migration state.
- Financial handlers still must not write expenses until deterministic storage scripts are implemented in a later slice.
- Tests prove temp-dir initialization, idempotence, required tables, no float money columns and no production runtime writes.

<!-- CONTEXT_APPEND_END id=CTX_20260517_FIN_INSTRUMENT_RUNTIME_STORAGE_INITIALIZER_IMPLEMENTED -->

<!-- CONTEXT_APPEND_BEGIN id=CTX_20260517_FIN_INSTRUMENT_DETERMINISTIC_STORAGE_SCRIPTS_IMPLEMENTED source=codex_combined_fix accepted_by_user=yes -->

## 2026-05-17 — Fin Instrument deterministic storage scripts implemented

Facts:
- Deterministic storage functions were implemented for the Fin Instrument financial tool layer.
- The storage layer uses the existing runtime storage initializer and SQLite schema when explicitly called with a configured root.
- `expense_add`, `expense_recent`, and `expense_month_summary` can now operate against initialized temp/runtime storage through deterministic code.
- Production runtime storage `/var/lib/openscript-agent-lab/fin-instrument/` was not created in this run.
- UI, Telegram, voice, Agent Farm and old expense-bot integration were not added.
- Financial writes are still owned by deterministic storage functions; agents do not write SQL directly.
- Tests cover add/recent/month summary, integer money, audit/operation rows, validation and no production runtime writes.

<!-- CONTEXT_APPEND_END id=CTX_20260517_FIN_INSTRUMENT_DETERMINISTIC_STORAGE_SCRIPTS_IMPLEMENTED -->

<!-- CONTEXT_APPEND_BEGIN id=CTX_20260517_FIN_INSTRUMENT_UI_READINESS_SURFACE_IMPLEMENTED source=codex_combined_fix accepted_by_user=yes -->

## 2026-05-17 — Fin Instrument UI read-only readiness surface implemented

Facts:
- A read-only readiness/status surface was added for the Fin Instrument.
- The UI can now show financial storage and tool readiness inside the “Фин инструмент” tab.
- The status surface reports whether the Fin Instrument runtime root and SQLite DB exist, schema readiness, tool readiness and the next required operator action.
- This run did not create production runtime storage or `finance.sqlite3`.
- This run did not add a DB init action, expense write UI, Telegram/voice integration, Agent Farm or old expense-bot import.
- The next slice should be a controlled runtime initialization operator action, still separate from Telegram/voice expense entry.

<!-- CONTEXT_APPEND_END id=CTX_20260517_FIN_INSTRUMENT_UI_READINESS_SURFACE_IMPLEMENTED -->

<!-- CONTEXT_APPEND_BEGIN id=CTX_20260517_FIN_INSTRUMENT_CONTROLLED_RUNTIME_INIT_ACTION_IMPLEMENTED source=codex_combined_fix accepted_by_user=yes -->

## 2026-05-17 — Fin Instrument controlled runtime initialization action implemented

Facts:
- A controlled operator action was added for Fin Instrument runtime storage initialization.
- The action creates the shared Fin Instrument SQLite storage only after explicit typed confirmation.
- The shared DB is for all financial agents and must be accessed only through Fin Instrument tools/storage, not direct agent SQL.
- Read-only status remains safe and does not create runtime storage.
- Production runtime storage was created live through the controlled admin endpoint in this run.
- Telegram/voice expense entry, expense write UI, Agent Farm and old expense-bot import were not added.
- The next slice should be a read-only expense view or a later Telegram/voice design slice, not another uncontrolled init path.

<!-- CONTEXT_APPEND_END id=CTX_20260517_FIN_INSTRUMENT_CONTROLLED_RUNTIME_INIT_ACTION_IMPLEMENTED -->

<!-- CONTEXT_APPEND_BEGIN id=CTX_20260517_FIN_INSTRUMENT_READ_ONLY_EXPENSE_VIEW_IMPLEMENTED source=codex_combined_fix accepted_by_user=yes -->

## 2026-05-17 — Fin Instrument read-only expense view implemented

Facts:
- The Fin Instrument UI/backend now shows read-only recent expenses and current-month summary from the shared SQLite database.
- The shared Fin Instrument runtime DB remains the single database for all financial agents and is accessed only through the Fin Instrument tools/storage layer.
- The read-only view handles empty state safely and does not add any expense write controls.
- No Telegram, voice, Agent Farm, or new security middleware was added in this slice.
- The next slice should move to controlled manual expense add UI or a later Telegram/voice design slice, not a DB/security rewrite.

<!-- CONTEXT_APPEND_END id=CTX_20260517_FIN_INSTRUMENT_READ_ONLY_EXPENSE_VIEW_IMPLEMENTED -->

<!-- CONTEXT_APPEND_BEGIN id=CTX_20260517_FIN_INSTRUMENT_TELEGRAM_CONTROLS_RESTORED source=codex_combined_fix accepted_by_user=yes -->

## 2026-05-17 — Telegram controls restored inside Fin Instrument tab

Facts:
- The Fin Instrument tab now shows the existing Telegram bot controls/status again instead of hiding them behind the legacy wrapper.
- The same tab still contains the financial storage/read-only blocks: “Финансовое хранилище”, “Последние расходы”, and “Сводка за месяц”.
- Telegram access control remains user_id/from.id based and lives in the same tab.
- The internal compatibility slug `telegram` remains unchanged; only the visible product label is “Фин инструмент”.
- This run did not add Telegram-to-expense integration, voice runtime enablement, expense write UI, Agent Farm, or new security middleware.

<!-- CONTEXT_APPEND_END id=CTX_20260517_FIN_INSTRUMENT_TELEGRAM_CONTROLS_RESTORED -->

<!-- CONTEXT_APPEND_BEGIN id=CTX_20260517_FIN_INSTRUMENT_AGENT_VOICE_CHECKBOXES_RESTORED source=codex_combined_fix accepted_by_user=yes -->

## 2026-05-17 — Per-agent voice checkboxes restored inside Fin Instrument tab

Facts:
- The “Голос для Telegram-агентов” section again renders per-agent Telegram voice checkboxes.
- The setting remains Telegram-owned per-agent config and uses `telegram_agent_settings[agent_slug].telegram_voice_enabled`.
- Future non-system agents appear automatically with the voice checkbox defaulting to false when no config exists yet.
- Restoring the checkbox list does not enable STT/TTS runtime, does not call Telegram API, and does not connect voice to financial tools.
- The same “Фин инструмент” tab still contains the Telegram controls/status and the financial storage/read-only blocks.

<!-- CONTEXT_APPEND_END id=CTX_20260517_FIN_INSTRUMENT_AGENT_VOICE_CHECKBOXES_RESTORED -->

<!-- CONTEXT_APPEND_BEGIN id=CTX_20260517_UI_ONLY_ROLLBACK_TO_WORKING_TELEGRAM_BASELINE source=codex_combined_fix accepted_by_user=yes -->

## 2026-05-17 — UI-only rollback to working Telegram baseline

Facts:
- The user requested an emergency UI-only rollback to the last working Telegram tab baseline before the Telegram interface was hidden/removed.
- The frontend was rolled back to the working Telegram-only tab baseline and the visible financial blocks were removed from the tab for this run.
- The production Fin Instrument runtime storage, schema, initializer and backend endpoints remain preserved and were not mutated by this rollback.
- No Telegram API calls, model calls, auth/provider changes, new security middleware, or Agent Farm changes were added.
- Financial UI re-add is deferred until after the user manually verifies the restored Telegram-only tab.

<!-- CONTEXT_APPEND_END id=CTX_20260517_UI_ONLY_ROLLBACK_TO_WORKING_TELEGRAM_BASELINE -->
