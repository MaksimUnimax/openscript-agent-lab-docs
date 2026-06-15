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

<!-- CONTEXT_APPEND_BEGIN id=CTX_20260517_UI_ROLLBACK_AND_TELEGRAM_NO_REPLY_CURRENT_STOPPOINT source=chatgpt_inline_current_dialogue accepted_by_user=yes -->
2026-05-17 — UI rollback completed; Telegram no-reply unresolved; last diagnostic prompt not sent
1. Current situation

The project is still OpenScript Agent Lab.

The immediate active incident is no longer Fin Instrument feature work.

Current emergency state:

UI was rolled back to the last working Telegram UI baseline before Telegram UI was removed/hidden.
User must verify old Telegram/voice UI manually.
After rollback, user reported that the Telegram bot does not answer.
A proof run incorrectly stopped earlier because it did not see a fresh update.
User then clarified that he had already sent the Telegram message кто ты.
The next correct action is to diagnose the already-sent message кто ты, not ask the user for another fresh message.
2. Important user correction

The user explicitly corrected the intended rollback target.

Wrong target:

commit f12467d911c7e5df5321a150ad8eb94e60eed374f35b as “clean Fin Instrument UI”.
That state was not accepted as the rollback target because it was after Telegram UI removal/hiding.

Correct target:

last working Telegram UI before Telegram UI removal/hiding.
This was identified as:
9dd3685e1225b436d707c30111f592ff29f14336

The user also explicitly required:

first restore old Telegram UI only;
no Fin Instrument UI addition during rollback;
user manually checks old forms first;
only after user confirms old Telegram/voice forms work may Fin Instrument UI be re-added in a separate run.
3. UI-only rollback run

Run:

OPENSCRIPT_AGENT_LAB_UI_ONLY_ROLLBACK_TO_WORKING_TELEGRAM_TAB_20260517_01

Result:

SUCCESS

Private commit:

b38a8bd35095dc0cf7117227215bd483fd2f3df1
message: Restore working Telegram UI baseline

Public docs commit:

1d1b578

Selected baseline:

9dd3685e1225b436d707c30111f592ff29f14336

Reason selected:

Telegram-only UI with:
Telegram-бот
Доступ к боту
Бот-роутер
allowlist controls
voice settings
without finance UI blocks.

What rollback changed:

restored agent_lab/static/index.html from selected baseline;
restored agent_lab/static/app.js from selected baseline;
updated tests/docs;
did not add Fin Instrument UI.

Final UI after rollback:

contains Telegram bot controls;
contains access control;
contains bot router;
contains voice settings if baseline had them;
does not contain financial storage;
does not contain recent expenses;
does not contain month summary;
duplicate IDs check passed.

Important:

financial backend/storage/runtime DB were preserved;
production DB was preserved;
Telegram backend was not changed;
no Telegram API calls;
no model calls;
no auth/provider changes;
no security middleware.

Checks passed:

compileall;
admin_server tests;
telegram_connector tests;
telegram_polling tests;
telegram_voice_transport tests;
fin contracts tests;
fin initializer tests;
fin storage tests;
duplicate_ids_ok;
service active;
healthz 200.
4. Current Fin Instrument backend state after UI rollback

UI rollback did not remove backend financial work.

Preserved backend/storage:

Fin Instrument contracts;
storage initializer;
deterministic storage scripts;
production runtime/DB;
read-only endpoints.

Previously completed financial backend work:

agent_lab/fin_instrument/schema.py
agent_lab/fin_instrument/storage_initializer.py
agent_lab/fin_instrument/storage.py
expense_add
expense_recent
expense_month_summary
production DB:
/var/lib/openscript-agent-lab/fin-instrument/finance.sqlite3

But after UI rollback:

Fin Instrument UI is intentionally absent.
Financial UI re-add is deferred until after user confirms Telegram/voice forms work.
5. Bad UI branch superseded

Two previous UI runs are superseded for UI behavior:

OPENSCRIPT_AGENT_LAB_FIN_INSTRUMENT_RESTORE_TELEGRAM_CONTROLS_20260517_01
commit: 1dafe2926030fcb253434a93c6f3a94a9edb6f97
problem: restored Telegram controls by un-hiding legacy UI container, which was not the desired recovery strategy.
OPENSCRIPT_AGENT_LAB_FIN_INSTRUMENT_RESTORE_AGENT_VOICE_CHECKBOXES_20260517_01
commit: e4da01c4cf37ac7660d98f17c7872a0aeb986eab
problem: continued fixing voice checkboxes on top of the wrong legacy restore path.

These runs should not be used as the future UI target.

6. Telegram no-reply after rollback

After UI-only rollback, the user reported:

bot does not answer in Telegram.

A proof run was attempted:

Run:

OPENSCRIPT_AGENT_LAB_TELEGRAM_NO_REPLY_AFTER_UI_ROLLBACK_20260517_01

Result:

STOP

Important report facts:

source head before:
b38a8bd35095dc0cf7117227215bd483fd2f3df1
service active: yes
healthz: 200
bot username: FinancAgent_bot
webhook URL empty: yes
pending_update_count: 0
live poller running: yes
last_seen_update_id == last_processed_update_id == 255681829
getUpdates from a second client returned HTTP 409 Conflict because live poller owns the long-poll session
allowlist was configured for expected user_id 286579139
selected agent from state: squidward
no files changed
no commit
no source changes

STOP reason:

Codex said no fresh Telegram update was available to exercise the reply path.

User correction after this STOP:

the user had already written кто ты in Telegram.
the next prompt must diagnose this existing message, not ask the user for another fresh message.
7. Relevant earlier same-day breakage patterns

The next diagnosis must not ignore prior same-day Telegram incidents.

Earlier today similar breakages included:

Telegram API could see updates, but local polling state did not consume them.
Polling stage instrumentation showed cycles reaching before_reply.
A failure mode existed where reply path reached Hermes but Hermes returned no reply:
Hermes runtime did not return a reply
There was a stale/manual UI process problem:
live Telegram polling was running in stale manual UI process, not canonical systemd service.
After stopping stale process / restoring canonical service ownership, updates could be consumed and replies sent.
There was also a send confirmation/state issue where telegram_message_id needed to be captured before commit_state().

Therefore the next run must verify:

current source still contains backend stage telemetry/fixes;
live server process is canonical systemd service;
no stale manual process owns polling/runtime;
message кто ты appears in logs/state or was consumed;
allowlist/router/Hermes/send chain stage;
whether Hermes/auth/provider is currently failing again.
8. Current correct stop-point

Current stop-point:

UI-only rollback is done.
Do not add Fin Instrument UI yet.
Do not do manual expense UI.
Do not do Telegram/voice → financial tool integration yet.
First restore Telegram bot reply behavior.

Next exact action:

run the unsent diagnostic prompt below:
OPENSCRIPT_AGENT_LAB_TELEGRAM_NO_REPLY_EXISTING_KTO_TY_AFTER_UI_ROLLBACK_20260517_01
9. Unsent next prompt to preserve

The following prompt was prepared by ChatGPT but user did not send it yet. It must be preserved so the next dialogue/run can continue exactly from this state.

UNSENT_NEXT_PROMPT_BEGIN

Сделай TELEGRAM BOT NO REPLY FOR EXISTING MESSAGE "КТО ТЫ" ROOT CAUSE/FIX RUN:
OPENSCRIPT_AGENT_LAB_TELEGRAM_NO_REPLY_EXISTING_KTO_TY_AFTER_UI_ROLLBACK_20260517_01.

RUN_MODE:

combined_proof_design_fix

Тип run:

live Telegram no-reply proof/fix.
Проверить уже отправленное пользователем сообщение "кто ты".
НЕ просить пользователя снова отправлять сообщение, пока не доказано, что это сообщение отсутствует в Telegram/local state.
Minimal fix only if exact root cause is proven.
НЕ UI work.
НЕ Fin Instrument UI.
НЕ security/auth middleware.
НЕ Agent Farm.
НЕ broad refactor.
НЕ provider change.
НЕ fallback.
НЕ direct manual Telegram send в обход нормального bot reply path.

Пользователь уже отправил в Telegram:

text: кто ты
expected user_id: 286579139
bot: FinancAgent_bot

Проблема:
После UI-only rollback к working Telegram baseline бот не отвечает в Telegram.
Нельзя снова отвечать "нет fresh update", не проверив конкретно сообщение "кто ты" в:

Telegram pending/consumed updates;
local polling state;
runtime status stage telemetry;
journal logs;
persisted polling state;
reply/Hermes/send status.

Контекст сегодняшних уже известных похожих поломок:

Ранее Telegram API видел updates, а local polling state не двигался.
Затем stage instrumentation доказал, что canonical loop consuming updates and reaching before_reply, but reply failed with:
"Hermes runtime did not return a reply".
Ранее уже была поломка stale/manual process: live Telegram polling ran in stale manual UI process, not canonical systemd service; после остановки stale process canonical service consumed updates and sent reply.
Ранее send confirmation тоже был отдельным исправлением: telegram_message_id должен сохраняться в last_send до commit_state().
Нельзя откатываться до состояния, где эти backend fixes/stage instrumentation потеряны.
UI rollback должен был быть UI-only, но надо проверить, что backend fixes still present in current HEAD and live service process actually runs this HEAD.

Последний UI rollback:

RUN_ID: OPENSCRIPT_AGENT_LAB_UI_ONLY_ROLLBACK_TO_WORKING_TELEGRAM_TAB_20260517_01
RESULT: SUCCESS
current commit after rollback:
b38a8bd35095dc0cf7117227215bd483fd2f3df1
selected UI baseline:
9dd3685e1225b436d707c30111f592ff29f14336
rollback changed static UI/tests/docs only according to report.
But now bot does not answer, so verify live runtime, process, config and reply path.

SOURCE PRIVATE REPO:

/opt/openscript-agent-lab

EXPECTED CURRENT HEAD:

b38a8bd35095dc0cf7117227215bd483fd2f3df1
If HEAD differs but contains b38a8bd35095dc0cf7117227215bd483fd2f3df1 as ancestor, continue and report.
If HEAD does not contain it, STOP.

PRECHECK:
cd /opt/openscript-agent-lab

Run:
git rev-parse HEAD
git log --oneline -20
git status --short
git status -sb
git fetch origin main
git rev-parse HEAD
git rev-parse origin/main

Requirements:

