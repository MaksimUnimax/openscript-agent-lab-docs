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