origin/main must equal HEAD before edits.
If origin/main != HEAD, STOP.
Do not stage runtime/db/config/auth files.
Pre-existing dirty agent-packages/** must remain untouched.

BACKEND FIX PRESENCE CHECK:
Before live diagnosis, prove whether today’s known backend fixes/stage telemetry still exist in current source.

Run targeted checks:
git log --oneline -- agent_lab/telegram_polling.py agent_lab/telegram_runtime.py agent_lab/agent_reply.py | head -40

grep -R "current_cycle_stage|last_cycle_reason|last_cycle_error|before_reply|reply_failed|last_fetch_update_ids_preview|lock_holder_pid" -n agent_lab/telegram_polling.py agent_lab/telegram_runtime.py agent_lab/admin_server.py || true
grep -R "telegram_message_id|last_send|commit_state" -n agent_lab/telegram_polling.py agent_lab/telegram_connector.py || true
grep -R "Hermes runtime did not return a reply|response_text_length|auth_configured|token_invalidated" -n agent_lab/agent_reply.py agent_lab/hermes_binding.py agent_lab/admin_server.py || true

Report:

stage_telemetry_present: yes/no
send_confirmation_fix_present: yes/no
hermes_empty_reply_detection_present: yes/no
current source contains today’s reply-path diagnostics: yes/no

DOCS_TO_READ EXACTLY:

docs/codex_source/ENTRYPOINT_FOR_CHATGPT.md
docs/codex_source/index.yaml
docs/codex_source/project/current_status.md
docs/codex_source/project/telegram_router.md
docs/codex_source/project/access_control.md
docs/codex_source/project/telegram_voice_pipeline.md
docs/codex_source/project/source_vs_runtime.md
docs/codex_source/project/runtime_git_canon.md
docs/codex_source/rules/workflow_run_modes.md
docs/codex_source/rules/codex_prompt_rules.md
docs/codex_source/rules/documentation_gate_rules.md
docs/codex_source/rules/repo_documentation_access_rules.md
docs/codex_source/rules/runtime_git_rules.md
docs/codex_source/context/context_manifest.yaml
docs/codex_source/context/current_dialogue_context.md
read_policy: tail/latest relevant append only

CODE_TO_READ EXACTLY:

agent_lab/admin_server.py
read_policy: targeted Telegram/status/Hermes auth status sections only
agent_lab/telegram_connector.py
read_policy: targeted config/allowlist/router/send/state sections only
agent_lab/telegram_runtime.py
read_policy: targeted runtime/status/thread/stage telemetry sections only
agent_lab/telegram_polling.py
read_policy: targeted polling cycle/update/allowlist/reply/send/stage telemetry sections only
agent_lab/agent_reply.py
read_policy: targeted selected-agent reply/Hermes invocation sections only
agent_lab/hermes_binding.py
read_policy: targeted Hermes readiness/invocation sections only
tests/test_telegram_connector.py
tests/test_telegram_polling.py
tests/test_admin_server.py
tests/test_telegram_voice_transport.py

DO NOT READ:

Do not read auth files directly.
Do not read /root/.codex/auth.json.
Do not read /root/.hermes/auth.json.
Do not print secrets/tokens.
Do not modify UI/static files in this run.
Do not modify Fin Instrument files.
Do not touch agent-packages/**.
Do not add security middleware.
Do not change provider.
Do not add fallback.
Do not manually send Telegram message except through the normal bot reply path.

LIVE PROOF REQUIRED:

Service/process proof:
Run:
systemctl is-active openscript-agent-lab-ui.service || true
systemctl show openscript-agent-lab-ui.service -p MainPID -p ExecStart -p WorkingDirectory --no-pager || true
ps -ef | grep -E "openscript|agent_lab|uvicorn|python|app/main.py" | grep -v grep || true
ss -ltnp | grep -E "18765|180|agent|python|uvicorn" || true
curl -sS -o /tmp/agent_lab_healthz_kto_ty.out -w '%{http_code}\\n' http://127.0.0.1:18765/healthz || true
cat /tmp/agent_lab_healthz_kto_ty.out || true

Must report:

canonical systemd MainPID
any extra/stale manual UI process
who listens on port 18765
whether live server process is the canonical systemd service

If stale/manual competing process exists:

classify possible stale process issue.
Do not kill blindly unless process owner/path proves it is old manual UI process conflicting with canonical service.
If proven stale process blocks polling or owns lock, stop only that stale process or restart canonical service as minimal runtime action; report exact command and proof.
Local status proof:
Run:
curl -sS http://127.0.0.1:18765/api/state 2>/dev/null > /tmp/agent_lab_state_kto_ty.json || true
curl -sS http://127.0.0.1:18765/api/telegram/status 2>/dev/null > /tmp/agent_lab_telegram_status_kto_ty.json || true

Print redacted safe summary only:

bot mode
selected/direct agent
router mode
allowlist enabled
whether 286579139 is allowed
polling_allowed
thread_running
processing_busy
last_seen_update_id
last_processed_update_id
current_cycle_stage
last_cycle_reason
last_cycle_error
last_fetch_update_count
last_fetch_update_ids_preview
last_router_stage
lock_holder_pid
last reply/send status if present
Hermes/auth status if API exposes safe status

Do not print tokens/secrets.

Search current logs for the exact message:
Run:
journalctl -u openscript-agent-lab-ui.service -n 500 --no-pager > /tmp/agent_lab_journal_kto_ty.txt || true

Search safely:
grep -i -C 5 "кто ты" /tmp/agent_lab_journal_kto_ty.txt || true
grep -E -i -C 3 "255681|before_reply|reply_failed|Hermes runtime did not return a reply|send|sendMessage|telegram_message_id|allowlist|denied|selected_agent|router|processing_busy|timeout|exception|traceback|token_invalidated|401|auth" /tmp/agent_lab_journal_kto_ty.txt || true

Report whether "кто ты" appears in logs.

Persisted Telegram state proof:
Find only known safe state files, do not print secrets:
/var/lib/openscript-agent-lab/telegram/polling_state.json if exists
any app state JSON path already used by project docs/code

Print redacted summary only:

last_seen_update_id
last_processed_update_id
last_message text preview if available
last_message from_id
last_message chat_id
last_message update_id
last_error
last_send status/message_id if available
current stage fields if persisted

Do not print raw token/file_id/secrets.

Telegram API proof:
Because live poller owns long-poll, do NOT repeat direct getUpdates unless needed.
Allowed:
getMe
getWebhookInfo
Report:
bot username
webhook empty yes/no
pending_update_count
last_error redacted

If pending_update_count=0 and local state/logs show update consumed, continue chain proof from local state.
If pending_update_count>0 and local state not consuming, classify polling issue.

Chain proof for message "кто ты":
Determine exact path:

A. MESSAGE_NOT_VISIBLE_ANYWHERE

"кто ты" not in logs/state and Telegram pending_update_count=0.
This means live poller may have consumed it but logging/state lacks text, or message was before current log window.
Then use last_seen/processed/stage to determine if no-reply happened after consumption.
Do not ask user for another message until checking stage telemetry and last errors.

B. POLLING_CONSUMED_BUT_REPLY_FAILED

local state/logs/stage show update consumed, current/last cycle before_reply/reply_failed/Hermes empty.

C. POLLING_STUCK_OR_STALE_PROCESS

fresh/pending update visible but local last_seen/processed does not move OR lock holder/stale process owns polling.

D. ALLOWLIST_DENIED

update from 286579139 reached gate but denied.

E. ROUTER_NO_AGENT_SELECTED

update passed allowlist but no selected agent.

F. HERMES_AUTH_OR_EMPTY_REPLY

reply reached Hermes; no response text; auth_configured false/token_invalidated/401 or response empty.

G. SEND_FAILED

reply created, send reached, Telegram send failed.

H. BOT_REPLIED_SUCCESSFULLY

send_result ok and telegram_message_id present.

I. UNKNOWN_NOT_PROVEN

only if evidence insufficient after all checks.

COMBINED FIX GUARD:
Proceed to edit or runtime action only if:

exact class is proven;
exact owner is proven;
minimal fix is safe.

Allowed minimal runtime action if proven:

restart canonical service if live service is stale or processing_busy stuck.
stop stale manual process if proven non-canonical and conflicting.
do not commit for runtime-only restart.

Allowed minimal code fix if proven:

only in exact owner files:
telegram_runtime.py
telegram_polling.py
telegram_connector.py
agent_reply.py
hermes_binding.py
tests matching changed owner
no UI/static changes.

Specific handling:

If F = Hermes auth/token_invalidated:
do not patch around auth.
report that user must use existing UI “Модель и авторизация” → “Войти заново”.
if existing auth recover endpoint/UI exists, verify status only.
no provider change, no fallback.
If F = Hermes empty reply but auth active:
use today’s previous diagnostics and exact response_text_length=0 proof.
fix only if exact reason in agent_reply/Hermes invocation is proven.
If C = stale process:
fix runtime process, verify canonical service consumes next update.
no code changes unless source bug caused duplicate process.
If D:
preserve user_id/from.id identity.
do not change to chat_id.

TESTS IF CODE CHANGED:
python3 -m compileall agent_lab tests
python3 -m unittest tests.test_admin_server -v
python3 -m unittest tests.test_telegram_connector -v
python3 -m unittest tests.test_telegram_polling -v
python3 -m unittest tests.test_telegram_voice_transport -v

SERVICE IF CODE CHANGED OR RUNTIME ACTION:
systemctl restart openscript-agent-lab-ui.service
systemctl is-active openscript-agent-lab-ui.service || true
curl -sS -o /tmp/agent_lab_healthz_kto_ty_after.out -w '%{http_code}\\n' http://127.0.0.1:18765/healthz || true
cat /tmp/agent_lab_healthz_kto_ty_after.out || true

DOCS UPDATE:
If root cause/fix is proven, append context.

Update:

docs/codex_source/project/current_status.md
docs/codex_source/context/current_dialogue_context.md
docs/codex_source/context/context_manifest.yaml
docs/codex_source/index.yaml

Append context:

<!-- CONTEXT_APPEND_BEGIN id=CTX_20260517_TELEGRAM_NO_REPLY_KTO_TY_AFTER_UI_ROLLBACK_DIAGNOSED source=codex_proof_fix accepted_by_user=yes -->
2026-05-17 — Telegram no-reply for existing “кто ты” after UI rollback diagnosed

Facts:

After UI-only rollback to the working Telegram baseline, the user sent кто ты in Telegram and reported no bot reply.
Codex diagnosed the existing message instead of asking for another fresh message.
The proof checked canonical service process, stale/manual process risk, polling state, stage telemetry, allowlist, router, Hermes reply and Telegram send path.
The root cause classification and any minimal fix/runtime action are recorded in the run report.
No Fin Instrument UI, financial integration, Agent Farm or security middleware was added in this run.
<!-- CONTEXT_APPEND_END id=CTX_20260517_TELEGRAM_NO_REPLY_KTO_TY_AFTER_UI_ROLLBACK_DIAGNOSED -->

CHECKS:
Run:
git diff --check -- docs/codex_source
git status --short

GIT:
If code/docs changed:

Stage only intended files.
Do not stage agent-packages/**.
Do not stage runtime/db/config/auth files.
Commit message:
Diagnose Telegram no-reply after UI rollback
Push private origin main.
Verify origin/main == HEAD.

If no source changes:

Do not create empty commit.
Report no source changes.

PUBLIC DOCS REFRESH:
If docs/codex_source/** changed:

refresh public docs repo and verify it contains only docs/codex_source/**.

REPORT:
Print final report between CHATGPT_REPORT_BEGIN and CHATGPT_REPORT_END.
Save report through codex_report_inbox.py only if current reporting path is available.

CHATGPT_REPORT_BEGIN

RUN_ID: OPENSCRIPT_AGENT_LAB_TELEGRAM_NO_REPLY_EXISTING_KTO_TY_AFTER_UI_ROLLBACK_20260517_01

RESULT:

SUCCESS / STOP / FAIL

BASELINE:

source_repo:
source_branch:
source_head_before:
private_origin_main_before:
public_docs_head_before:
working_tree_status:

DOCS:

docs_to_read_provided:
docs_read:
docs_missing:
docs_stub:
docs_contradictions:
documentation_gate_passed:

CONTEXT_APPEND:

append_added:
append_id:
append_duplicate_found:
append_target:
unsent_next_prompt_preserved:
unsent_next_prompt_run_id:
file_download_created: no

DOCS_UPDATED:

context_manifest:
current_status:
task_card:
import_queue:
index_updated:

CHECKS:

git_diff_check_docs_only:
required_files_check:
yaml_check:
source_change_guard:
context_append_unique:

PRIVATE_SOURCE_GIT:

commit:
head_after:
push_success:
origin_main_equals_head:
no_source_changes:

PUBLIC_DOCS_REFRESH:

public_remote:
export_dir:
public_commit:
public_push_success:
public_head_after:
contains_only_docs_codex_source:
context_append_exists_public:

FILES_CHANGED:

...

SECURITY:

secrets_printed: no
tokens_printed: no
auth_files_read: no
model_calls_run: report actual
telegram_api_calls_run: report actual safe calls
services_restarted: no

NEXT_STEP:

Run preserved prompt OPENSCRIPT_AGENT_LAB_TELEGRAM_NO_REPLY_EXISTING_KTO_TY_AFTER_UI_ROLLBACK_20260517_01.
Do not resume Fin Instrument UI work until Telegram reply is restored.

CHATGPT_REPORT_END

UNSENT_NEXT_PROMPT_END

10. Next exact step after this docs context append

After this docs-only context append is committed and public docs are refreshed:

Send the preserved diagnostic prompt:
OPENSCRIPT_AGENT_LAB_TELEGRAM_NO_REPLY_EXISTING_KTO_TY_AFTER_UI_ROLLBACK_20260517_01
Do not resume Fin Instrument UI work.
Do not add financial UI blocks back into the tab.
Do not ask the user to send another message until the already-sent кто ты has been checked in logs/state/runtime.
<!-- CONTEXT_APPEND_END id=CTX_20260517_UI_ROLLBACK_AND_TELEGRAM_NO_REPLY_CURRENT_STOPPOINT -->

<!-- CONTEXT_APPEND_BEGIN id=CTX_20260517_FIN_PRODUCT_SCHEMA_V2_SUCCESS source=chatgpt -->
## 2026-05-17 — Fin Instrument schema v2 / product-field success

Facts:
- Run `OPENSCRIPT_AGENT_LAB_FIN_EXPENSE_PRODUCT_FIELD_SCHEMA_UI_FIX_20260517_01` completed SUCCESS.
- Private commit `f0235cbeed7f27392c5d3bcca88a44c6315654dd` was pushed to `origin/main`.
- Fin expense schema is now v2.
- `expense_records` now has a dedicated `product` column.
- `product` / `Товар` is required and stored separately from `description`.
- `category` is optional and defaults to `Без категории` / `bez_kategorii`.
- `description` is now optional comment text.
- Legacy description-only add payloads are rejected safely.
- Live controlled POST `amount=12, product=хлеб, currency=RUB, payment_source=card` returned 200.
- `/api/state` now shows `product=хлеб` and `category=Без категории`.
- Tests passed: 143.
- Service was active and healthz returned 200.
- Telegram UI/auth/provider paths were left untouched.

Next:
- Any follow-up feature work must be separate and must not touch Telegram/Hermes without proof.
<!-- CONTEXT_APPEND_END id=CTX_20260517_FIN_PRODUCT_SCHEMA_V2_SUCCESS -->

<!-- CONTEXT_APPEND_BEGIN id=CTX_20260519_CONTEXT_TOOLS_VOICE_PENDING_PROMPT_V1 source=chatgpt_inline_current_dialogue accepted_by_user=yes -->
## 2026-05-19 — Current dialogue context: CONTEXT, TOOLS, and pending universal VOICE tool/capability prompt
### 1. Main tasks that must be repeated until solved
The user explicitly required that these tasks be repeated in every relevant working answer until they are solved:
1. CONTEXT:
   - The next Telegram turn must see the full receipt context:
     - receipt_draft;
     - receipt_item_lines;
     - last action/result;
     - prior assistant reply.
   - The next turn must not see only the total amount.
   - If the bot showed a receipt with item rows, the following turn must be able to use those item rows.
2. TOOLS:
   - Telegram live agent must be Hermes tool-capable:
     - Fin tools are available to the agent;
     - agent/model semantically chooses the needed tool;
     - tool reads/writes DB;
     - tool result returns to the agent/model;
     - final answer is based on tool result.
   - This must not be implemented through keyword matchers, phrase routers, prompt-memory workarounds, or direct LLM DB writes.
3. VOICE:
   - Voice must be a universal Hermes tool/capability, not a separate business-logic branch.
   - Voice must be:
     Telegram voice/audio -> STT transcript -> same canonical text/Hermes agent/tool loop.
   - Voice must not own Fin business logic.
   - Voice must not own confirmation logic.
   - Voice must not own receipt logic.
   - Voice must not own DB write logic.
### 2. Why this context append is needed
The user clarified that the previous Codex prompt for the VOICE task was not sent/executed and must be saved in repo-based context, using the correct context append prompt format.
This append stores:
- the current accepted task framing;
- the proven status of CONTEXT and TOOLS;
- the fact that VOICE still needs a universal tool/capability implementation;
- the full pending Codex prompt that should be used next when the user asks to proceed.
### 3. Proven CONTEXT status
A proof/design/fix and finalize sequence was completed for receipt context hydration.
Important run:
- OPENSCRIPT_AGENT_LAB_FIX_RECEIPT_CONTEXT_HYDRATION_NEXT_TURN_20260519_01
Finalize run:
- OPENSCRIPT_AGENT_LAB_FINALIZE_RECEIPT_CONTEXT_HYDRATION_COMMIT_RESTART_20260519_01
Reported final facts:
- context fix committed: 8cdba40 (Hydrate receipt context for next turns)
- pushed to origin/main
- service restarted
- healthz ok
- final repo clean
What became live:
- Next Telegram turns now carry receipt_context with:
  - receipt_draft
  - receipt_item_lines
  - last_action_result
  - prior_assistant_reply
- Hermes prompt serialization includes that receipt context block.
- The context fix was explicitly not the tools implementation.
CONTEXT is considered source/runtime live-ready by the report, but future live failures must still be proven from runtime before new fixes.
### 4. Proven TOOLS status
A canonical proof showed the old broken state:
- Telegram live fallback used prompt/session-resume only.
- agent_reply.py / hermes_execution.py launched the live subprocess with enabled_toolsets=[].
- Fin receipt operations were app-local handlers, not Hermes-visible tools.
- Therefore the live Telegram agent could not call Fin tools.
Then a tool-loop implementation was reported:
- commit: fb6f892569dc78db5d24bc8541d297fc9ab22556
- message: Add Hermes receipt tool loop
Reported changes:
- Telegram live reply forwards enabled Fin toolset into Hermes instead of hardcoding enabled_toolsets=[].
- Hermes smoke execution instantiates AIAgent with those toolsets.
- Added Hermes-visible fin.receipt toolset with:
  - receipt_current
  - receipt_items
  - receipt_confirm
  - last_receipt
- Tools are wired to existing Fin handlers and deterministic confirm/write path.
- Fin storage read shape fixed so last_receipt can rehydrate linked receipt items.
- Service restarted.
- healthz 200.
- HEAD == origin/main.
- working tree clean.
Verification run:
- OPENSCRIPT_AGENT_LAB_VERIFY_HERMES_RECEIPT_TOOL_LOOP_LIVE_20260519_01
Reported verification:
- current_head: fb6f892569dc78db5d24bc8541d297fc9ab22556
- service_loaded_commit: fb6f892569dc78db5d24bc8541d297fc9ab22556
- context_status: preserved and proven in source/tests
- fin_receipt_tool_registration: registered and discoverable via Hermes registry
- telegram_enabled_toolsets_actual: non-empty for the Fin-capable Telegram path; includes fin.receipt
- AIAgent receives enabled_toolsets from payload
- receipt_current dispatch works in test fixture
- receipt_items dispatch works in test fixture
- receipt_confirm uses deterministic confirm/write and only temp test DB
- tool result return path proven by registry dispatch plus Hermes role: tool message append back into the loop
- no provider/model calls by Codex
- no Telegram API calls by Codex
- no production side effects
TOOLS is considered implemented and verified by source/runtime/tests, but a full manual live dialogue with provider/model tool calls still requires observation if failures continue.
### 5. New live VOICE problem after tool setup
After tools were configured, the user reported that voice stopped answering.
A proof-only voice root-cause run found:
- live voice update was seen;
- polling active;
- service active and healthz 200;
- voice gate passed;
- STT/download/transcript path succeeded;
- transcript reached the model request;
- reply died at the provider request validation step;
- sendMessage was not attempted;
- first failing step: MODEL_REQUEST_REJECTED_INVALID_TOOL_NAME.
Important live failure:
- provider request included tool name: fin.expense_add
- provider rejected it because the endpoint only accepts tool names matching:
  ^[a-zA-Z0-9_-]+$
- root cause classification:
  provider request rejected due invalid tool name serialization.
This matters because:
- voice was not dead at polling/STT level;
- voice reached the model/tool path;
- the failure exposed that legacy voice/tool serialization is still not aligned with the provider-safe Hermes tool contract.
### 6. User correction about VOICE architecture
The user clarified:
- voice is a tool/capability.
- voice must not be a separate костыльная branch.
- voice must be configured universally, not under one agent.
- voice must not be hardcoded to plankton or any other specific agent.
- voice must use the same selected_agent/capability/toolset configuration as text.
- voice must become:
  audio -> transcript -> canonical text/Hermes agent/tool loop.
Important accepted wording:
- Voice = transport/capability.
- Voice should not own business logic.
- After transcript, voice must enter the same canonical path as text.
- Any fix must be universal for all agents and future tools.
### 7. Universal requirement for the next VOICE prompt
The next implementation must be generic for all agents and future tools.
Do not hardcode:
- plankton;
- any specific agent_slug;
- any specific chat_id/user_id;
- a one-off Fin-only voice path;
- a one-off receipt-only voice path;
- a one-off confirmation phrase path;
- a one-off Telegram-only business branch.
Use existing generic configuration:
- selected_agent;
- agent capability settings;
- agent tool allowlist;
- resolved enabled_toolsets for that selected agent;
- shared voice/STT capability settings;
- shared canonical text -> Hermes agent path.
Tests must prove:
- voice transcript enters the same canonical path as text;
- voice path carries the same enabled_toolsets as text for the same Fin-capable agent;
- voice path can access fin.receipt tools through provider-safe names;
- provider request does not contain invalid dot-named tool names;
- provider-safe tool call maps back to the correct internal handler;
- non-Fin agent does not receive fin.receipt tools by accident;
- no agent slug is hardcoded;
- no chat/user id is hardcoded;
- voice branch no longer owns confirmation/receipt business logic;
- context hydration remains intact;
- Fin receipt tool loop remains intact.
### 8. Pending next Codex prompt to run when user asks to proceed
The following prompt was prepared in the current ChatGPT dialogue but not yet sent/executed. Save it as pending next prompt context.
PENDING_CODEX_PROMPT_BEGIN
RUN_ID:
OPENSCRIPT_AGENT_LAB_VOICE_AS_UNIVERSAL_HERMES_TOOL_CAPABILITY_20260519_01
RUN_MODE:
proof_design_fix_universal_voice_tool_capability
Follow AGENTS.md.
MAIN_TASKS_TO_SOLVE:
1. CONTEXT:
Next Telegram turn must see full receipt context:
receipt_draft + receipt_item_lines + last action/result + prior assistant reply.
Not only total.
Context hydration is already live-ready and must remain intact.
2. TOOLS:
Telegram live agent must be Hermes tool-capable:
Fin tools available to the selected agent -> model chooses tool -> tool reads/writes DB -> tool result returns to model.
Hermes receipt tool loop is already implemented and must remain intact.
3. VOICE:
Voice must be a universal Hermes tool/capability, not a separate business-logic branch.
Voice must be:
Telegram voice/audio
-> STT transcript
-> same canonical text/Hermes agent/tool path as normal text.
UNIVERSALITY REQUIREMENT:
This implementation must be generic for all agents and future tools.
Do not hardcode:
- plankton;
- any specific agent slug;
- any specific chat_id/user_id;
- a one-off Fin-only voice path;
- a one-off receipt-only voice path;
- a one-off confirmation phrase path;
- a one-off Telegram-only business branch.
Use existing generic configuration:
- selected_agent;
- agent capability settings;
- agent tool allowlist;
- resolved enabled_toolsets for that selected agent;
- shared voice/STT capability settings;
- shared canonical text -> Hermes agent path.
Voice is a transport/capability.
Voice must not own Fin business logic.
Voice must not own confirmation logic.
Voice must not own receipt logic.
Voice must not own DB write logic.
After STT, voice transcript must enter the same path as text.
TASK:
Refactor/repair the live Telegram voice path so voice is treated as a universal Hermes tool/capability feeding the same canonical agent/tool loop as text.
This run must not create another agent-specific workaround.
This run must not create another phrase matcher.
This run must not create another receipt-specific voice branch.
BASELINE:
Context hydration is live-ready:
- receipt_draft + receipt_item_lines + last_action_result + prior_assistant_reply are carried into next-turn context.
Hermes receipt tools are live-ready:
- Telegram Fin-capable path includes non-empty enabled_toolsets.
- fin.receipt is Hermes-visible.
- receipt_current, receipt_items, receipt_confirm, last_receipt are registered and dispatch in tests.
- Service loaded commit fb6f892569dc78db5d24bc8541d297fc9ab22556.
Latest live voice proof showed:
- voice update was seen;
- voice gate passed;
- STT/download/transcript produced text;
- transcript reached the model request;
- failure happened at provider request validation because a dot-named tool was serialized as fin.expense_add.
This means voice is not dead.
Voice is entangled with the tool path, but the implementation still has legacy voice_branch behavior and invalid provider tool-name serialization.
SYMPTOM:
Live voice messages do not reliably produce normal agent replies through the same tool-capable path as text.
SUSPECTED HIGHER-LEVEL CAUSE:
The current voice implementation still contains legacy branch-specific routing and does not cleanly use the universal Hermes tool/capability contract.
Possible failure classes:
- VOICE_STILL_HAS_BUSINESS_LOGIC_BRANCH
- VOICE_NOT_MODELED_AS_UNIVERSAL_CAPABILITY
- VOICE_TRANSCRIPT_NOT_HANDOFF_TO_CANONICAL_TEXT_AGENT_PATH
- VOICE_PATH_USES_DIFFERENT_ENABLED_TOOLSETS_THAN_TEXT
- VOICE_PATH_SERIALIZES_INVALID_TOOL_NAMES
- TOOL_NAME_CANONICALIZATION_MISSING
- INTERNAL_TOOL_ID_NOT_MAPPED_BACK_FROM_PROVIDER_SAFE_NAME
- TOOL_RESULT_NOT_RETURNED_TO_AGENT_LOOP
- OLD_VOICE_DRY_RUN_PATH_STILL_CONTROLS_REPLY
- AGENT_SLUG_HARDCODE
- NON_UNIVERSAL_FIX_ATTEMPT
- UNKNOWN_STOP
PROVE:
Before changing code, prove:
1. Current voice path:
   - where voice/audio is normalized;
   - where voice gate/dry_run/voice_branch controls routing;
   - where STT transcript is produced;
   - where transcript is handed to reply generation;
   - where old voice-specific business logic still exists.
2. Current text canonical path:
   - where normal text enters Telegram routing;
   - where context envelope is built;
   - where selected_agent is resolved;
   - where enabled_toolsets are resolved;
   - where agent_reply invokes Hermes;
   - where tool results return.
3. Voice vs text comparison:
   - same selected_agent?
   - same conversation key?
   - same context hydration?
   - same enabled_toolsets?
   - same provider-safe tool name mapping?
   - same tool result loop?
   - same reply sending path?
4. Tool name problem:
   - where internal tool ids such as fin.expense_add / fin.receipt are serialized into provider request;
   - whether provider accepts dots in tool names;
   - where provider-safe names must be generated;
   - how provider-safe names map back to internal tool ids;
   - whether this mapping is generic for all tools, not only Fin.
5. Universal configuration:
   - where selected_agent tool allowlist lives;
   - how enabled_toolsets are resolved per agent;
   - how to ensure Fin tools are only enabled for agents that have them;
   - how to ensure non-Fin agents do not receive Fin tools accidentally.
NOT A SOLUTION:
- no agent-specific hardcode;
- no plankton-only logic;
- no chat/user hardcode;
- no new keyword matcher;
- no receipt/OCR/item parser changes;
- no Fin DB schema changes;
- no UI/static changes;
- no prompt-memory workaround;
- no separate voice confirmation logic;
- no direct LLM DB writes;
- no provider/model calls in tests;
- no Telegram API calls in tests;
- no production expense creation by Codex;
- no broad unrelated refactor.
TASK-SPECIFIC DOCS:
Read only these exact docs/source because this task depends on Hermes tools and voice capability.
Hermes tools:
- docs/codex_source/vendor/hermes/tools/tools_runtime.md
- docs/codex_source/vendor/hermes/tools/tool_gateway.md
- docs/codex_source/vendor/hermes/runtime/api_server.md
- vendor/hermes-agent/tools/registry.py
- vendor/hermes-agent/model_tools.py
- vendor/hermes-agent/gateway/platforms/api_server.py
Voice / Telegram source owners:
- agent_lab/telegram_connector.py
- agent_lab/telegram_polling.py
- agent_lab/telegram_voice_transport.py
- agent_lab/agent_reply.py
- agent_lab/hermes_execution.py
- agent_lab/hermes_binding.py
- agent_lab/storage.py
- agent_lab/tool_registry.py
Existing tool source owners:
- vendor/hermes-agent/tools/fin_receipt_tool.py
- vendor/hermes-agent/tools/fin_expense_add_tool.py
- agent_lab/fin_instrument/receipt_hermes_adapter.py
Do not read current_dialogue_context.md.
Do not read current_status.md.
Do not read module_map.md.
Do not scan docs broadly.
If a listed file directly references another exact voice/tool runtime file required for implementation, read only that file and report why.
ALLOWED_SCOPE:
- universal voice tool/capability wrapper;
- Telegram voice transcript handoff;
- voice path routing into canonical text/Hermes agent path;
- enabled_toolsets parity between text and voice;
- provider-safe tool name serialization;
- internal tool id mapping back from provider-safe names;
- tests for voice -> transcript -> canonical agent path;
- tests for provider-safe tool names;
- tests proving Fin tools remain available on voice path when selected_agent has them;
- tests proving Fin tools are not available to an agent without that allowlist.
FORBIDDEN_TASK_SPECIFIC_SCOPE:
- AGENTS.md;
- ChatGPT workflow rules docs;
- OCR parser/item parser;
- Fin DB schema migration;
- UI/static files;
- broad Hermes vendor rewrite;
- Telegram tokens/config secrets;
- real Telegram API calls;
- real provider/model calls in tests;
- production expense creation by Codex;
- hardcoded selected agent;
- hardcoded plankton;
- hardcoded chat/user;
- one-off receipt-only solution.
PLAN:
1. Map current voice path:
   Telegram voice/audio
   -> normalize_update
   -> voice gate
   -> STT/download
   -> transcript
   -> routing
   -> reply/model request.
2. Map canonical text path:
   Telegram text
   -> selected_agent
   -> context envelope
   -> agent_reply
   -> Hermes enabled_toolsets
   -> tool-capable response path.
3. Compare voice vs text:
   - same selected_agent;
   - same context hydration;
   - same enabled_toolsets;
   - same tool name serialization;
   - same tool result loop;
   - same final reply path.
4. Implement universal voice capability behavior:
   - voice/STT layer only materializes transcript and safe metadata;
   - after transcript, route into the same canonical text/Hermes agent path;
   - keep voice gate only for transport readiness/safety;
   - remove or neutralize old voice-specific business decision points;
   - do not let voice branch decide Fin intent;
   - do not let voice branch decide receipt confirmation.
5. Implement provider-safe tool name mapping if required:
   - internal tool ids may stay dot-named internally;
   - provider request must use safe names matching ^[a-zA-Z0-9_-]+$;
   - map provider-safe names back to internal tool ids on tool call execution;
   - make mapping generic for all tools, not Fin-only;
   - preserve Hermes registry semantics internally.
6. Preserve agent-specific tool allowlists:
   - selected_agent drives enabled_toolsets;
   - Fin tools only appear for agents that have Fin toolsets enabled;
   - voice path and text path use the same allowlist resolver.
7. Add tests:
   - voice transcript enters the same canonical path as text;
   - voice path carries the same enabled_toolsets as text for the same Fin-capable agent;
   - voice path can access fin.receipt tools through provider-safe names;
   - provider request does not contain invalid dot-named tool names;
   - provider-safe tool call maps back to correct internal handler;
   - non-Fin agent does not receive fin.receipt tools by accident;
   - implementation does not hardcode plankton;
   - implementation does not hardcode chat/user id;
   - voice branch no longer owns confirmation/receipt business logic;
   - context hydration remains intact;
   - no provider/model calls;
   - no Telegram API calls;
   - no production DB writes.
8. Commit and push.
9. Restart service if runtime Python changed, then healthz.
TARGETED_CHECKS:
Run focused tests for:
- tests.test_telegram_connector
- tests.test_telegram_polling
- tests.test_telegram_voice_transport
- tests.test_agent_reply
- tests.test_hermes_execution
- tests.test_fin_receipt_hermes_tools
- tool registry / Hermes tool tests if separate
Also run:
- python -m compileall agent_lab tests
- git diff --check
ACCEPTANCE:
- Voice is a universal transport/tool capability, not a separate business-logic branch.
- Voice transcript is routed through the same canonical text -> Hermes agent path.
- Voice path receives the same enabled_toolsets as text for the same selected_agent.
- Fin tools are not exposed to agents that do not have them in their allowlist.
- Provider request does not contain invalid dot-named tool names.
- Internal tool ids still map to correct handlers.
- Tool results return to the agent loop.
- Context hydration remains intact.
- Fin receipt tool loop remains intact.
- No provider/model calls in tests.
- No Telegram API calls in tests.
- No production expense created by Codex.
- No agent slug hardcode.
- No chat/user hardcode.
- Commit pushed.
- Service restarted if source changed.
- Working tree clean.
REPORT:
Use AGENTS.md report contract.
Add task-specific fields:
- MAIN_TASKS_REPEATED
- universal_scope_proof
- voice_current_path
- canonical_text_path_reuse
- voice_tool_capability_design
- voice_business_logic_removed_or_neutralized
- selected_agent_tool_allowlist_source
- enabled_toolsets_text_vs_voice
- non_fin_agent_safety
- provider_tool_name_mapping
- internal_tool_id_mapping
- voice_transcript_to_agent_tests
- voice_toolset_tests
- provider_safe_name_tests
- no_agent_slug_hardcode_proof
- no_chat_user_hardcode_proof
- context_hydration_preserved
- fin_receipt_tools_preserved
- production_side_effects
PENDING_CODEX_PROMPT_END
### 9. Current stop-point after this append
Current stop-point:
- CONTEXT source/runtime fix is reported live-ready.
- TOOLS receipt tool loop is reported implemented and verified by source/runtime/tests.
- VOICE is the next unresolved architecture task.
- The pending next Codex prompt is OPENSCRIPT_AGENT_LAB_VOICE_AS_UNIVERSAL_HERMES_TOOL_CAPABILITY_20260519_01.
- Do not run a new OCR, matcher, receipt parser, DB schema, or context-router fix before the VOICE/tool capability task unless new proof changes the root cause.
### 10. What not to do next
Do not:
- fix more confirmation words;
- add another matcher;
- add another receipt-specific voice branch;
- hardcode plankton;
- hardcode chat/user IDs;
- treat voice as Fin-specific;
- change OCR/item parsing;
- change DB schema;
- change UI;
- run provider/model calls in tests;
- run Telegram API calls in tests;
- create production expenses by Codex.
### 11. Next exact step
When the user asks to proceed, use the pending prompt:
OPENSCRIPT_AGENT_LAB_VOICE_AS_UNIVERSAL_HERMES_TOOL_CAPABILITY_20260519_01
Purpose:
- make voice a universal transport/tool capability;
- make voice transcript enter the same canonical text -> Hermes agent/tool path;
- preserve CONTEXT and TOOLS fixes;
- add provider-safe tool name mapping if required;
- prove no agent-specific hardcode.
<!-- CONTEXT_APPEND_END id=CTX_20260519_CONTEXT_TOOLS_VOICE_PENDING_PROMPT_V1 -->

<!-- CONTEXT_APPEND_BEGIN id=CTX_20260519_PROJECT_DOCS_UPDATE_CONTEXT_TOOLS_VOICE_STATUS source=chatgpt_inline_project_update accepted_by_user=yes -->

## 2026-05-19 — Project docs update: CONTEXT / TOOLS / VOICE status

This append records the project-level documentation update after the context and tool-loop work.

Main tasks to keep visible:

1. CONTEXT:
   - next Telegram turn must carry full receipt context;
   - not just total amount;
   - reported live-ready via commit `8cdba40`.

2. TOOLS:
   - Telegram live agent must be Hermes tool-capable;
   - Fin tools available to selected agent;
   - model chooses tools semantically;
   - tools read/write DB;
   - tool results return to model/agent;
   - reported live-ready via commit `fb6f892569dc78db5d24bc8541d297fc9ab22556`.

3. VOICE:
   - next unresolved architecture task;
   - must be universal transport/tool capability;
   - not a separate business branch;
   - not hardcoded to one agent;
   - transcript must enter canonical text/Hermes agent/tool loop.

Latest saved context:
- `CTX_20260519_CONTEXT_TOOLS_VOICE_PENDING_PROMPT_V1`
- private commit: `ea0bc2b4e03b12f1895c9520ca8ad24fbfd0a1fe`
- public docs commit: `170fbf31d35b69882b69936a26e4b9684391579f`

Next exact prompt:
- `OPENSCRIPT_AGENT_LAB_VOICE_AS_UNIVERSAL_HERMES_TOOL_CAPABILITY_20260519_01`

Do not run local symptom fixes before the VOICE task unless new proof changes the root cause.

<!-- CONTEXT_APPEND_END id=CTX_20260519_PROJECT_DOCS_UPDATE_CONTEXT_TOOLS_VOICE_STATUS -->

<!-- CONTEXT_APPEND_BEGIN id=CTX_20260520_TELEGRAM_HERMES_FIN_RECEIPT_EXTRACTION_AND_DOCS_WORKFLOW source=chatgpt_inline_current_dialogue accepted_by_user=yes -->

## 2026-05-20 — Telegram/Hermes/Fin receipt current state and docs-update workflow correction

### Summary

The dialogue spent a long sequence isolating repeated failures in the Telegram -> agent -> Hermes -> tools -> Telegram chain.

The user repeatedly emphasized:

- do not fix one small piece and break another;
- tests are valid only if they prove the whole system still works after the run;
- completion is invalid if the bot is left paused or if only one agent is checked;
- universal behavior across agents is mandatory;
- receipt photo must go through `receipt_photo_draft`;
- the receipt tool must extract all receipt information, not only final amount.

### Proven chain facts from recent reports

The chain was eventually proven for multiple normal agents:

Fin-enabled agents:
- `squidward`
- `plankton`

Non-Fin normal agent:
- `runtime_apply_smoke_20260507`

For Fin agents:
- receipt photo reached `receipt_photo_draft` through Hermes;
- next-turn context could answer “какая сумма?” from prior receipt result.

For non-Fin agent:
- `fin.receipt` was blocked as expected.

### Telegram pause issue

A later “agent does not answer” symptom was proven to be:

- `worker_not_polling`
- `bot_status=paused`
- `live_enabled=false`
- `thread_running=false`

Cause:
- persisted Telegram control state was paused in `/var/lib/openscript-agent-lab/telegram/connector_state.json`.

Important rule learned:
- after any Telegram/Hermes/Fin run, final state must be working;
- run cannot be complete if bot is left paused.

### Current receipt OCR issue

The user sent a generated product receipt through Telegram.

Visible on image:
- grocery/product receipt;
- visible total `1 189.63`;
- visible item lines;
- visible date appeared to be `24.05.2025 14:32`.

Bot response:
- draft saved;
- merchant extracted;
- date extracted as `28.05.2025`;
- amount missing.

Proof run conclusion:
- current photo reached `receipt_photo_draft`;
- no stale state;
- first failing step: `OCR_total_missing`;
- selected OCR candidate did not contain usable total line;
- tool result had `amount=null`, `item_count=0`;
- Hermes correctly reported missing amount from tool result.

### Product correction

The user clarified that per ТЗ the goal is not just final amount.

The receipt business layer must extract the full useful receipt structure:

- merchant;
- date/time;
- total;
- item names;
- quantities;
- unit prices;
- item sums;
- taxes/payment lines when available;
- structured missing fields when extraction fails.

### Generated receipt images

Receipt image #1:
- supermarket receipt;
- visible total `1 189.63`;
- multiple product rows;
- used in Telegram and failed OCR total extraction.

Receipt image #2:
- supermarket receipt;
- visible total `1 421.56`;
- rows include milk, bread, eggs, cheese, sausage, tomatoes, cucumbers, apples, tea, sugar, bag;
- date: `24.05.2025 14:32`;
- intended for further product receipt extraction testing.

These must not be hardcoded.
They are examples for the shared class: Telegram-compressed/product receipt OCR.

### Corrected documentation-update workflow

The user clarified a standing docs-update workflow rule.

When project docs/context/roadmap/module-map need updating:

1. ChatGPT must first check current repo docs/public docs.
2. ChatGPT must identify the last saved docs point:
   - context append id;
   - roadmap append id;
   - module map append id;
   - current_status state;
   - project snapshot id/time.
3. ChatGPT must then use only new dialogue content after that saved point.
4. ChatGPT must synthesize the new context/roadmap/module-map append text itself.
5. The Codex prompt must include all append text explicitly inline.
6. Codex must only apply the given text, update metadata, run checks, commit/push and refresh public docs.
7. Codex must not be asked to “figure out what to append” from old docs or memory.

### Current next technical step

Next correct Codex run:
- shared receipt extraction proof/design/fix.

It should not start with Telegram/auth/Hermes unless fresh current proof says that is broken.

It must focus on:

- OCR artifact retention for diagnostics;
- OCR candidate generation and scoring;
- parsing amounts with thousand spaces and decimal dot/comma;
- parsing date/time robustly;
- extracting item names/quantities/prices/sums;
- structured tool result;
- tests over multiple product receipt fixtures.

### Non-negotiable acceptance for future receipt fix

A future receipt extraction run is not complete unless:

- `receipt_photo_draft` is called through Hermes;
- merchant/date/total/items are extracted when visible;
- all item sums are present in structured output when visible;
- missing fields are truthful;
- no hardcoded one receipt;
- no agent-invented facts;
- no app-layer bypass;
- no final expense without confirmation;
- bot remains enabled and working at the end if live Telegram is in scope.

<!-- CONTEXT_APPEND_END id=CTX_20260520_TELEGRAM_HERMES_FIN_RECEIPT_EXTRACTION_AND_DOCS_WORKFLOW -->

## 2026-05-21 — YouTube subtitles tool implemented, UI-connected, and manually proven through Telegram

The planned “Ютуб” tool family has advanced from planned/design state to a working MVP for the first capability: YouTube subtitles/transcript extraction with timings by video URL.

Implemented tool slug:

- `youtube.subtitles_get`

Accepted product architecture remains:

- Agent Lab -> selected agent -> Hermes runtime/profile -> tool call -> deterministic executor -> structured factual result -> agent answer.

The tool is not a standalone script, not a UI-only parser, not a free-form LLM transcript generator, and not globally enabled for all agents.

Completed/proven layers:

1. Vendor mechanism imported and documented:
   - local vendor docs for `youtube-transcript-api` were imported under `docs/codex_source/vendor/youtube_transcript_api/**`;
   - first mechanism is direct public transcript retrieval by `video_id`;
   - no YouTube Data API, OAuth, API keys, cookies, proxies, yt-dlp, video download, audio download, ASR, or LLM-generated transcript are used for the first version.

2. Source implementation added:
   - deterministic executor around `youtube-transcript-api`;
   - YouTube URL -> `video_id` extraction;
   - accepted URL types include `watch?v=`, `youtu.be/`, and `shorts/`;
   - invalid/channel/search/playlist-only/arbitrary URLs are rejected by normalized errors;
   - structured result includes timestamped subtitle segments.

3. Operator UI added:
   - top-level tab `Ютуб`;
   - operator form for manual subtitle test;
   - backend test route `POST /api/tools/youtube-subtitles/test`;
   - route reuses the shared deterministic executor;
   - operator test does not enable the tool for agents.

4. Language selection corrected:
   - old strict requested-language matching was removed;
   - new policy: default priority `ru -> en -> any available transcript`;
   - operator-provided languages are priority hints, not strict filters;
   - if any transcript exists, the tool should not fail with `requested_language_unavailable` only because the requested language is unavailable.

5. Agent attachment UI added:
   - the `Ютуб` tab has agent connection controls;
   - operator can attach `youtube.subtitles_get` to the selected agent through the UI;
   - source package skill/doc and tool binding are created/updated by the existing source-package flow;
   - Hermes apply remains the normal source -> runtime sync boundary;
   - no global tool enablement is performed.

6. Manual Telegram proof succeeded:
   - the user connected the tool to `squidward` through the UI;
   - `squidward` is available through Telegram bot/router;
   - the user sent a YouTube request to Telegram;
   - the bot/agent returned subtitles in Telegram;
   - this proves the end-to-end path: Telegram message -> selected agent -> Hermes-visible YouTube tool -> deterministic subtitle extraction -> Telegram response.

Current accepted status:

- `youtube.subtitles_get`: IMPLEMENTED / UI_CONNECTED / AGENT_ATTACHABLE_VIA_UI / MANUALLY_TELEGRAM_PROVEN
- operator UI test: DONE
- agent attachment UI: DONE
- language fallback `ru -> en -> any`: DONE
- Telegram manual proof with Squidward: DONE

Current stop-point:

Do not restart YouTube vendor/API/design/implementation work from older planned-state docs.

Next YouTube work, if requested, should be polish/extension only, such as:

- long transcript chunking for Telegram limits;
- continuation/pagination UX;
- summary mode on top of returned subtitles;
- language/source display polish;
- applying the tool to additional agents through the UI;
- regression proof if a new failure appears.

Do not regress:

- do not reclassify “Ютуб” as not implemented;
- do not ask Codex to rediscover the vendor mechanism;
- do not reintroduce YouTube Data API/OAuth/cookies/proxies/yt-dlp as the first path;
- do not bypass Hermes with an app-local-only tool;
- do not hardcode Squidward as the only supported agent;
- do not globally enable the tool for all agents;
- do not remove the operator UI test path;
- do not remove the agent-attachment UI path.

## 2026-05-21 — New product direction: Telegram AI/Vibecoding Publisher Agent and YouTube Research pipeline

After completing the first “Ютуб” subtitles tool MVP, the user defined the next product direction.

The future product target is an agent that helps run a Telegram public channel about neural networks, AI tools, coding agents, and vibe coding.

The future agent should use a staged pipeline:

1. find relevant YouTube videos;
2. store video metadata in a database;
3. collect subtitles through the existing `youtube.subtitles_get`;
4. store transcripts and lifecycle state;
5. deduplicate already-known and already-published sources;
6. rank/sort candidates;
7. run an LLM-based editorial evaluation on already collected facts;
8. later compose Telegram posts;
9. later generate illustrations;
10. later publish to Telegram.

Critical decision:

Do not implement this as one monolithic “agent searches and posts by itself” tool.

The next technical block is the YouTube Research intake pipeline, starting with video search and storage.

Initial conceptual tools/stages:

- `youtube.search_candidates`
- `youtube.collect_subtitles_for_candidates`
- `youtube.rank_candidates`
- `youtube.editorial_evaluate`

Shared storage is required for:

- video metadata;
- channel name/channel id;
- subtitles/transcripts;
- candidate status;
- publication status;
- duplicate detection;
- approximately 3-month transcript/full-text retention;
- longer published markers to prevent reposting.

Important product rule:

Published videos must not be loaded back into the posting queue.

The current next discussion/technical step is search-provider evaluation for `youtube.search_candidates`, not Telegram publishing, not image generation, and not full automation.

## CTX_20260522_YOUTUBE_SEARCH_AGENT_TOOL_GATE_FIX_AND_VISIBILITY_RESOLUTION

### Summary

The YouTube Research pipeline advanced from subtitles-only to a working search/intake + full-description enrichment + agent-attachable Hermes tool path.

Completed and proven:

- `youtube.subtitles_get` was already implemented, UI-connected, attachable to agents, and manually proven through Telegram.
- `youtube.search_candidates` search/intake stage was implemented for operator UI.
- Search profile persistence was implemented.
- Russian UI labels and language/region preset chips were added.
- Runtime dependency `yt-search-python==2.0.0` was declared and installed for the live service runtime.
- Test candidate DB was cleaned after setup/proof runs while preserving the saved search profile.
- Full video description enrichment was proven and implemented as a separate stage over saved candidates, not as direct provider bypass.
- Enrichment uses metadata-only `youtubesearchpython.Video.get(...)` through the application route/stage, not transcripts, not StreamURLFetcher, not yt-dlp, not cookies, not API keys.
- `youtube.search_candidates` was made attachable to agents through UI/source-package/runtime/Hermes path.
- Hermes wrapper propagation was fixed universally by invoking the Hermes vendor restore/sync helper on UI startup.
- Final visibility issue was proven and fixed in the `youtube.search_candidates` gate/profile detection path.

### Search and enrichment pipeline status

The current YouTube Research backend/operator pipeline consists of:

1. `youtube.search_candidates`
   - reads saved UI profile;
   - searches YouTube through the approved `yt-search-python` provider path;
   - applies deterministic filters and deduplication;
   - stores candidates in the YouTube Research SQLite DB.

2. `youtube.enrich_candidate_metadata`
   - operates only on already saved candidates;
   - fetches full video descriptions through metadata-only provider path;
   - stores fields such as `description_full`, `description_full_length`, `description_full_fetched_at`, provider/source/error metadata.

3. Future stages remain separate:
   - metadata pre-evaluation/ranking;
   - subtitle collection;
   - editorial/post formatting;
   - image generation;
   - Telegram publication.

Do not merge future stages into the search tool.

### DB cleanup status

After search/enrichment proof runs, test candidate data was cleaned:

- candidate rows before cleanup: 122;
- enriched rows before cleanup: 12;
- candidate rows after cleanup: 0;
- enriched rows after cleanup: 0;
- saved search profile rows after cleanup: 1;
- DB schema preserved;
- DB file not deleted;
- backup created under `/tmp/openscript_youtube_research_cleanup_20260521/`.

### Agent/Hermes attach status

`youtube.search_candidates` is now attachable to a selected agent through the YouTube search UI.

The attach path follows the same source/runtime pattern as `youtube.subtitles_get`:

- UI attach card/button in `Ютуб → Поиск видео`;
- source package binding in `agent-packages/<slug>/tools.json`;
- skill doc `agent-packages/<slug>/skills/youtube-search-tool.md`;
- runtime apply copies package/skills/registry snapshot into the Hermes profile;
- Hermes wrapper exposes the tool to Hermes;
- agent invokes the tool through narrow input contract.

The tool remains saved-profile-driven. In v1, the agent must not invent arbitrary raw search queries or provider parameters. Operator edits the search profile in UI; agent invokes the saved profile.

### Critical bug: agent did not see youtube.search_candidates

Symptom:

- User manually attached `youtube.search_candidates` to Squidward through UI and applied runtime.
- Squidward in Telegram still said it did not have the YouTube search tool.
- `youtube.subtitles_get` was visible and usable.
- A separate manual test showed `youtube.subtitles_get` also worked for Plankton after adding it, so the cause could not be assumed to be a generic “session stale” issue.

Wrong hypotheses that were investigated and rejected as final root cause:

- session refresh as the primary fix;
- `/new` or `/reset`;
- session file deletion;
- runtime apply missing;
- Telegram routed to wrong agent;
- wrapper missing from vendor path;
- dot-vs-underscore naming mismatch;
- registry metadata mismatch;
- wrapper registration mismatch.

Important diagnostic lesson:

If a new tool is invisible but a similar working tool is visible, do not start by fixing sessions. First compare the working tool and broken tool across:

- source registry;
- root tool registry;
- source package binding;
- runtime profile binding;
- runtime registry snapshot;
- Hermes wrapper import;
- wrapper registration;
- safe registry check_fn/gate;
- gateway discovery;
- `agent.tools`;
- `session_meta.tools`.

### Session snapshot confusion: symptom, not root cause

During debugging, `session_meta.tools` looked like the broken layer because the live Squidward session artifact contained `youtube_subtitles_get` but did not contain `youtube_search_candidates`.

This led to a wrong intermediate hypothesis:

- the session was stale;
- the product needed `/new` or `/reset`;
- session files should be deleted or rebuilt;
- the system needed a per-turn runtime/toolset check;
- runtime apply should invalidate all session tool contexts.

This hypothesis was rejected after comparing the working `youtube.subtitles_get` path with the broken `youtube.search_candidates` path.

Important conclusion:

`session_meta.tools` was only the place where the symptom became visible. It was not the first broken layer.

The actual first broken layer was earlier:

`youtube.search_candidates` was filtered out by the Hermes safe registry gate before `agent.tools` was built.

Therefore the correct solution was NOT:

- session reset;
- `/new`;
- `/reset`;
- manual session deletion;
- session invalidation on every reply;
- broad runtime/session refresh;
- Squidward-specific patch.

The correct solution was:

- compare working subtitles gate and broken search gate;
- inspect `inspect_youtube_search_candidates_gate()`;
- inspect `check_youtube_search_candidates_available()`;
- inspect `registry.get_definitions(...)`;
- prove that search was excluded by the safe registry filter;
- fix the search gate profile detection.

Final fix:

`agent_lab/youtube_search_candidates.py` was changed to resolve the active Hermes profile with the same live per-profile HERMES_HOME mechanism as the working subtitles tool:

`hermes_constants.get_hermes_home()`

instead of static:

`paths.HERMES_HOME`

After this fix and service restart, safe discovery returned both:

- `youtube_search_candidates`;
- `youtube_subtitles_get`.

The agent then began seeing the search tool.

Future debugging rule:

If `session_meta.tools` lacks a tool, do not immediately fix session lifecycle. First prove whether the tool was filtered before `agent.tools` by checking gate/check_fn/discovery.

### Final proven root cause

Final proof established that `youtube.search_candidates` was filtered out by the Hermes safe registry before `agent.tools` was built.

Working subtitles gate:

- `agent_lab/youtube_subtitles.py` used the live per-profile Hermes home:
  `hermes_constants.get_hermes_home()`;
- with `HERMES_HOME=/var/lib/openscript-agent-lab/hermes/profiles/squidward`,
  `_current_profile_slug()` resolved `squidward`;
- `inspect_youtube_subtitles_gate().ok=true`;
- gateway discovery returned `youtube_subtitles_get`.

Broken search gate before fix:

- `agent_lab/youtube_search_candidates.py` used static:
  `paths.HERMES_HOME.resolve()`;
- under live per-profile `HERMES_HOME=/var/lib/openscript-agent-lab/hermes/profiles/squidward`,
  `_current_profile_slug()` returned null;
- `inspect_youtube_search_candidates_gate()` returned `profile_missing`;
- `check_youtube_search_candidates_available()` returned false;
- patched safe registry filtered the tool out;
- gateway discovery did not return `youtube_search_candidates`;
- therefore the tool never reached `agent.tools`, `agent_result["tools"]`, or `session_meta.tools`.

This was not a session-refresh bug and not a wrapper-registration bug.

### Fix

Commit:

`df3a3b009132ada4ff3ada75178a97e46fd2a686`

Fix summary:

- changed `youtube.search_candidates` gate/profile detection to use the same live HERMES_HOME pattern as `youtube.subtitles_get`;
- `_current_profile_slug()` now resolves the active profile slug correctly under per-profile HERMES_HOME;
- search gate now returns ok when runtime profile has the tool, saved profile exists, and provider dependency is available;
- focused tests added for per-profile HERMES_HOME, gate success/failure, and discovery.

After service restart:

- `openscript-agent-lab-ui.service` restarted successfully;
- `/healthz` returned ok;
- safe discovery with `HERMES_HOME=/var/lib/openscript-agent-lab/hermes/profiles/squidward` returned:
  - `youtube_search_candidates`;
  - `youtube_subtitles_get`;
- user confirmed the agent began seeing the search tool.

### Future rule for similar bugs

For future Hermes tool visibility problems:

1. Compare a working tool and broken tool side-by-side.
2. Verify wrapper propagation and import, but do not stop there.
3. Check safe registry gate/check_fn before blaming session snapshots.
4. Explicitly inspect:
   - `inspect_<tool>_gate()`;
   - `check_<tool>_available()`;
   - `registry.get_definitions(...)`;
   - gateway discovered tool names.
5. If working tool uses `hermes_constants.get_hermes_home()` and broken tool uses static `paths.HERMES_HOME`, fix the broken tool to use live per-profile HERMES_HOME.
6. Do not use `/new`, `/reset`, manual session deletion, or per-turn runtime checks unless a separate proof proves a real session lifecycle bug.

### Current stop point

YouTube search agent tool visibility is fixed.

Current recommended next step:

- user manually tests the Squidward Telegram command:
  `запусти поиск ютуб по сохранённому профилю и покажи результат`.

Expected:

- Squidward sees the tool;
- calls `youtube.search_candidates`;
- uses saved UI profile;
- runs search + enrichment;
- returns factual summary and candidate preview.

If the tool call works, the next technical stage is metadata pre-evaluation/ranking design.
If the tool is visible but execution fails, diagnose the live tool execution path, not registry/wrapper/gate.

<!-- CONTEXT_APPEND_BEGIN id=CTX_20260522_YOUTUBE_SELECT_CANDIDATES_MANUAL_FIRST_HERMES_MEDIATED_TOOL source=chatgpt_inline -->

## CTX_20260522_YOUTUBE_SELECT_CANDIDATES_MANUAL_FIRST_HERMES_MEDIATED_TOOL

### Summary

The next YouTube Research pipeline stage is `youtube.select_candidates`.

This stage is a manual-first tool, but manual-first does not mean bypassing Hermes. The human operator must be able to start and review the selection manually, but the execution path must still use the same Hermes/tool contract that future agents will use.

This decision prevents two incompatible implementations: one manual direct-backend path and one later Hermes/agent path.

### Role separation

Do not confuse these roles:

1. **Human operator**

   The operator manually starts candidate selection and reviews the proposed candidates.

   The operator is not the curator agent and is not the future public-manager agent.

   The operator-facing manual path must still be Hermes-mediated through the same tool contract, not a direct DB bypass.

2. **`youtube.select_candidates` tool**

   This is the independent sorting/selection tool.

   It reads already stored YouTube candidates, performs deterministic pre-filter/pre-rank, may use an internal curator/evaluator Hermes profile for editorial judgement, asks for operator review when configured, writes candidate lifecycle statuses, and returns a structured result.

   It must not call the next editing/formatting/publishing tool directly.

3. **Internal curator/evaluator Hermes profile**

   This is the LLM-backed evaluator used inside the selection tool.

   It is not the agent that initiates the whole publication chain.

   It evaluates stored factual candidate snapshots and learned/policy preferences. It must not browse YouTube, invent facts, publish to Telegram, or call the next pipeline tool.

4. **Future public-manager agent**

   This future agent will manage the Telegram public/channel workflow.

   It may later call `youtube.select_candidates` through the same Hermes/tool contract that the operator uses manually.

   It receives selected candidates and then decides whether and when to call the next independent editing/formatting tool.

5. **Next editing/formatting tool**

   This is a separate future tool.

   `youtube.select_candidates` must only return candidates ready for the next stage. It must not invoke the editing/formatting tool itself.

### Required execution model

`youtube.select_candidates` must support:

- operator/manual initiation first;
- later future-agent initiation;
- one shared Hermes/tool contract for both;
- no separate direct DB bypass for manual use;
- deterministic pre-rank/filter before LLM evaluation;
- optional internal curator/evaluator Hermes profile for selection;
- operator review when enabled;
- structured output for the caller.

### MVP operator feedback

MVP feedback buttons are exactly:

- `✅ Подходит`
- `⏭ Пропустить`
- `❌ Не подходит`

Do not add these buttons in MVP:

- `📄 Нужны субтитры`
- `📝 Причина/заметка`

### Candidate lifecycle meaning

`✅ Подходит` means:

- mark candidate as approved by operator;
- mark candidate as ready for the next pipeline stage;
- return it in `selected_candidates`.

`⏭ Пропустить` means:

- skip candidate for the current batch;
- optionally apply cooldown / not-in-current-batch behavior;
- do not treat it as a permanent rejection.

`❌ Не подходит` means:

- mark candidate as rejected;
- do not suggest it again for this tool unless an explicit reset/reopen action is introduced later.

### Storage and memory boundary

The DB stores objective facts and lifecycle state:

- candidate metadata;
- candidate status;
- shown/reviewed markers;
- approved/skipped/rejected state;
- ready-for-next-stage markers;
- anti-repeat state;
- published markers.

The DB is not the primary learned taste memory.

Hermes profile-local memory stores learned curator taste:

- what the operator tends to approve;
- what the operator tends to skip or reject;
- recurring preference patterns.

A source-managed policy document stores current editorial priorities and hard exclusions.

Policy outranks learned memory.

Learned memory may bias selection, but must never override:

- objective DB facts;
- anti-repeat;
- published markers;
- hard negative topics;
- current policy priorities.

### System agent boundary

The existing `system_filter` protected system agent must not be reused for YouTube curator taste memory or editorial selection.

`system_filter` remains a system-level gate/filter agent.

The YouTube selector/curator must be a separate tool/profile design.

### Current implementation order

Do not implement the full curator immediately.

The safe implementation order is:

1. document this contract;
2. design/prove current candidate storage/status owner;
3. implement manual-first Hermes-mediated backend action;
4. implement operator review UI/actions;
5. add status transitions;
6. add internal curator/evaluator profile;
7. add learned memory update;
8. add clear curator memory action;
9. expose the same contract to future public-manager agent;
10. implement the next editing/formatting tool separately.

<!-- CONTEXT_APPEND_END id=CTX_20260522_YOUTUBE_SELECT_CANDIDATES_MANUAL_FIRST_HERMES_MEDIATED_TOOL -->

<!-- CONTEXT_APPEND_BEGIN id=CTX_20260522_YOUTUBE_SELECT_CANDIDATES_SYSTEM_OPERATOR_CORRECTION source=chatgpt_inline -->

## CTX_20260522_YOUTUBE_SELECT_CANDIDATES_SYSTEM_OPERATOR_CORRECTION

### Correction

The previous `youtube.select_candidates` documentation used misleading wording around “human operator”, “manual operator”, and “manual-first”.

Correct product meaning:

`youtube.select_candidates` is a Hermes-mediated selection tool.

The sorting actor is a **system Hermes operator / curator profile** inside the tool, not a direct human/manual backend operator.

This system operator works through Hermes.

### Correct roles

1. **Future public-manager agent**

   This future agent manages the Telegram public/channel workflow.

   It may initiate `youtube.select_candidates` through the Hermes/tool contract.

   It receives the selected candidates and decides whether and when to call the next independent editing/formatting tool.

2. **`youtube.select_candidates` tool**

   This is the independent sorting/selection tool.

   It consumes already stored YouTube candidate facts from DB.

   It performs deterministic pre-filter/pre-rank, then may use a system Hermes operator/curator profile for LLM-assisted selection.

   It returns selected candidates and lifecycle/status information.

   It must not call the next editing/formatting/publishing tool directly.

3. **System Hermes operator / curator profile**

   This is the internal sorting/evaluation actor used by the selection tool.

   It has its own policy, skills, profile-local Hermes memory, and learned taste.

   It evaluates stored factual candidate snapshots only.

   It must not browse YouTube, publish to Telegram, call the next pipeline tool, or invent facts.

4. **Human reviewer, if enabled later**

   A human may later confirm selection through Telegram review buttons if review mode is enabled.

   That review is a confirmation layer, not a direct backend/manual mode.

### Correct review buttons

If human review is enabled later, MVP buttons remain exactly:

- `✅ Подходит`
- `⏭ Пропустить`
- `❌ Не подходит`

Do not add in MVP:

- `📄 Нужны субтитры`
- `📝 Причина/заметка`

### Memory and policy

The system Hermes operator/curator profile owns learned selection taste through Hermes profile-local memory.

Source-managed policy stores current priorities and outranks learned memory.

DB stores objective candidate facts, lifecycle states, anti-repeat and published markers.

DB is not the learned taste memory.

### Pipeline boundary

`youtube.select_candidates` returns selected candidates.

The next editing/formatting tool is a separate independent tool.

The public-manager agent, not the selection tool, decides when to call the next tool.

<!-- CONTEXT_APPEND_END id=CTX_20260522_YOUTUBE_SELECT_CANDIDATES_SYSTEM_OPERATOR_CORRECTION -->

<!-- CONTEXT_APPEND_BEGIN id=CTX_20260522_YOUTUBE_SELECT_CANDIDATES_CURATOR_RUNTIME_UI_PROGRESS source=chatgpt_inline_project_update accepted_by_user=yes -->

## CTX_20260522_YOUTUBE_SELECT_CANDIDATES_CURATOR_RUNTIME_UI_PROGRESS

### Summary

After the previous correction that `youtube.select_candidates` uses a system Hermes sorting operator, the YouTube Research selection stack advanced through multiple implementation layers.

The current stack now has:

1. `youtube.select_candidates` source contract.
2. Selection lifecycle storage.
3. Protected `youtube_curator` source package.
4. Offline selector-to-curator boundary.
5. `youtube_curator` runtime profile.
6. Read-only UI/status panel.
7. Source-policy editor.
8. UI apply preview/apply controls.

This update records completed work only. It does not mean live Hermes-backed curator execution is enabled yet.

### `youtube.select_candidates` contract

The first source-level selector contract was implemented at commit:

`2d0b62afa968ad685da49f25c62aaf16b20ce175`

It added the deterministic response-only selector service, Hermes wrapper/overlay, registry metadata, and focused tests.

Important properties:

- deterministic selection only;
- no live DB mutation from the public selection path;
- no LLM/provider call;
- no Telegram call;
- no next editing/formatting tool call;
- `next_tool_called: false`.

This contract is the shared boundary that future callers use. It must not become a one-off UI shortcut.

### Selection lifecycle storage

Selection storage was implemented at commit:

`a9f1c602e006523f71534750ead5b1efd5917e2e`

Added tables:

- `youtube_selection_batches`
- `youtube_candidate_selection_state`

The old `youtube_candidates.status` enum remains unchanged.

Selection-specific states such as:

- `approved`
- `skipped`
- `ready_for_next_stage`

are stored in selection storage, not in the old base status enum.

`rejected` remains a hard-block state and updates both selection state and the base candidate row.

### `youtube_curator` source package and protection

The `youtube_curator` source package was created at commit:

`d8227f5c8486f5828d2cadfded871120e27e8ce0`

Package files:

- `manifest.json`
- `SOUL.md`
- `rules.md`
- `examples.md`
- `provider.defaults.json`
- `README.md`
- `skills/youtube-selection-policy.md`

The multi protected system agent registry was implemented at commit:

`efed938a224047d99f3d6749dc6df42c6944cc9d`

Protected slugs now include:

- `system_filter`
- `youtube_curator`

`youtube_curator` is protected/internal/system, non-deletable through normal product paths, not creatable through normal create, not cloneable into, and excluded as a Telegram command candidate.

Manifest-only protection is not trusted as authority. The source-owned protected slug registry is the authority.

### Telegram routing clarification

A temporary investigation around the Telegram “Бот-роутер” UI clarified that the selected router agent shown there is the active/default/fallback routing target, not proof of a separate deleted LLM router brain.

Current accepted state:

- Telegram works.
- Agents answer.
- Agent switching works.
- No Telegram/router fix is active now.
- Do not create a new `telegram_router` system agent unless a future explicit architecture design proves it is needed.

This is separate from `youtube_curator`.

### Offline selector-to-curator boundary

The offline curator boundary was implemented at commit:

`cc60c9c82683fc71dff91fe2a8b745ccf4cce1a7`

Implemented in:

- `agent_lab/youtube_select_candidates.py`
- `tests/test_youtube_select_candidates.py`

Added:

- compact curator snapshot builder;
- policy snapshot loaded only from safe source package files:
  - `agent-packages/youtube_curator/rules.md`
  - `agent-packages/youtube_curator/SOUL.md`
  - `agent-packages/youtube_curator/skills/youtube-selection-policy.md`
- `memory_snapshot = null`;
- pluggable curator backend interface;
- offline fake curator backend;
- strict response validation for unknown ids, invalid decisions, and `next_tool_called` / `next_tool_name` violations;
- planned selection actions.

The fake backend selects only known candidate ids. It does not invoke Hermes, provider/model, Telegram, YouTube live search, runtime memory, or live DB mutation.

### Runtime profile

The `youtube_curator` runtime profile was created through the approved runtime apply path.

Runtime profile path:

`/var/lib/openscript-agent-lab/hermes/profiles/youtube_curator`

Last apply timestamp recorded:

`2026-05-22T12:59:30.782514Z`

The apply created/synced expected runtime files and dirs, including:

- `SOUL.md`
- `.agent-lab/source_docs/rules.md`
- `.agent-lab/source_docs/examples.md`
- `skills/youtube-selection-policy.md`
- `.agent-lab/tool-registry.snapshot.json`
- `.agent-lab/last_apply.json`
- `memories/`
- `sessions/`
- `logs/`
- `cron/`
- `.agent-lab/secrets/`

The apply did not call provider/model, Telegram, YouTube, or DB. It did not write or delete runtime memory.

### Read-only UI/status panel

The read-only YouTube Curator panel was implemented at commit:

`bfc14480d35c84ad2d4d217028d3b3015e14ecfe`

Changed:

- `agent_lab/admin_server.py`
- `agent_lab/static/index.html`
- `agent_lab/static/app.js`
- `tests/test_admin_server.py`

It extended `/api/state` with sanitized `youtube_curator_status` and rendered a read-only panel in:

`Ютуб → Сортировка`

The panel shows:

- source package status;
- protected/internal status;
- runtime profile status;
- last apply status;
- policy source presence;
- selector defaults;
- readiness.

The panel does not expose secrets, runtime memory contents, sessions, logs, or `.agent-lab/secrets/`.

A controlled service restart verified the live process:

- service: `openscript-agent-lab-ui.service`
- PID changed from `1296580` to `1343343`
- `/healthz` stayed `200 / ok`
- live `/api/state` now includes `youtube_curator_status`
- static UI panel is present.

### Source policy editor

The source policy editor was implemented at commit:

`d59bfde6f631b7fcb1fb800038e613d07818b72d`

UI location:

`Ютуб → Сортировка → YouTube Curator / Системный оператор отбора`

Editable source file:

`agent-packages/youtube_curator/rules.md`

Endpoint reused:

`/api/agents/youtube_curator/documents/rules.md`

This editor writes source package policy only. It does not apply to runtime automatically.

The UI warns that a separate runtime apply is required after saving.

### Apply preview/apply controls

Apply controls were implemented at commit:

`d0b2eb970e7748d2e0a4254fefb0020bfe85cbb4`

Controls:

- `Предпросмотр apply`
- `Применить правила в runtime`

Existing generic endpoints are reused:

- `POST /api/agents/youtube_curator/runtime/apply-dry-run`
- `POST /api/agents/youtube_curator/runtime/apply`

No custom backend route was added.

Real apply is disabled while the policy editor is dirty. Preview is also disabled while dirty, so preview targets saved source only.

Live verification after this commit proved:

- static UI contains both buttons;
- dirty/unsaved warning is present;
- live curator test button is absent;
- `/api/state` still contains sanitized `youtube_curator_status`;
- no apply endpoint was called;
- no runtime mutation occurred.

### Current stop point

Current user-facing next action:

- hard-refresh browser;
- open `Ютуб → Сортировка`;
- verify the YouTube Curator panel, policy editor, and apply controls are visible.

Current technical stop point:

- Do not run live Hermes-backed curator yet.
- First use the UI to edit/save policy, preview apply, and explicitly apply source policy to runtime.
- After policy/apply verification, the next technical block is a separate proof/design for the live Hermes-backed curator adapter.

### Do not repeat

Do not repeat already completed work unless a fresh regression is reported:

- `youtube.search_candidates` implementation;
- search tool visibility/session debugging;
- selection storage design;
- `youtube_curator` package creation;
- protected system-agent registry;
- runtime profile creation;
- read-only UI panel;
- source policy editor;
- apply controls.

Do not restart Telegram/router work for this block. Telegram routing is not the current blocker.

<!-- CONTEXT_APPEND_END id=CTX_20260522_YOUTUBE_SELECT_CANDIDATES_CURATOR_RUNTIME_UI_PROGRESS -->

<!-- CONTEXT_APPEND_BEGIN id=CTX_20260528_YOUTUBE_RANKED_BATCH_LIFECYCLE_AND_SORTING_CORRECTION source=chatgpt_dialogue_and_codex_reports -->
APPEND_ID: CTX_20260528_YOUTUBE_RANKED_BATCH_LIFECYCLE_AND_SORTING_CORRECTION
SOURCE_KIND: chatgpt_dialogue_and_codex_reports
DATE_UTC: 2026-05-28
STATUS: accepted_current_context
TITLE: YouTube ranked moderation lifecycle corrected after sorting/callback drift

Summary:
The current dialogue established that the active technical issue was not Telegram callback handling, but YouTube ranked moderation lifecycle and sorting. The assistant initially drifted into repeated callback/polling investigations. The user corrected the framing: if sorting does not create or serve a correct ranked batch, callback behavior is secondary.

Accepted product model:
- Search stores YouTube candidates in DB.
- Ranking/selection is a separate UI/backend operator action, not “apply runtime” and not “next stack”.
- Curator/Hermes ranks/selects candidates from already stored DB facts.
- Backend persists a durable ranked batch.
- Moderation stack is a slice from an already-ranked batch.
- Stack size is configured display stack size; it is not hardcoded and not the ranking target.
- Ranking target / selected count and moderation stack size are independent values.
- Telegram inline “Следующий стек” is the next-stack control.
- Inline “Следующий стек” must read the next configured stack from the same existing ranked batch.
- Inline “Следующий стек” must not run YouTube search, enrichment, Hermes ranking, or youtube.select_candidates.
- While an active/resumable ranked batch has pending rows, new Curator ranking is blocked.
- Only after the active batch is exhausted may a new ranking be considered.
- If the active batch is exhausted and DB has no eligible candidates, backend must return structured needs_new_search/no_eligible_candidates.
- Empty Curator selection or zero persisted rows must not be ok=true and must not create active empty success batches.

Key accepted proof:
OPENSCRIPT_AGENT_LAB_YOUTUBE_RANKING_EMPTY_CURATOR_SELECTION_ROOT_CAUSE_PROOF_20260528_01 proved:
- current code default target_count was 3, but user product expectation was larger ranking batches;
- stack_size is display stack size and next stack semantics should use the same ranked batch;
- latest empty batch select-a887c112f423 had candidate_pool_size=20 but only one fresh candidate reached Curator due selected-state/window starvation;
- Curator returned selected_video_ids=[] and decisions=[];
- create_ranked_batch persisted 0 rows;
- build_moderation_cards returned 0 cards;
- runner returned ok=true and created an active empty shell;
- this represented DB/window starvation plus zero-selection acceptance.

User correction after proof:
The user clarified that rows marked selected/ranked are not simply “old candidates to skip” during moderation. If they belong to an active ranked batch and remain pending moderation, they must be served to the moderator through next stack until the batch is exhausted.

Accepted fix:
OPENSCRIPT_AGENT_LAB_FIX_YOUTUBE_RANKED_BATCH_LIFECYCLE_AND_CONFIGURED_STACK_SIZE_20260528_01 completed SUCCESS at commit e21a6874ee864a79ad4f2221b6ee4a8a3d723753.
The report stated:
- runner now checks latest non-empty active batch first and serves its current stack;
- only when no active batch is resumable does it call Curator again;
- zero-ranked selection is now structured failure;
- persisted Russian card text is stored for new batches;
- legacy active batches can render cards from stored facts;
- stack_size comes from runner payload / launch parameters and is persisted on ranked batch;
- runner default stack size is 5;
- target_count comes from runner payload / launch parameters and is independent from stack size;
- runner default target_count is 10;
- get_latest_active_batch ignores empty shells and returns latest non-empty active batch only;
- get_current_stack / get_next_stack use stored batch stack size;
- no Telegram callback work was done;
- live proof reused existing active batch select-e9b53dfe41a3, selector/provider were not called, one moderation card was built, and Telegram messages 581/582 were dispatched.

Current stop-point:
Do not continue callback debugging until the user explicitly asks. The latest accepted block is YouTube ranked batch lifecycle fix/report review. The next likely documentation/product gap is whether docs/roadmap should explicitly specify a separate Telegram command for “start ranking”; current ТЗ proves UI/backend start ranking action, Telegram continue moderation command, and inline next stack, but not a separate Telegram bot command for manual ranking launch.

Guardrail:
Future assistants must not describe “Следующий стек” as a Telegram command. It is an inline button/control. The Telegram command described in ТЗ is continue moderation, which resumes active/latest ranked batch; “start ranking/selection run” is a UI/backend operator action unless a future docs update explicitly adds a Telegram command.
<!-- CONTEXT_APPEND_END id=CTX_20260528_YOUTUBE_RANKED_BATCH_LIFECYCLE_AND_SORTING_CORRECTION -->

<!-- CONTEXT_APPEND_BEGIN id=CTX_20260528_RECEIPT_FULL_EXTRACTION_ACTIVE_BLOCK source=chatgpt_dialogue_and_codex_reports -->
## CTX_20260528_RECEIPT_FULL_EXTRACTION_ACTIVE_BLOCK

### Status

The active project block is now full receipt extraction for the Financial Instrument / receipt business layer.

This update records the current working context so future ChatGPT/Codex runs do not restart from Telegram, auth, Hermes, or send-path fixes.

### Proven chain

The current proof state is:

- a receipt photo reached the Telegram chain;
- the same receipt photo reached the selected agent;
- the selected agent invoked `receipt_photo_draft` through Hermes;
- the current broken step is not proven to be Telegram routing;
- the current broken step is not proven to be Telegram auth;
- the current broken step is not proven to be Hermes reply;
- the current broken step is not proven to be Telegram send;
- the proven failing step is OCR/parser extraction;
- observed failing step label: `OCR_total_missing`.

### Receipt facts from the failing case

The visible receipt image contained a total amount:

- `1 189.63`

The tool/OCR result failed to extract usable structured data:

- `amount=null`;
- `item_count=0`;
- OCR candidate text did not provide a usable total line;
- OCR date candidate was `28.05.2025`;
- the visible receipt indicated that the expected date was different.

This must be treated as a class problem in receipt extraction, not as a one-image special case.

### User requirement

The user clarified that receipt processing must extract all useful receipt information, not only the final total.

Required target fields for the next technical block:

- merchant / store name;
- date;
- time if visible;
- final total amount;
- item rows;
- item names;
- quantities;
- unit prices;
- line totals;
- payment facts if visible;
- taxes if visible;
- honest `missing_fields` when OCR/parser cannot recover a field.

### Architecture boundary

Receipt extraction belongs to deterministic business layer.

Hermes/agent may help with language, explanation, and user-facing confirmation text, but must not invent:

- money amounts;
- dates;
- item names;
- quantities;
- prices;
- payment facts;
- taxes.

The business layer must own OCR/preprocessing/parser extraction and must return factual structured results.

### Next technical run

The next technical run should be:

`OPENSCRIPT_AGENT_LAB_RECEIPT_FULL_EXTRACTION_PROOF_DESIGN_FIX`

Run goal:

- prove current OCR/preprocessing/parser path;
- prove why total, date and item rows are missed;
- design and implement a minimal universal full receipt extraction improvement;
- add tests for total, date, item rows, and missing_fields;
- keep Telegram/Hermes routing untouched unless fresh proof shows they are now the first broken layer.

### Not next

Do not reopen these areas unless fresh proof shows they are first broken:

- Telegram polling/routing;
- Telegram auth;
- Hermes auth/provider;
- Telegram send delivery;
- selected-agent routing;
- receipt_photo_draft invocation path.

Do not accept a fix that only extracts the final total. The target is full receipt structure extraction.

### Completion rule

A future receipt extraction fix-run is not complete if:

- the bot ends paused or the Telegram chain is broken;
- receipt_photo_draft stops being called;
- only final total is extracted;
- item rows are ignored without explicit `missing_fields`;
- Hermes invents financial facts instead of consuming deterministic tool output.
<!-- CONTEXT_APPEND_END id=CTX_20260528_RECEIPT_FULL_EXTRACTION_ACTIVE_BLOCK -->

<!-- CONTEXT_APPEND_BEGIN id=CTX_20260529_YOUTUBE_RANKED_BATCH_ACTIVE_STATUS_CORRECTION source=chatgpt_dialogue_and_codex_reports -->
APPEND_ID: CTX_20260529_YOUTUBE_RANKED_BATCH_ACTIVE_STATUS_CORRECTION
SOURCE_KIND: chatgpt_dialogue_and_codex_reports
DATE_UTC: 2026-05-29
STATUS: accepted_current_context
TITLE: YouTube ranked batch active status correction

Summary:
The earlier `receipt_full_extraction` active pointer is stale for the current working stop-point. The accepted current work is the YouTube ranked batch lifecycle and moderation stack, with the open product/docs question about whether ranking start should be a separate Telegram command or remain a UI/backend operator action.

Accepted current stop-point:
- Current active block is YouTube ranked batch lifecycle / moderation stack.
- Search stores YouTube candidates in DB.
- Ranking/selection is a separate UI/backend operator action, not "apply runtime" and not "next stack".
- Curator/Hermes ranks/selects candidates from already stored DB facts.
- Backend persists a durable ranked batch.
- Moderation stack is a slice from an already-ranked batch.
- Inline "Следующий стек" reads the next configured stack from the same existing ranked batch.
- Inline "Следующий стек" is a UI/control surface, not a Telegram command.
- Inline "Следующий стек" must not run search, enrichment, Hermes ranking, or `youtube.select_candidates`.
- While an active/resumable ranked batch has pending rows, new Curator ranking is blocked.
- Empty Curator selection or zero persisted rows must not be `ok=true` and must not create an active empty success batch.

Guardrail:
Do not restart receipt extraction, Telegram auth, Telegram routing, Hermes auth/provider, or callback debugging from this docs state unless the user explicitly asks for those paths.

Product/docs gap:
The next question is whether docs/roadmap should explicitly define a separate Telegram command for starting ranking, or keep start-ranking as a UI/backend operator action while Telegram only continues moderation and serves inline next stack.

Historical note:
The earlier receipt full extraction block remains historical context and is not the current active pointer.
<!-- CONTEXT_APPEND_END id=CTX_20260529_YOUTUBE_RANKED_BATCH_ACTIVE_STATUS_CORRECTION -->

<!-- CONTEXT_APPEND_BEGIN id=CTX_20260530_YOUTUBE_CANDIDATES_BASE_UI_CLEANUP_AND_MODERATION_SEMANTICS source=chatgpt_dialogue_and_codex_reports -->
APPEND_ID: CTX_20260530_YOUTUBE_CANDIDATES_BASE_UI_CLEANUP_AND_MODERATION_SEMANTICS
SOURCE_KIND: chatgpt_dialogue_and_codex_reports
DATE_UTC: 2026-05-30
STATUS: accepted_current_context
TITLE: YouTube candidates base UI cleanup and moderation semantics update

Summary:
The current active YouTube work continues under the ranked-batch moderation lifecycle, but the visible `База / кандидаты` tab now uses the backend-persisted latest search summary and paginated candidates list instead of all-time DB/debug counters.

Accepted current UI/product state:
- `Загружено в последнем поиске` comes from `latest_search_summary.stored_new_count`.
- If `latest_search_summary` is null, the UI shows `—` / `нет данных` rather than falling back to all-time DB totals.
- `Доступно к ранжированию` comes from `selection_overview.available_for_selection_count`.
- The main visible candidates summary no longer shows provider, all-time loaded total, already-in-selection, available-for-selection wording, ranked total, pending moderation, full-description raw summary rows, DB path, or active batch/debug counters.
- The candidates list uses `limit=10`, `offset`, `has_more`, and prev/next pagination.
- The UI does not request or render 50 rows by default, and it does not accumulate pages into one giant list.
- The backend candidates API still clamps candidate list limit to 20, but the frontend page size is 10.

Accepted ranking/moderation semantics that remain current:
- Sorting counters use `selection_overview.available_for_selection_count` for `Доступно к ранжированию`.
- `Доступно к отправке на модерацию` means `active_batch.counts.pending_count + active_batch.counts.ranked_count`, not just the current visible stack size.
- Future active batches supersede previous active batches and archive old rows.
- Contract sanitizer hardening remains in force: unknown `skipped_video_ids` and `rejected_video_ids` do not abort ranking; unknown `selected_video_ids` still hard-fail; validator remains enabled; no hardcoded video IDs were introduced.
- `/agent-lab/api/youtube/moderation/batches` has a route-specific nginx timeout of 300s for read/send; the broader `/agent-lab/api/` timeout was not globally changed.

Current stop-point:
The docs stop-point remains the YouTube ranked batch moderation lifecycle question, including the open product/docs decision about whether ranking start should be a separate Telegram command or remain a UI/backend operator action while Telegram continues moderation and inline next stack.

Proven latest implementation reference:
The latest UI cleanup commit reported by the code run was `1ba686b1d00e6d9dbe71fddbb0df8f3bf2a20092`.

Guardrail:
Do not restart receipt/OCR context from this block. The current active work is YouTube ranked batch moderation lifecycle plus candidates-base UI semantics.
<!-- CONTEXT_APPEND_END id=CTX_20260530_YOUTUBE_CANDIDATES_BASE_UI_CLEANUP_AND_MODERATION_SEMANTICS -->

---
APPEND_ID: CTX_20260601_POST_YOUTUBE_TG_FIXES_AND_CODEX_RUN_RULES
SOURCE_KIND: chatgpt_dialogue_and_codex_reports
DATE_UTC: 2026-06-01
STATUS: accepted_current_context
TITLE: Post-20260530 YouTube/Hermes/Telegram fixes and Codex run-rule correction

### Summary
After the previously saved YouTube candidate-base UI cleanup and moderation semantics block, the dialogue continued with multiple accepted runtime fixes and process corrections. This block records only new accepted context after the last saved append point.

### Accepted YouTube search/readiness fix
The YouTube search workflow was corrected so `Запусти поиск` is not considered complete when it only stores metadata-only candidates. Search now auto-completes the readiness/enrichment step when needed so candidates become rank-ready.

Accepted proof:
- search through Telegram/Hermes produced real Telegram replies;
- `available_to_rank` increased from `0 -> 10` and then `10 -> 20`;
- `description_full` remains a real business-layer rank-readiness requirement, but search now satisfies it automatically instead of requiring a manual hidden UI step;
- direct route/API/script/DB was not accepted as live proof;
- fallback was not accepted as success.

Accepted implementation reference:
- commit `013deb284a61e2da2cf952060747b8e72b3ede83`.

### Accepted rank-pool consistency fix
The previous mismatch where UI could show enough available candidates while ranking produced fewer than requested was fixed.

Accepted proof:
- runtime target_count was `13`;
- `available_to_rank_before_rank` was `20`;
- rank candidate pool count was `13`;
- `ranked_count` was `13`;
- ranked count matched target;
- proof went through Telegram -> selected agent -> Hermes -> existing YouTube rank action -> business layer -> Telegram reply.

Accepted implementation reference:
- commit `013deb284a61e2da2cf952060747b8e72b3ede83`.

### Accepted cleanup recent-days / Hermes-only proof
Stale non-finalized YouTube candidate cleanup was corrected from “older than N days” to “candidates collected during last N days”.

Accepted semantics:
- `N=1` means candidates collected today;
- `N=2` means today + yesterday;
- this is not “older than N days”;
- cleanup protects approved, rejected, deferred/postponed/move-to-next-time, finalized or explicitly carried-forward candidates.

Accepted live proof:
- dry-run command went through Telegram -> selected agent -> Hermes -> existing YouTube cleanup dry-run action;
- apply command went through Telegram -> selected agent -> Hermes -> existing YouTube cleanup apply action;
- dry-run Telegram message_id: `890`;
- apply Telegram message_id: `891`;
- apply deleted `47` candidates and `29` selection-state rows and updated `6` batch refs;
- no cleanup fallback was used;
- no direct DB/script/route cleanup was used as live proof;
- protected finalized/deferred candidates were preserved;
- service remained healthy and bot status was restored.

Accepted implementation reference:
- commit `2d95c264da9f0da44b369f8b8cea4022e3af776f`.

### Accepted global Telegram/Hermes no-reply fix
A later regression caused the Telegram bot to stop replying to all messages, including `Кто ты?`.

Root cause:
- `process_pending_updates_cycle()` treated any fetched `update_id <= persisted cursor` as duplicate;
- stale cursor state could silence the live poller by skipping real updates;
- live runtime skipped updates instead of resyncing cursor.

Accepted fix:
- duplicate gate now skips only exact repeats;
- lower update IDs can resync the cursor;
- regression tests were added.

Accepted live proof:
- `Запусти модерацию` reached selected agent `plankton`, Hermes returned text, Telegram returned real message_id `909`;
- `кто ты?` reached selected agent `plankton`, Hermes returned text, Telegram returned real message_id `910`;
- reply chain Telegram -> selected agent -> Hermes -> Telegram send was restored.

Accepted implementation reference:
- commit `36d0f6d08c727afc412c9c75e89eac501a14d16e`.

### Process correction: Codex run rules with real chain tests
The user corrected the workflow expectation for Codex runs. Future implementation runs must not stop at code changes or unit tests when the task is runtime/user-flow.

New rule:
- Codex must fix the task and test the real working chain that imitates actual product logic.
- For agent/tool actions, proof must go through the required architecture path, currently often:
  Telegram inbound simulation -> project handler -> selected agent -> Hermes -> existing tool/facade action -> deterministic business layer -> real Telegram reply/message_id.
- Direct route/API/DB/script/manual send is not accepted as live proof.
- A fallback that only imitates success or bypasses Hermes/tool architecture is not accepted.
- If Hermes/provider auth/rate-limit blocks the run, Codex should first use project-owned auth/recovery tools when available, then retry the proper proof path.
- If recovery cannot solve it, Codex must report a true blocker instead of bypassing the architecture.

### Active-context caution
Do not infer the next product stage from a stale historical block alone. Before answering “what is next”, ChatGPT must compare:
- current_status;
- roadmap tail;
- context tail;
- module_map tail;
- project snapshot;
- latest accepted runtime reports in the dialogue.

Kilo/CLI-provider exploration was explicitly canceled by the user and must not be treated as current roadmap work.

Fin Instrument blocks are historical/completed/deferred according to their own accepted statuses and must not be named the next step unless the user explicitly reopens them or current docs/runtime proof says so.

Receipt full extraction remains a saved historical/pending business-layer block, but it is not to be duplicated as a new active pointer by this docs update.

<!-- CONTEXT_APPEND_BEGIN id=CTX_20260601_YOUTUBE_POST_DRAFT_EDITOR_LIVE_GATE_SKELETON source=chatgpt_inline_project_update accepted_by_user=yes -->
## 2026-06-01 — YouTube post draft editor live-gate skeleton

CONTEXT_APPEND_ID: CTX_20260601_YOUTUBE_POST_DRAFT_EDITOR_LIVE_GATE_SKELETON

### Current active block

The current active project block is `youtube.prepare_post_draft`, also referred to as the YouTube Post Draft Preparation Tool.

This block is not Fin Instrument and not receipt extraction. Older receipt/OCR context remains historical only unless the user explicitly returns to that line.

### Product goal

The tool prepares Telegram-ready post drafts from videos that were already selected/approved by the YouTube sorting/moderation pipeline.

The intended product chain is:

1. selected/approved YouTube candidate from sorting/selection;
2. durable post draft shell;
3. durable transcript/subtitle snapshot;
4. protected internal editor-agent contract;
5. fake/injected editor execution adapter;
6. guarded live editor route skeleton;
7. moderation-ready post draft;
8. passive `Готовы к публикации` queue after approval;
9. future publication tool consumes the passive queue later.

Publication is not part of this tool.

### UI/operator-first boundary

The current operator surface is the YouTube tab `Редакторская оценка`.

The user clarified the correct workflow:

- show ready/approved videos that have not yet been edited;
- allow operator checkbox selection;
- operator clicks `Создать посты`;
- drafts are created/reused idempotently;
- moderation/preview/ready-publication blocks exist;
- `Готовы к публикации` is a passive output queue;
- there is no manual `Передать в публикацию` action inside this tool.

### Accepted implementation chain

The following implementation/proof chain is accepted in the current dialogue:

1. Storage/lifecycle foundation:
   - `youtube_post_drafts` exists.
   - draft shell creation is idempotent.
   - current-draft uniqueness exists per candidate.
   - revision path is deliberate.
   - approved selected videos are blocked from re-selection.
   - current tool does not delete source candidate history.

2. Workflow-first operator UI:
   - ready videos can be selected with checkboxes;
   - bulk `Создать посты` exists;
   - `Посты на модерации`, `Предпросмотр поста`, and `Готовы к публикации` blocks exist;
   - future actions are staged/disabled where not implemented.

3. Publication boundary:
   - misleading `Передать в публикацию` UI action was removed.
   - `Одобрить` is the terminal action of this tool.
   - after approval the draft belongs in the passive `Готовы к публикации` output queue.
   - a future publication tool will consume approved/unpublished drafts later.

4. C1 harness-first content chain:
   - explicit stage observability exists for subtitle/editor stages.
   - deterministic harness can produce `draft_text`, `image_brief`, `image_prompt`, and `image_negative_prompt`.
   - harness moves drafts to `ready_for_moderation` / `needs_review`.
   - harness does not approve or publish.

5. C2a transcript snapshot persistence:
   - durable transcript snapshot storage exists.
   - snapshots are linked by `transcript_snapshot_ref`.
   - transcript snapshot payloads are attached without live YouTube/subtitles fetch.
   - missing/invalid transcript state fails safely.

6. C2b-1 editor request/response contract:
   - editor input is built from source facts and stored transcript snapshot.
   - deterministic fake editor contract output exists.
   - validator rejects empty/ungrounded/invalid output.
   - valid output persists post text and image prompt metadata.
   - invalid output does not overwrite prior valid production fields.

7. Protected internal editor agent readiness:
   - `agent-packages/youtube_post_editor_agent/` exists.
   - it is `system_agent=true`, `protected=true`, `non_public=true`.
   - it remains excluded from Telegram/public command registration.
   - runtime profile was created under `/var/lib/openscript-agent-lab/hermes/profiles/youtube_post_editor_agent`.
   - source/runtime profile files were verified by hash/size during repeat-proof.
   - provider defaults now resolve `effective_model="gpt-5.4-mini"`.
   - readiness reached `can_live_execute=True`, but no live call was made.

8. C2b-2A injected fake editor execution adapter:
   - `POST /api/youtube/post-drafts/editor-execute` exists.
   - `mode="fake"` works.
   - `mode="live"` is rejected on the fake route.
   - fake runner is deterministic and non-live.
   - validation is reused before persistence.
   - approval/publication remain untouched.

9. Guarded live route skeleton:
   - `POST /api/youtube/post-drafts/editor-execute-live` exists.
   - it requires `confirm="HERMES_EDITOR_LIVE"`.
   - readiness/source facts/transcript/approved-published guards fail closed before runner call.
   - default/no-runner path returns `live_runner_not_configured` and does not call Hermes/provider/model.
   - injected runner tests prove success/failure state transitions without live execution.
   - UI shows a separate disabled live warning/action.
   - fake route remains unchanged.
   - no live Hermes/provider/model/auth call has been made.

### Current accepted commit references

Current accepted source HEAD for this block:
`bd32dbee9ef9f0ce358f250ee5e69d46229b5384`

Important accepted intermediate commits from the dialogue include:
- `ef498eeea1cbff0291cf5006f8ddb2b3b7c5e66b` — post draft storage/lifecycle foundation repeat-proof.
- `9fc4641471b9a969c34a8b510423d6bc5995e692` — publication handoff removed; passive publication queue semantics.
- `fec59422553f7abc5a7bcc211458d99018ec76ff` — C1 harness chain state.
- `7c466969188d9f8813ba94f0ad1a55dc0c9cafee` — C2a transcript snapshot persistence.
- `0b27dec0baed6a41a7eee41b77ebd1c790457991` — C2b-1 editor contract/fake executor.
- `16b4e6eb326e9755161496f18576172b59635a76` — source internal execution gate.
- `1d1d1a06a94ab8bb0e0332b2ba561284e10490b7` — provider defaults/model mapping readiness.
- `d64e69b68f5ca242c2833be904f4785508d26e25` — injected fake editor execution adapter.
- `bd32dbee9ef9f0ce358f250ee5e69d46229b5384` — guarded live editor route skeleton.

### Current stop-point

The current stop-point is:

Guarded live route skeleton is repeat-proven. The next technical step can only be a separately approved live-smoke proof/design run.

No live Hermes/provider/model call has been attempted yet.

### Next safe step

The next safe step is not an implementation by default. It is a user-approved proof/design for a controlled live-smoke run of `youtube_post_editor_agent` through the guarded live route.

The live-smoke proof/design must specify:
- exact draft/input fixture;
- explicit operator/admin confirmation;
- max one controlled live execution unless otherwise approved;
- no Telegram send;
- no image generation;
- no publication;
- no runtime apply;
- no public exposure;
- validation through the existing C2b-1 validator before persistence;
- safe failure handling;
- report with exact live-call result and whether output was stored.

### Hard boundaries

Do not restart old Telegram/Hermes/auth debugging unless fresh proof shows it is the first broken layer.

Do not resume Fin Instrument or receipt extraction from this active block.

Do not treat `can_live_execute=True` as permission to call a model. It is only readiness state. A live call requires a separate explicitly approved run.
<!-- CONTEXT_APPEND_END id=CTX_20260601_YOUTUBE_POST_DRAFT_EDITOR_LIVE_GATE_SKELETON -->

<!-- CONTEXT_APPEND_BEGIN id=CTX_20260602_YOUTUBE_POST_EDITOR_LIVE_SOURCE_INVISIBLE_SUCCESS source=chatgpt_inline_project_update accepted_by_user=yes -->
## CTX_20260602_YOUTUBE_POST_EDITOR_LIVE_SOURCE_INVISIBLE_SUCCESS

Status: accepted current context append
Date: 2026-06-02
Active block: YouTube post draft editor live workflow

### Summary

The YouTube post draft editor moved from live-gate skeleton to a proven controlled live workflow for the current prepared post draft.

The current working draft proof target was:

- draft_id: `post-draft-6af43220e9bb`
- video_id: `D67SfjYSMok`
- source video title: `AI News: Claude Opus 4.8, Hundreds of AI Agents in Claude Code, How to Spend $500 Million on APIs?`
- channel: `Продуктивный Совет`

The final accepted technical state is not “live route skeleton”. A controlled live editor execution has now succeeded after multiple proof/fix loops, and the draft is persisted for manual review.

### Key proven facts

- The internal protected editor agent is `youtube_post_editor_agent`.
- The editor agent must remain visible for inspection but action-locked for unsafe UI actions.
- Existing ready/working agents must not be touched when configuring the editor agent.
- The editor output must be a standalone editorial/news post, not a recap of the video/channel/host/episode.
- The source video/channel/title/transcript are internal grounding material only.
- Visible `draft_text` must not mention source-reference framing such as:
  - author/host/channel/video/episode/source;
  - `в ролике`;
  - `в выпуске`;
  - `с канала`;
  - `цитата из выпуска`;
  - `автор разбирает`;
  - `канал рассказывает`.
- Grounding is preserved through machine-readable `source_facts_used` and source snapshots, not by forcing source metadata into the visible post text.
- The model may return `source_facts_used` as a dict keyed by canonical grounding keys; backend postprocess now canonicalizes the accepted shape before validation.
- Missing genuine grounding still fails closed.
- The editor draft remains a manual-review artifact: no automatic approval, publication, Telegram send, or image generation is part of the editor live step.

### Important resolved failures

1. The live runner initially failed contract validation because the prompt did not require the full validator contract.
   - Fixed by requiring `draft_text`, image fields, `source_facts_used`, and `style_guard_result`.

2. The editor live execution initially timed out or became too heavy.
   - The live payload was trimmed.
   - Timestamp-heavy transcript text was stripped for live prompt usage.
   - The editor live runner received a bounded longer timeout override.
   - Temporary Hermes timeout/session-correlation diagnostics remain as cleanup debt.

3. Agent training docs existed but were not visible in model context.
   - Fixed by injecting a compact allowlisted training context into the live prompt.
   - Runtime profile docs are preferred, with source-package fallback.
   - The context is bounded and secret-safe.

4. The text formatting/newline issue was not model/storage/API loss.
   - Model output, parser, storage, and API preserved multiline text.
   - UI CSS collapsed whitespace in preview surfaces.
   - Fixed in UI/CSS only.

5. The source-invisible agent training initially conflicted with backend prompt/validator.
   - Backend prompt and validator required visible candidate title, channel name, and transcript excerpt.
   - This forced `Выпуск ... с канала ...` and `Цитата из выпуска`.
   - Fixed by removing literal visible-source requirements while preserving `source_facts_used` grounding.

6. The last validation failure was caused by `source_facts_used` shape handling.
   - The model returned `source_facts_used` as a dict of canonical keys with values.
   - Validator treated non-list source_facts_used as empty.
   - Fixed by canonicalizing dict/list/scalar outputs in postprocess when request grounding is complete.

### Final successful live state

Run:
`OPENSCRIPT_AGENT_LAB_YOUTUBE_POST_EDITOR_ONE_LIVE_EXECUTION_AFTER_SOURCE_FACTS_USED_FIX_REFRESH_20260602_01`

Source HEAD:
`3047fb23c403428057466c44929a6f92dd74feac`

Result:

- exactly one live execution was attempted;
- no retry loop;
- validation passed;
- `source_facts_used` was accepted as canonical grounding keys;
- the regenerated draft was persisted;
- final `draft_status`: `ready_for_moderation`;
- final `moderation_status`: `needs_review`;
- `approved_at=null`;
- `published_at=null`;
- `publication_status=null`;
- no Telegram send;
- no image generation;
- no publication;
- no draft approval.

Output quality flags from the final proof:

- `text_is_standalone_news_not_video_recap=true`
- `news_items_expanded_beyond_topic_listing=true`
- `forbidden_source_reference_phrases_present=false`
- `text_contains_numbered_or_bulleted_list=true`
- `image_brief_present=true`
- `image_brief_is_collage_or_composite=true`
- `image_prompt_present=true`
- `image_prompt_is_collage_or_composite=true`
- `ready_for_manual_review=true`

The final draft preview begins as a standalone AI news digest, for example:
`На этой неделе ИИ-рынок снова показал, что главное соревнование идёт не за красивые демо, а за то, кто научится превращать модели в рабочую инфраструктуру...`

### Current stop-point

The next step is manual UI review of the generated draft text.

Do not run more live editor calls before the user reviews the full draft text in the UI.

If the user accepts the text, the next technical block may be controlled illustration generation through the project workflow using the saved `image_brief`, `image_prompt`, and `image_negative_prompt`.

Do not generate images through ChatGPT chat for this workflow.

If the user rejects the text, use the concrete final draft content as proof and adjust the editor agent/prompt path narrowly. Do not reintroduce visible source metadata requirements and do not add validator gates that block manual-review drafts.

### Cleanup debt

Temporary Hermes timeout/session-correlation diagnostics are still present.
They should be reduced to a bounded production-safe summary only after the editor path is accepted by manual review.

### Not current

The older receipt full extraction block remains historical/pending, but it is not the current active block unless the user explicitly switches back to receipts.

Telegram/auth/Hermes routing must not be reopened for this editor path unless a fresh proof shows the first failing step moved there.
<!-- CONTEXT_APPEND_END id=CTX_20260602_YOUTUBE_POST_EDITOR_LIVE_SOURCE_INVISIBLE_SUCCESS -->
<!-- CONTEXT_APPEND_BEGIN id=CTX_20260604_YOUTUBE_POST_DRAFT_MODERATION_REVISION_FLOWS source=chatgpt_inline_project_update accepted_by_user=yes -->
## CTX_20260604_YOUTUBE_POST_DRAFT_MODERATION_REVISION_FLOWS

### Scope
This append records the current OpenScript Agent Lab working context after the last saved docs point `CTX_20260602_YOUTUBE_POST_EDITOR_LIVE_SOURCE_INVISIBLE_SUCCESS`.

The active block is now the YouTube post-draft moderation/editor pipeline, not receipt extraction, Telegram auth, Hermes auth, or Fin Instrument UI.

### Completed/proven since last saved point

1. Controlled YouTube post illustration pipeline progressed from fail-closed internal slice to live direct Codex image generation.
   - Direct Codex imagegen backend was implemented and proven with real draft smoke.
   - Production prompt source is `youtube_post_drafts.image_prompt`.
   - Stored `image_prompt` is passed through unchanged to image generation.
   - No OpenAI API/FAL/Hermes gateway provider key path is the current image path.
   - Direct Codex imagegen path is the accepted working path for current YouTube illustrations.

2. Runtime illustration asset preview was implemented and fixed.
   - Runtime image asset refs are served through a safe preview route.
   - Browser path prefix mismatch under `/agent-lab/` was fixed.
   - A stale live service process previously caused 404 until `openscript-agent-lab-ui.service` restart loaded current source.

3. Approved sorting candidates can feed the post editor queue.
   - Old/finalized candidates must be excluded.
   - Approved active candidates without draft are eligible for editor processing.
   - Processing one candidate moves it out of the editor waiting queue.
   - Queue counts must represent current waiting items, not historical approved totals.

4. One-candidate full editor pipeline was operator-tested.
   - Candidate `NJg4_3qUHPY` / title `It's a disease...` was processed into `post-draft-2479cdb8ffb4`.
   - Draft text, image generation, deterministic Russian title overlay, caption validation, and Telegram moderation card send were executed.
   - The draft stayed not approved and not published.
   - The candidate was finalized/used after processing.

5. Telegram post-draft moderation card shape was corrected.
   - Moderator must see the post as it will be released.
   - Correct moderation card is one Telegram photo message:
     image + caption + inline buttons.
   - No separate “additional text” message is acceptable for a release-shaped post.
   - Caption limit is enforced; overlong captions block/send to text revision rather than splitting.

6. Caption compression / release text sizing was added.
   - Photo caption must fit Telegram caption limit.
   - Current target is caption-sized final post text, preferred under the limit with readable paragraph formatting.
   - Silent truncation and split fallback are not acceptable.

7. Telegram moderation callbacks and durable acknowledgements were improved.
   - Post-draft moderation and sorting/candidate moderation callbacks now have visible chat confirmations.
   - Popup-only `answerCallbackQuery` is not enough.
   - Sorting approval confirmation must include current editor-waiting count.
   - Post approval confirmation must include current publication-waiting count.
   - Counts must decrease when the next tool consumes the item.
   - Historical approved rows must not inflate current waiting counts.

8. Sorting moderation durable confirmation live gap was fixed.
   - A helper signature mismatch around `message_thread_id` prevented sorting durable confirmation in one live path.
   - Sorting approval now sends the durable chat message with editor-waiting count when the candidate exists and is valid.
   - A previously attempted old candidate was missing from DB and should not be used as proof of current path failure.

9. Approved post revision guard was added and live-confirmed.
   - If a draft is already `approved_for_publication` / publication-ready, text/image revision actions must be blocked unless the moderator explicitly returns the draft to work.
   - Regeneration must not start on approved/publication-ready drafts.
   - Approved draft remains in publication queue.
   - Durable blocked message:
     `Пост уже одобрен к публикации. Правки невозможны; верните пост в работу, если нужна доработка.`
   - This was later live-confirmed by the user.

10. Editorial quality fixes were applied to YouTube editor skills.
   - Raw source/video/author framing was removed from final Telegram post style.
   - Final post must be a standalone Russian Telegram post, not a raw video summary.
   - Single-topic post needs a headline and coherent flow.
   - News/roundup mode must remain preserved and separate.
   - Codex must not delete or weaken the already tuned news/roundup behavior while improving single-topic editorial style.

11. Deterministic Russian title overlay was improved.
   - Base image generation should not attempt to render text.
   - Overlay title is deterministic post-processing.
   - Overlay title must be Russian and meaningful.
   - Raw English clickbait fragments such as `It's disease` are not acceptable.
   - Overlay title must not include emoji.

12. Emoji policy was improved.
   - Final Telegram caption should use semantic, variable emoji.
   - Headline should start with a relevant emoji.
   - Emoji should structure paragraphs/sections, not appear randomly mid-sentence.
   - Emoji pattern must not be fixed across posts.
   - News/roundup mode remains preserved.
   - Overlay titles remain emoji-free.
   - Last reported accepted semantic emoji policy commit: `6beadd03e56de2dcf49bd9724fc36e7ae77fceb8`.
   - Latest target draft after this run: `post-draft-2479cdb8ffb4`, moderation message `952`.

### Current active stop-point

The current unresolved block is revision execution for a fresh, non-approved post-draft moderation card.

Latest screenshot/evidence in the dialogue showed:
`✏️ Запрошены правки текста. Черновик поставлен на текстовую доработку.`

Therefore the next technical run must not assume image revision. The next technical run should first target text revision flow unless fresh proof shows the image action was clicked.

### Correct next technical block

Implement/prove text revision flow for a non-approved post draft:

`Запросить правки текста`
→ editor rewrites caption only
→ caption remains <= Telegram photo caption limit
→ image refs remain unchanged
→ title overlay image remains unchanged
→ resend/replace full Telegram moderation card:
   same titled image + new caption + same buttons
→ draft remains not approved and not published.

### Not next

Do not proceed next to:
- image revision flow, unless fresh callback/log/screenshot proves the `image` action was clicked;
- publication queue;
- publication tool;
- processing another candidate;
- Telegram auth/Hermes auth;
- receipt OCR/full extraction;
- Fin Instrument UI.

### Important lesson from the dialogue

Do not misread screenshot evidence:
- If screenshot says `✏️ Запрошены правки текста`, the evidence is text revision request, not image revision request.
- Do not write prompts claiming the user clicked “Запросить новую иллюстрацию” unless the fresh evidence actually shows that action.
- Always state the exact visible Telegram message before choosing the next prompt.

### Source/layer boundaries for next work

Likely source areas for the next text revision flow:
- `agent_lab/youtube_post_draft_moderation_dispatch.py`
  - callback action handling and resend/replace moderation card.
- `agent_lab/youtube_post_draft_service.py`
  - draft text revision, caption validation, lifecycle.
- `agent-packages/youtube_post_editor_agent/skills/telegram_editorial_writer.md`
  - editorial policy already improved; read only if prompt composition requires it.
- `agent-packages/youtube_post_editor_agent/rules.md`
  - read only if text revision prompt must reuse editor rules.

Read-only / do-not-touch unless fresh proof requires it:
- `agent_lab/youtube_post_illustration_service.py`
- `agent_lab/youtube_post_codex_imagegen_runtime.py`
- `agent_lab/youtube_image_title_overlay.py`
- Telegram auth/provider/Hermes paths.
<!-- CONTEXT_APPEND_END id=CTX_20260604_YOUTUBE_POST_DRAFT_MODERATION_REVISION_FLOWS -->
## CTX_20260605_YOUTUBE_POST_DRAFT_REVISION_REPEAT_PROOF_AND_TELEGRAM_INTAKE_STATUS
Status: accepted current context append
Date: 2026-06-05
Source kind: ChatGPT dialogue + Codex reports after CTX_20260604_YOUTUBE_POST_DRAFT_MODERATION_REVISION_FLOWS

### Active block
The active block remains `youtube.prepare_post_draft`, specifically the YouTube post-draft moderation/revision pipeline.

This block is not:
- receipt extraction;
- Fin Instrument UI;
- Telegram auth/Hermes auth unless fresh proof shows it is first broken;
- publication;
- approval workflow;
- generic Telegram listener work.

### What has been completed/proven since the previous saved point

1. Text revision flow progressed beyond the earlier request-only state.

Accepted source/runtime sequence included:
- request stage was separated from completion stage;
- old-card resend on request click was removed;
- real text revision completion path was added;
- explicit text revision completion markers were added:
  - `text_revision_completed_at`;
  - `text_revision_completed_for_requested_at`;
- `moderation_sent_at >= revision_requested_at` is no longer sufficient completion proof;
- stale requested state without explicit completion marker retries the editor path;
- completion marker is per-cycle, not a permanent lock;
- a completed text revision no longer blocks future text revision requests;
- fresh click after completed cycle starts a new revision cycle;
- repeated text revision cycles were proven through the runtime flow.

Important accepted implementation references from this dialogue branch:
- `413ed76e4abd7147bdd27a4f8845cab9c9dabed4` — real text revision completion path.
- `ad7b596552bf68c02270e5ea4e8cbec16332397f` — explicit text revision completion marker.
- `acaf72b5c77af80d4d82a1285e9bf5fb64f7031b` — fresh revision cycle after completion.
- `fafad3226f303b0f871f60243bea5ff3724a979e` — nested source_facts grounding normalization.
- `9ac59e9c7358f5f530f3732d021bc94d12b69aaa` — text revision grounding normalization cleanup.

2. Text caption style/formatting was corrected.

Accepted state:
- dense regenerated captions are deterministically reflowed/normalized into readable paragraph groups;
- editor rules/skills were tightened for Telegram-readable captions;
- grounding validation remains strict;
- missing required grounding still fails;
- valid nested `source_facts_used` is normalized into required canonical keys;
- repeated text revision remains supported;
- text-only revision preserves the same titled image.

Proof evidence accepted in dialogue:
- repeated text cycles produced real moderation message transitions `982 -> 984 -> 986`;
- recorded paragraph counts included 6 and 5;
- same titled image remained for text-only revision.

3. Image/illustration revision flow progressed and repeat proof was accepted.

Accepted state:
- image revision creates fresh `image_asset_ref`;
- titled overlay image regeneration creates fresh `image_titled_asset_ref`;
- titled image preview support was added in UI;
- repeated illustration regeneration was proven;
- text/caption remained valid through image-only cycles.

Important accepted implementation references:
- `b123831` — live post-draft image revision flow fix.
- `9287473` — regenerate titled image assets on base image changes.
- `de40b115e141870292710171446c69b515b88a2e` — titled image preview support.

Accepted live proof:
- illustration cycle 1 changed image refs and moved moderation message `990 -> 992`;
- illustration cycle 2 changed image refs again and moved moderation message `992 -> 994`;
- both cycles used the existing dispatch path and real Telegram connector;
- no shortcut/manual send/fake message_id was accepted.

4. Dirty working tree after interrupted runs was normalized by scope.

Accepted cleanup commits:
- `9ac59e9c7358f5f530f3732d021bc94d12b69aaa` — text revision grounding normalization.
- `de40b115e141870292710171446c69b515b88a2e` — titled image preview support.
- `a76371c6f867ece52474d2b8d10defd292fd610f` — Telegram connector control audit logging.

Remaining dirty/untracked files were classified as unrelated to the YouTube post-draft live proof path and not blockers, provided they remain untouched.

5. Telegram polling/intake state was diagnosed.

Accepted facts:
- live manual Telegram callback proof initially failed because polling was disabled and the bot was paused;
- official control path `POST /api/telegram/mode` with `{"bot_status":"enabled"}` was used to enable runtime intake;
- after that, state became:
  - `bot_status=enabled`;
  - `live_enabled=true`;
  - `polling_worker_active=true`;
  - `ready_for_live_polling=true`;
- polling cycle count advanced, but later observation windows still did not capture real manual `callback_query`.

Important boundary:
- No new Telegram listener was written and none should be written.
- Existing owner remains the project polling path in `agent_lab/telegram_polling.py`.

6. Request timing and image backend failure surfacing were fixed.

Accepted implementation reference:
- `ce34fd2b70a10c4a64f9b3180d05637d8a02a67e` — request status timing and image failure surfacing.

Accepted changes:
- request-status Telegram message is sent immediately after `answerCallbackQuery` and before long text/image generation work;
- final moderation card remains completion-only;
- raw `codex exec failed` from image backend is mapped to a safe provider-failure message;
- failed image generation sets a safe retryable failure state;
- `codex_imagegen_cli` backend failure remains a backend failure and is not treated as success.

Service state reported after this fix:
- service restarted from PID `1275620` to `1339657`;
- healthz OK;
- source HEAD and origin/main matched `ce34fd2b70a10c4a64f9b3180d05637d8a02a67e`.

### Current unresolved stop-point
The current unresolved stop-point is not the text revision business layer and not the image revision business layer.

Latest proof after `ce34fd2...` stopped because no real manual `callback_query` was observed during the observation window, even though service was healthy and polling ready.

Therefore the next correct technical block is:

`youtube_post_draft_manual_callback_identity_current_card_proof`

Goal:
- remove ambiguity around real Telegram inline clicks by creating or refreshing one current moderation card through the existing project-owned moderation delivery path;
- record the fresh `moderation_message_id`;
- ask the user to click exactly the inline button on that fresh card/message id;
- prove whether a real `callback_query` arrives for that exact message id;
- if callback arrives, trace route/dispatch;
- if callback does not arrive, identify whether the first broken layer is wrong bot/card/chat, webhook/getUpdates conflict, offset/intake issue, or Telegram client/card mismatch.

### What is closed and must not be re-debugged without fresh proof
Do not restart these as next work:
- text revision completion markers;
- text fresh-cycle repeat behavior;
- caption grounding normalization;
- caption paragraph formatting;
- repeated illustration lifecycle;
- titled image ref regeneration;
- Telegram bot pause/enabled control path;
- image backend raw `codex exec failed` surfacing;
- unrelated dirty file cleanup already handled by scope.

### What is not next
Not next unless fresh proof shows it is first broken:
- new Telegram listener;
- Telegram auth/Hermes auth;
- receipt/OCR;
- Fin Instrument;
- publication tool;
- approval queue implementation;
- direct DB cleanup;
- another candidate/draft;
- direct service/business proof.

### Hard run-rule reminders accepted in this dialogue
For future runtime/user-flow tasks:
- unit tests alone are not acceptance;
- direct route/API/curl is not live proof;
- direct Python service call is not live proof;
- direct DB write is not live proof;
- manual Telegram send is not live proof;
- fake message_id is not live proof;
- UI/Chromium click is not live proof;
- fallback after Hermes/provider failure is not accepted if the task required Hermes/tool path;
- Codex must not add shortcuts that only pass tests;
- source changes require tests/compile/checks/commit/push;
- runtime proof requires deployed source when applicable;
- if Hermes/provider auth/rate-limit blocks a required tool path, use project-owned recovery helpers first, then retry; only a proven unrecoverable blocker may be HARD_BLOCKER.
END_CONTEXT_APPEND_TEXT
<!-- CONTEXT_APPEND_BEGIN id=CTX_20260605_YOUTUBE_POST_DRAFT_REVISION_REPEAT_PROOF_AND_TELEGRAM_INTAKE_STATUS source=chatgpt_inline_project_update accepted_by_user=yes -->
<!-- CONTEXT_APPEND_BEGIN id=CTX_20260608_CODEX_IMAGEGEN_FIXED_AND_CARD_REFRESHED source=chatgpt_runtime_proof accepted_by_user=yes -->

## 2026-06-08 — YouTube post-draft image generation fixed and moderation card refreshed

Resolved state:
- direct Codex image-generation backend now uses the prompt-based `$imagegen` contract
- the obsolete `--enable image_generation` invocation was removed
- image generation completed successfully for `post-draft-2479cdb8ffb4`
- fresh `image_asset_ref` and `image_titled_asset_ref` were written
- Telegram moderation card was refreshed through the existing product-owned resend path
- moderation message id changed from `1007` to `1008`
- no approve/publish action happened

Next open design topic:
- Codex Toolchain Guard

Purpose of next design topic:
- prevent regressions caused by Codex binary drift, version drift, feature-list drift, invocation-contract drift, or auth-readiness drift

<!-- CONTEXT_APPEND_END id=CTX_20260608_CODEX_IMAGEGEN_FIXED_AND_CARD_REFRESHED source=chatgpt_runtime_proof accepted_by_user=yes -->

<!-- CONTEXT_APPEND_BEGIN id=CTX_20260608_YOUTUBE_PREPARE_POST_DRAFT_TOOL_EDITOR_QUEUE_PROVEN source=chatgpt_inline_project_update accepted_by_user=yes -->

## CTX_20260608_YOUTUBE_PREPARE_POST_DRAFT_TOOL_EDITOR_QUEUE_PROVEN

SOURCE_KIND: chatgpt_dialogue_delta_verified_against_repo_docs
DATE_UTC: 2026-06-08
ACTIVE_BLOCK: youtube_prepare_post_draft_attachable_tool_editor_queue_proven
PREVIOUS_SAVED_BLOCK_SUPERSEDED: youtube_post_draft_manual_callback_identity_current_card_proof
DOCS_UPDATE_RUN_ID: OPENSCRIPT_AGENT_LAB_DOCS_UPDATE_YOUTUBE_PREPARE_POST_DRAFT_TOOL_EDITOR_QUEUE_20260608_01

### Current stop-point

The current OpenScript Agent Lab active work has moved from the 2026-06-05 manual callback identity/intake blocker to the YouTube prepare-post-draft attachable tool line.

The latest proven stop-point is:

* `youtube.prepare_post_draft` is a public attachable tool for normal agents.
* `youtube_post_editor_agent` is an internal/system editor agent inside that tool, not the tool id and not the recipient agent.
* The active recipient agent used in proof is `plankton`.
* `plankton` has `youtube.prepare_post_draft` in source package and runtime profile.
* The UI manual attach block exists in `Ютуб → Редакторская оценка`.
* Hermes can call the model-visible tool `youtube_prepare_post_draft` from a simulated Telegram message routed to `plankton`.
* The action `list_ready_drafts` now returns categorized post-draft lifecycle buckets.
* The new action `list_editor_queue` now returns both upstream ready-for-creation YouTube candidates and existing post-draft lifecycle buckets.

Manual Telegram review of the final delivered message remains the natural acceptance check, but no further code change was required by the latest report.

### Proven implementation sequence after the 2026-06-05 docs point

#### Image/text revision and moderation callback work

The earlier docs stop-point expected proof of real callback identity/current card intake. After this point the dialogue progressed through the post-draft moderation/revision area:

* Text revision request flow was already proven before the 2026-06-05 docs update.
* Image revision work later proved that Telegram intake and moderation resend were not the first broken layer.
* The image generation bottleneck was in the Codex imagegen backend/completion path.
* Artifact-first completion was added so a valid requested PNG artifact can be accepted even if textual last-message/path parsing is weak.
* A later fix restored resend target resolution by passing callback-derived Telegram delivery binding into the resend dispatcher.
* The live repeat illustration flow then delivered a refreshed moderation card with a real Telegram message id.
* A separate timing proof showed a long 525s run was caused by slow image/provider runtime inside synchronous Codex exec, not overlay, Telegram resend, or artifact detection.

These facts are historical context only. They must not cause future runs to reopen Telegram callback intake, moderation resend, or image artifact completion without fresh proof.

#### Approval / return-to-work DB lifecycle

The approval/return lifecycle was also clarified:

* Approve does not publish.
* Approve transitions the durable draft row to:

  * `draft_status=approved_for_publication`
  * `moderation_status=approved_for_publication`
  * `publication_status=ready`
  * `approved_at` set
  * `published_at=null`
* Return-to-work / reject / needs-changes does not delete draft/source rows.
* Return-to-work preserves candidate/video identity and durable draft state.
* Source candidates/videos remain durable and must not be deleted by cancel/return actions.
* Manual approve was later verified in DB for `post-draft-2479cdb8ffb4` with `publication_status=ready` and `published_at=null`.

Future work must keep the distinction:

* approval = ready for future publication;
* publication = separate future tool/action;
* return-to-work = durable state transition, not deletion.

#### Correct tool architecture

A major correction happened around tool identity:

Wrong framing rejected:

* `youtube_post_editor_agent` is not the public tool id.
* The public tool must not be attached to `youtube_post_editor_agent` as the normal recipient.
* Old tools such as Fin, YouTube search, subtitles, and select/sort were reference patterns only; they must not be changed as the target.

Correct framing accepted:

* `youtube.prepare_post_draft` is the public attachable tool.
* `youtube_post_editor_agent` is an internal/system editor agent inside `youtube.prepare_post_draft`.
* Normal agents receive `youtube.prepare_post_draft` through source package `tools.json` + skill + runtime apply.
* The deterministic business layer owns storage, lifecycle, source snapshots, image adapter calls, moderation state, and queue handoff.
* Hermes/agent owns language, style, explanation, and editorial reasoning only through the tool contract.

#### Hermes callable path

The initial source attach attempt correctly stopped because source package `tools.json` + skill alone would have been fake availability.

A Hermes-facing callable wrapper was then added:

* wrapper file: `tools/hermes_vendor_overlay/hermes-agent/tools/youtube_prepare_post_draft_tool.py`
* public tool id: `youtube.prepare_post_draft`
* model-visible callable name: `youtube_prepare_post_draft`
* initial safe actions exposed:

  * `prepare_draft_from_selected_video`
  * `read_post_draft`
  * `list_ready_drafts`
  * `show_source`
  * `approve_for_publication`
  * `return_to_work`
* deferred actions at that time:

  * `regenerate_text`
  * `regenerate_image`
  * `package_moderation_preview`
* commit reference: `1f010e2c5654d98ea933e9e96500b14d1e9c2279`

The callable wrapper path was added without modifying old tools, without provider/model/Telegram calls, and without production DB mutation.

#### Source attach and runtime apply

The source-package attach layer was implemented:

* registry/source attach metadata exists for `youtube.prepare_post_draft`;
* temporary recipient package proof passed;
* generated skill file: `youtube-prepare-post-draft-tool.md`;
* old tools were unchanged;
* no real package was mutated in that source attach proof;
* commit reference: `c33649167a6070f19b9ee1a8938932a6b230faaa`.

Runtime apply dry-run later proved that source `tools.json` and skill copy safely into a Hermes runtime profile while preserving:

* `memories/`
* `sessions/`
* `logs/`
* `auth.json`
* `.env` when present.

The active agent was then proven as `plankton` from project state:

* admin state selected agent was `plankton`;
* Telegram router active agent was `plankton`;
* `plankton` was a normal agent, not a system/internal agent.

The tool was attached and runtime-synced for `plankton`:

* source package:

  * `agent-packages/plankton/tools.json`
  * `agent-packages/plankton/skills/youtube-prepare-post-draft-tool.md`
* runtime profile:

  * `/var/lib/openscript-agent-lab/hermes/profiles/plankton/.agent-lab/tools.json`
  * `/var/lib/openscript-agent-lab/hermes/profiles/plankton/skills/youtube-prepare-post-draft-tool.md`
* commit reference: `0eb41e88efc4a34fb0e8cca2bf192d983fd9143c`

Runtime profile was updated by the project apply path, not by direct manual edit.

#### Manual UI attach control

The operator UI now has a manual attach block in the YouTube post-draft/editorial workflow:

* UI surface: `Ютуб → Редакторская оценка`
* label shown to user: `Подключение youtube.prepare_post_draft`
* selected agent shown: `plankton`
* status shown: connected and applied
* skill doc shown: exists
* Hermes apply shown: not required
* button state: already connected
* commit reference: `1492963be5a7a1a6bba8ad7fc64e4b9ab3e8b116`

Manual UI screenshot confirmed the block is visible and correctly reports `plankton` as already connected/applied.

This UI block is operator convenience only. It is not proof that Hermes calls the tool.

#### Hermes model visibility and forced tool choice

A simulated Telegram proof initially showed:

* Telegram handler worked;
* selected agent was `plankton`;
* Hermes/provider ran;
* real Telegram delivery occurred;
* but the model saw only old tools:

  * `youtube_search_candidates`
  * `youtube_select_candidates`
  * `youtube_subtitles_get`

Root cause:

* `youtube.prepare_post_draft` was registered and present in schema, but `agent_reply.py` only forced tool choices for receipt, search, and select flows.
* Explicit prepare-post-draft requests were left to model choice and could be answered as if the tool were unavailable.

Fix:

* `agent_reply.py` now detects explicit prepare-post-draft requests.
* It forces model tool choice to `youtube_prepare_post_draft` when the toolset is enabled.
* Public/source id remains `youtube.prepare_post_draft`.
* Model-visible function name remains `youtube_prepare_post_draft`.
* commit reference: `a00871ac39965200578b4c2d9e292b116effbfa1`

Proof:

* simulated Telegram message reached `plankton`;
* Hermes invoked;
* tool call attempted;
* action `list_ready_drafts`;
* business layer reached;
* real Telegram delivery message id reported;
* no DB mutation;
* no publication;
* no fallback.

#### Draft lifecycle definition and `list_ready_drafts`

The term “черновик” was clarified.

A post draft is not only “ready for publication”. It is a durable row in `youtube_post_drafts` with lifecycle buckets.

The lifecycle proof found live state:

* total rows: 3
* current rows: 3
* `draft_status=approved_for_publication(3)`
* `moderation_status=approved_for_publication(3)`
* `publication_status=ready(3)`
* `published_at NULL=3`
* UI also showed 2 upstream ready-for-creation candidates.

Previous bug:

* `list_ready_drafts` was hard-coded to the moderation queue only:

  * `ready_for_moderation`
  * `needs_review`
  * `published_at NULL`
* Therefore it returned empty even when 3 drafts were ready for publication.

Fix:

* service function added: lifecycle bucket listing in `youtube_post_draft_service.py`;
* `youtube_prepare_post_draft_tool.py` action `list_ready_drafts` now returns categorized buckets:

  * `all_drafts`
  * `editable_drafts`
  * `needs_work_or_regeneration`
  * `in_moderation`
  * `ready_for_publication`
  * `published_drafts`
  * `failed_or_blocked_drafts`
* live counts after fix:

  * `all_drafts=3`
  * `editable_drafts=0`
  * `needs_work_or_regeneration=0`
  * `in_moderation=0`
  * `ready_for_publication=3`
  * `published_drafts=0`
  * `failed_or_blocked_drafts=0`
* commit reference: `9bb0987308b21760fa5ae6cdbb59017ccb3ada3f`

Proof:

* simulated Telegram message reached `plankton`;
* Hermes called `youtube_prepare_post_draft`;
* action `list_ready_drafts`;
* business layer reached;
* Telegram reply delivered with real message id;
* no DB mutation;
* no publication.

#### Full editor queue and `list_editor_queue`

The user clarified that the UI had two distinct layers:

1. Upstream ready videos/candidates waiting for post creation/editing.
2. Existing post drafts already in `youtube_post_drafts`.

`list_ready_drafts` correctly belongs to the draft lifecycle layer only.
A new read-only action was added for the full editor work queue:

* action: `list_editor_queue`
* tool: `youtube.prepare_post_draft`
* model-visible callable: `youtube_prepare_post_draft`
* service owner: `youtube_post_draft_service.py`
* combines:

  * `ready_for_creation_candidates`
  * existing draft lifecycle buckets

Live/proven counts:

* `ready_for_creation_count=2`
* `current_draft_count=3`
* `ready_for_publication_count=3`
* `total_work_items=5`

Files changed in this final action:

* `agent-packages/plankton/skills/youtube-prepare-post-draft-tool.md`
* `agent_lab/agent_reply.py`
* `agent_lab/storage.py`
* `agent_lab/tool_registry.py`
* `agent_lab/youtube_post_draft_service.py`
* `tests/test_agent_reply.py`
* `tests/test_prepare_post_draft_tool.py`
* `tests/test_storage.py`
* `tests/test_youtube_post_draft_service.py`
* `tool-registry/tools.json`
* `tools/hermes_vendor_overlay/hermes-agent/tools/youtube_prepare_post_draft_tool.py`

Runtime apply was run because the active agent skill changed:

* dry-run first;
* live apply after clean plan;
* no direct runtime profile edit.

Final proof:

* simulated Telegram message;
* route selected `plankton`;
* Hermes called `youtube_prepare_post_draft`;
* action `list_editor_queue`;
* tool output included:

  * `ready_for_creation_candidates=2`
  * `ready_for_publication=3`
  * `current_draft_count=3`
* business layer reached;
* Telegram connector delivered real message id `1037`;
* no DB mutation;
* no publication;
* no fallback;
* old tools unchanged.
* commit reference: `02a154e04c841a92c1a24bfc8acdc429d7256b13`

### Current active block

`youtube_prepare_post_draft_attachable_tool_editor_queue_proven`

### Current accepted state

Accepted/proven:

* `youtube.prepare_post_draft` exists as a public attachable tool.
* `youtube_post_editor_agent` is internal/system only.
* Active agent `plankton` has the tool in source and runtime.
* UI manual attach block is visible in `Ютуб → Редакторская оценка`.
* Hermes model visibility is fixed through forced tool choice for explicit prepare-post-draft requests.
* `list_ready_drafts` returns categorized post-draft lifecycle buckets.
* `list_editor_queue` returns full editor queue:

  * upstream ready-for-creation candidates;
  * post-draft lifecycle buckets.
* Proof uses the required chain:

  * simulated Telegram message
  * Telegram handler
  * selected agent
  * Hermes
  * existing tool/facade action
  * deterministic business layer
  * Telegram delivery proof.
* Real Telegram delivery was reported for the final proof.

### Current not-closed / next human check

The natural remaining check is manual review of the Telegram message delivered by the final proof, especially message id `1037`, to confirm that the user-visible response shows:

* ready-for-creation candidates: 2
* current drafts: 3
* ready-for-publication drafts: 3
* total work items: 5

Do not declare the user-visible scenario accepted without user confirmation if the user is actively checking Telegram/UI.

### Correct next technical block

If user accepts the final Telegram response, the next technical block should be chosen explicitly by the user.

Likely next blocks:

1. `youtube_prepare_post_draft_ready_candidate_creation_flow`

   * create post drafts from the 2 ready-for-creation candidates;
   * mutating action;
   * requires proof/design and DB lifecycle guard;
   * must not publish.
2. `youtube_prepare_post_draft_publication_tool_design`

   * only if user explicitly asks to move toward publication;
   * publication remains a separate future tool, not part of `youtube.prepare_post_draft`.
3. UI polish for the `Редaktorская оценка` queue display;

   * only if user requests it;
   * not a substitute for business/tool proof.

Not next by default:

* receipt/OCR;
* Fin Instrument;
* Telegram auth/provider;
* Hermes auth;
* old YouTube search/subtitles/select tools;
* publication;
* image generation timeout tuning;
* callback identity proof from 2026-05-05;
* ranking start command documentation question.

### Hard invariants added or reinforced

* Do not use `youtube_post_editor_agent` as the public tool id.
* Do not attach external tools to `youtube_post_editor_agent` as if it were a normal recipient unless a separate internal need is proven.
* Do not treat `tools.json` + skill as sufficient proof of callable Hermes availability.
* Do not count UI-visible tool status as proof of model tool-call.
* Do not accept a runtime/tool task unless it proves the full chain through simulated Telegram or equivalent project-owned inbound handler when the user flow requires it.
* Do not call direct Python, curl/API, DB write, shell script, or fallback path as final proof for agent/tool tasks.
* Do not publish from `youtube.prepare_post_draft`.
* Approve means ready for future publication, not published.
* Return-to-work preserves durable DB rows and candidates.
* `list_ready_drafts` is draft lifecycle only.
* `list_editor_queue` is full editor work queue: ready candidates plus draft buckets.
* Old YouTube tools remain independent:

  * search;
  * subtitles;
  * select/sort.
* Business facts and lifecycle buckets belong in `youtube_post_draft_service.py` / deterministic layer, not in prompt text or UI-only logic.

<!-- CONTEXT_APPEND_END id=CTX_20260608_YOUTUBE_PREPARE_POST_DRAFT_TOOL_EDITOR_QUEUE_PROVEN source=chatgpt_inline_project_update accepted_by_user=yes -->

## CTX_20260610_TELEGRAM_PUBLICATION_TWO_BOT_AND_ADMIN_TRIGGER_READY
SOURCE_KIND: chatgpt_dialogue_delta_verified_against_repo_docs
DATE_UTC: 2026-06-10
ACTIVE_BLOCK: telegram_publication_admin_live_send_trigger_source_ready_pending_main_integration
PREVIOUS_SAVED_BLOCK: youtube_prepare_post_draft_attachable_tool_editor_queue_proven

### Scope
This append records the current OpenScript Agent Lab working context after the repo-docs saved point `CTX_20260608_YOUTUBE_PREPARE_POST_DRAFT_TOOL_EDITOR_QUEUE_PROVEN`.

The active block is now Telegram Publication / TG poster controlled live-send enablement, not YouTube editor queue, receipt extraction, Fin Instrument, Hermes auth, or Telegram Router restoration.

### Completed/proven since the last saved point

1. Telegram Publication / TG poster tool integration reached main.
- `telegram.publication` exists as a Hermes-visible tool.
- Safe actions are:
  `list_configs`, `list_jobs`, `list_ready_materials`, `list_logs`, `ingest_ready_materials`, `plan_queue_dry_run`.
- The tool remains no-live-send.
- Main integration commit for the tool line:
  `b7be7c9b4eb56813a576fd5f5f5637dd92309681`.

2. Old Telegram Router bot was restored and later superseded by split-token proofs.
- The old Router bot path was proven through inbound Telegram -> handler -> router -> selected agent -> response send.
- Later token split and secret migration proofs supersede the original restoration proof.

3. YouTube stuck editor/moderation continuation blocker was closed.
- Source and runtime reached:
  `3d6c840a1a364560cef56571aae2400a8af32356`.
- Existing stuck draft evidence:
  `post-draft-80c04bfaf644`.
- The fix resumed from persisted editor output and stored transcript snapshot.
- `text_generation_rerun` was `no`.
- `editor_status` advanced from `pending` to `succeeded`.
- image generation completed through `codex_imagegen_cli`.
- moderation was sent with real Telegram moderation message id `1059`.
- This closed the YouTube continuation blocker. It must not be reopened without fresh proof.

4. Telegram two-bot token split was implemented and integrated.
- Final main commit for token split:
  `c47f2c62be26998c7f1c6de9d3ab0185cd65b49e`.
- Router token policy:
  `TELEGRAM_ROUTER_BOT_TOKEN` is preferred;
  `TELEGRAM_BOT_TOKEN` is legacy Router fallback only.
- Publication token policy:
  `TELEGRAM_PUBLICATION_BOT_TOKEN` is required;
  publication must not fall back to Router or legacy token.
- Missing publication token fails closed with redacted error.
- Metadata is presence-only; no token values, hashes, fingerprints, or env dumps.

5. Runtime deploy of the token split was proven before secret migration.
- Runtime deployed to:
  `c47f2c62be26998c7f1c6de9d3ab0185cd65b49e`.
- Legacy Router fallback proof succeeded after deploy.
- Proof message:
  `PING_AFTER_TOKEN_SPLIT_DEPLOY_20260610`.
- Real Telegram reply message id:
  `1061`.

6. Runtime secret migration to two bot roles completed.
- Env file path:
  `/etc/openscript-agent-lab/telegram.env`.
- Backup was created:
  `/etc/openscript-agent-lab/telegram.env.bak.20260610T144210Z`.
- Runtime env key names after migration:
  `TELEGRAM_BOT_TOKEN`;
  `TELEGRAM_ROUTER_BOT_TOKEN`;
  `TELEGRAM_PUBLICATION_BOT_TOKEN`.
- Token values were not printed.
- Env was not dumped.
- Service restarted healthy.

7. Post-migration Router proof succeeded.
- Proof message:
  `PING_AFTER_SECRET_MIGRATION_20260610`.
- The Router selected `plankton`.
- Real Telegram reply message id:
  `1063`.
- This proves the old Router bot still works after the split-token secret migration.

8. Publication config proof passed without live send.
- `TELEGRAM_PUBLICATION_BOT_TOKEN` presence was proven redacted.
- `telegram.publication` registry/wrapper/skill visibility was proven.
- Live publication send was not attempted.

9. Live Publication send design identified the real blocker.
- Runtime was healthy.
- Publication target config existed, redacted.
- Dry-run/preview paths existed.
- Durable proof fields existed.
- Existing live-send functions were internal business-layer functions only.
- Admin endpoints stopped at settings/status.
- Hermes-visible tool was intentionally no-live-send.
- Result:
  `HARD_BLOCKER_NO_SAFE_PRODUCT_SEND_PATH`.

10. Admin/product live-send trigger source branch is ready.
- Source branch:
  `feature/telegram-publication-admin-live-send-trigger-20260610-agent1`.
- Source commit:
  `481fa4ee4ce862245142144098629dbf7094b91e`.
- Commit title:
  `Add Telegram publication admin run-cycle trigger`.
- New endpoint:
  `POST /api/telegram-publication/run-cycle`.
- Endpoint defaults to preview/dry-run and does not send unless `confirm_live_send: true`.
- First live proof is capped to one post through `max_posts=1`.
- Endpoint calls the existing business-layer run-cycle/send-execution path.
- Endpoint does not call Telegram API directly.
- Endpoint does not read token values directly.
- Publication token resolution remains in send-execution.
- Publication does not use Router token.
- Hermes tool remains no-live-send.
- Response redacts secrets and returns durable proof fields.
- Tests and diff checks passed in the feature branch.
- No runtime deploy or live send was done for this source branch.

### Current stop-point
The correct current stop-point is:
`telegram_publication_admin_live_send_trigger_source_ready_pending_main_integration`.

The branch `feature/telegram-publication-admin-live-send-trigger-20260610-agent1` is ready, but not integrated into `origin/main`.

### Correct next technical run
Next run should integrate source commit:
`481fa4ee4ce862245142144098629dbf7094b91e`

Expected main before integration:
`c47f2c62be26998c7f1c6de9d3ab0185cd65b49e`.

The run must be source integration only:
- no runtime deploy;
- no service restart;
- no env/token changes;
- no live endpoint call;
- no Telegram send.

### Not next
The following are not next unless fresh proof changes the active block:
- redo YouTube continuation/editor/moderation work;
- redo old Router token restoration;
- redo token split implementation;
- redo secret migration;
- live publication send before source integration and runtime deploy/proof;
- direct Telegram API call;
- direct Hermes/tool call;
- internal business-layer function call as product proof;
- removal of legacy `TELEGRAM_BOT_TOKEN`;
- Fin Instrument/receipt/OCR.

### Invariants
- Telegram Router and Telegram Publication are separate roles.
- Router uses `TELEGRAM_ROUTER_BOT_TOKEN`, with `TELEGRAM_BOT_TOKEN` only as legacy fallback.
- Publication uses `TELEGRAM_PUBLICATION_BOT_TOKEN` only.
- `telegram.publication` Hermes tool remains no-live-send.
- Live publication proof must use the normal admin/product endpoint after integration and deploy.
- Runtime target/channel/token details remain runtime configuration, not source constants.
- Telegram message ids recorded in this append are proof evidence only, not implementation constants.

## 2026-06-14 — Telegram Publication admin trigger source integrated, pending runtime proof

Current active block:

`telegram_publication_admin_trigger_source_integrated_pending_runtime_proof`

Source integration completed:

* private source commit `fcde3149e4baa0ba6a01664e1ba029da0e1399f4` is now on `origin/main`;
* only these four source/test files were committed:

  * `agent_lab/admin_server.py`
  * `agent_lab/telegram_publication_run_cycle.py`
  * `tests/test_admin_server.py`
  * `tests/test_telegram_publication_run_cycle.py`
* the endpoint source contract remains:

  * `POST /api/telegram-publication/run-cycle` exists;
  * preview/dry-run is the default path;
  * `confirm_live_send: true` is required for live send;
  * first live proof remains capped to `max_posts=1`;
  * the endpoint delegates to `telegram_publication_run_cycle.run_telegram_publication_run_cycle`;
  * the run-cycle layer delegates to `telegram_publication_send_execution.run_telegram_publication_send_execution`;
  * the endpoint does not call Telegram API directly;
  * the endpoint does not read or print token values;
  * the endpoint does not hardcode agent, user, chat, provider, or message id values;
* `telegram.publication` Hermes tool remains no-live-send;
* runtime deploy, restart, live-send, and env/token changes were not performed;
* the frontend/auth repo was not touched and belongs to another agent/repo;
* unrelated untracked pollution remains and is not part of this docs run:

  * `agent-packages/**`
  * `tools/hermes_vendor_overlay/hermes-agent/tools/fin_receipt_tool.py`
  * `.venv-hermes/**`
  * `**/__pycache__`
  * `vendor/**`
* new stop-point:

  * source is integrated, but runtime/product proof is still pending;
* recommended next run:

  * proof_only source-vs-runtime / endpoint availability check;
  * verify whether the running service exposes `POST /api/telegram-publication/run-cycle`;
  * no live send;
* no Telegram API call;
* no deploy/restart unless a later explicitly approved deploy run is created;
* if endpoint is absent in runtime, stop and propose a separate deploy/restart design/proof.

## 2026-06-14 — Telegram Publication live proof success, pending preview/live selection stability

SOURCE_KIND: chatgpt_dialogue_delta_verified_against_repo_docs
DATE_UTC: 2026-06-14
ACTIVE_PHASE: telegram_publication_live_proof_success_pending_preview_live_selection_stability
PREVIOUS_PHASE_SUPERSEDED: telegram_publication_admin_trigger_source_integrated_pending_runtime_proof

### Context update

- the one-post Telegram Publication live proof succeeded through the normal admin/product endpoint;
- `live_send_executed` was `true`;
- `jobs_sent` was `1`;
- `jobs_published` was `1`;
- `telegram_message_id` was `8`;
- approved unpublished drafts were ingested through `agent_lab.telegram_publication_ready_materials.ingest_ready_materials`;
- three publication jobs were created;
- the runtime target summary remained safe and non-secret: `@openscriptwibe via @EditorWaib_bot`;
- no direct Telegram API call was made by Codex;
- no Hermes live-send was used;
- no source edits, deploys, restarts, or secret exposure occurred in this docs run;
- the frontend/auth repo was not touched;
- tracked source tree remained clean;
- unrelated untracked pollution remains untouched.

### Follow-up issue

- preview selected job id:
  `telegram-publication-job:v1:a81eed31baa9d5c5eb8b3643bc97fa89d959c2dfe7830ad9654f5df3557c52de`
- live sent job id:
  `telegram-publication-job:v1:7f8de8ded4b92c0e09a640345a34041fa2b0886b058f4ff6cfe7c352f2857c10`
- preview/live selection should be stabilized so the approval step can name the exact same job identity before execution.

### Current active block

`telegram_publication_live_proof_success_pending_preview_live_selection_stability`

### Recommended next run

- a proof-only or fix run to add deterministic preview-to-live selection identity (`selected_job_id`, `preview_plan_id`, or equivalent) and prove preview/live operate on the same job before any future live-proof approval.

## CTX_20260615_YOUTUBE_EDITOR_SKILL_SELECTION_EXPERIENCE_AND_FRESH_PIPELINE_RESTART_READY

Status: appended from ChatGPT dialogue
Active block: `youtube_editor_skill_selection_experience_documented_then_fresh_pipeline_restart`
Related document: `docs/codex_source/project/youtube_post_editor_skill_selection_experience_20260615.md`

### New proven context

After the Telegram Publication media live proof was documented, the active YouTube/Post Publisher work continued through a full Hermes/operator-style editorial pipeline experiment.

The following facts are newly relevant and should be available for future ChatGPT/Codex runs:

1. A one-time DB cleanup was performed earlier in the dialogue and preserved published history while clearing active selection/draft/publication work items for a fresh YouTube chain.
2. A fresh YouTube candidate moderation run was performed through Hermes/operator flow.
3. Telegram moderation cards were delivered to the operator flow.
4. Three candidate drafts were generated and sent for moderation.
5. Image/title overlay layout was iterated. The accepted direction is:
   - title remains on the illustration;
   - image base and title overlay remain separate;
   - the title is applied by Python script overlay, not baked into the generated base image;
   - the lower-third title plate layout is currently acceptable enough to proceed.
6. The main unresolved quality work became the `youtube_post_editor_agent` writing quality.

### Editor skill-selection experience

The project tried multiple editor skill directions:
- `talkstream/ru-text`
- `coreyhaines31/marketingskills` social/copywriting/copy-editing
- `ilyautov/humanizer-ru`
- `Stahlwalker/developer-marketing`
- `ComposioHQ/content-research-writer`
- `conorbronsdon/avoid-ai-writing`

Main lesson:
The issue is not simply “bad style”. The editor must first transform source material into one editorial angle before writing the Telegram post.

### Important proof

A proof run showed that `regenerate_text_requested` does not rewrite old draft text as its main input. It builds an editor-contract request from:
- `source_facts_snapshot`
- `transcript_snapshot`
- `editorial_constraints`
- `editorial_rules`
- `grounding`

Old `draft_text` is not part of the request; it is used only after the model returns for no-op comparison/update logic.

Therefore repeated weak output was not caused by source starvation or old draft reuse.

### Current editor stop-point

The latest source-to-angle skill update was applied to runtime and text-only regeneration delivered new moderation cards:
- `post-draft-aa6589f0fe2c` -> Telegram moderation message `1148`
- `post-draft-bc7a951fa811` -> Telegram moderation message `1150`
- `post-draft-a2dc0520ab53` -> Telegram moderation message `1152`

The user judged the current result acceptable enough to proceed, but not as a final editorial-quality solution.

### What is closed

Closed/proven:
- text regeneration uses source/transcript, not previous draft as main input;
- source-to-angle is the correct next editor direction;
- editor diagnostics must remain advisory, not blocking;
- image/title overlay is not the same problem as writing quality;
- `youtube.prepare_post_draft` still must not publish;
- publication remains a separate business/tool path;
- future user-facing steps must still go through Hermes/tool/operator flow.

### What is not closed

Not closed:
- final high-quality Russian Telegram editorial voice;
- stable taste calibration for the internal editor;
- accepted corpus of good/bad Telegram post examples;
- committing/reconciling all dirty source changes from the editor-skill iteration;
- a fresh full YouTube pipeline run after documentation update.

### Current next desired sequence

The user requested:
1. First, document the editor-skill selection experience and update repo docs.
2. Then, in a separate later run, repeat the previous safe cleanup + fresh pipeline maneuver:
   - clean active DB work items safely, preserving history/published proofs;
   - run fresh search/selection/moderation through Hermes/operator flow;
   - generate new drafts through `youtube.prepare_post_draft`;
   - review in Telegram moderation;
   - do not publish without explicit approval.

### Not next

Not next:
- publication;
- direct Telegram API shortcuts;
- manual SQL without an explicitly approved cleanup run;
- provider/model calls in docs update;
- image overlay redesign;
- new random skill search before using the recorded lessons;
- blocking editorial quality gates;
- application code edits inside docs-only run.

## CTX_20260615_YOUTUBE_EDITOR_SKILL_SELECTION_DOCS_COMPLETED_FRESH_PIPELINE_NEXT

Status: appended from ChatGPT dialogue
Corrects: `CTX_20260615_YOUTUBE_EDITOR_SKILL_SELECTION_EXPERIENCE_AND_FRESH_PIPELINE_RESTART_READY`
Active block: `youtube_fresh_pipeline_restart_after_editor_skill_docs_completed`
Related document: `docs/codex_source/project/youtube_post_editor_skill_selection_experience_20260615.md`

### Correction

The YouTube editor skill-selection experience has now been documented in repo docs and pushed to both the private source repo and public docs repo.

The previous active blocker:
`editor_skill_selection_experience_not_yet_documented`

is closed.

### Current active block

Current active block is now:
`youtube_fresh_pipeline_restart_after_editor_skill_docs_completed`

### Current stop-point

The project is ready for a separate technical run that repeats the previous safe cleanup + fresh YouTube pipeline maneuver.

That future run must:
- clean only active/current YouTube selection/draft/publication work items;
- preserve published history and proof rows;
- preserve documentation and skill-selection experience;
- run fresh YouTube search/selection/moderation through Hermes/operator flow;
- generate new drafts through `youtube.prepare_post_draft`;
- deliver Telegram moderation cards;
- not publish without explicit approval.

### Not part of this docs correction

This docs correction does not run:
- DB cleanup;
- YouTube search;
- candidate selection;
- draft generation;
- provider/model calls;
- Telegram delivery;
- publication;
- runtime apply;
- application code changes.

### Guard for the next technical run

The next technical run must start with proof/current-state checks before cleanup:
- inspect active YouTube candidate batches/selections/drafts/publication jobs;
- preserve published history;
- prove what will be marked inactive/cleared before any mutation;
- do not use broad destructive SQL;
- use the previously accepted cleanup pattern only after explicit scope proof;
- no direct Telegram API shortcuts;
- no publication in the same run unless separately approved.
