# Roadmap

STATUS: INITIAL_FROM_CURRENT_REPO_DOCS

This file is append-only.

Do not rewrite historical blocks destructively.

<!-- ROADMAP_APPEND_BEGIN id=RM_20260516_0001 -->
Repo documentation foundation:
- source-of-truth docs exist under `docs/codex_source/**`
- Hermes vendor docs were extracted
- Telegram vendor docs were extracted
- the project docs / memory layer is being created
- main ТЗ work is paused until repo docs/memory and GitHub visibility are in place
<!-- ROADMAP_APPEND_END id=RM_20260516_0001 -->

<!-- ROADMAP_APPEND_BEGIN id=RM_20260516_PUBLIC_DOCS_VISIBILITY -->
## 2026-05-16 — Public docs repository is visible

Status: DONE

Facts:
- Private source repo was pushed successfully.
- Public docs-only repo was created and exported.
- Public docs repo contains only `docs/codex_source/**`.
- ChatGPT verified web visibility of `ENTRYPOINT_FOR_CHATGPT.md`.
- A stale HEAD reference in the entrypoint/current docs was corrected.

Next:
- Import actual user-provided ТЗ / roadmap / rules / context / module map.
- Keep imports append-only where required.

<!-- ROADMAP_APPEND_END id=RM_20260516_PUBLIC_DOCS_VISIBILITY -->

<!-- ROADMAP_APPEND_BEGIN id=RM_20260516_IMPORTED_ROADMAP_V0_7_CURRENT source=chatgpt_inline_roadmap accepted_by_user=yes -->

## 2026-05-16 — Imported actual roadmap v0.7 as current roadmap state

### Source

This roadmap import was based on inline roadmap content provided directly in the Codex prompt.
Codex did not need uploaded ChatGPT files.

### Current roadmap version

Current actual roadmap is:

`Roadmap v0.7 — Append-only final Telegram voice success`

v0.7 supersedes v0.6 as the active status.

### Roadmap lineage

- v0.2: historical standalone Expense Bot roadmap.
- v0.3: pivot to Hermes-first Agent Lab.
- v0.4: product layer rebuild, no simulation-response, Agent/source/runtime/provider/business separation.
- v0.5: Hermes runtime/tools/voice.telegram foundation.
- v0.6: Telegram voice + universal Hermes + auth UI blocker state.
- v0.7: final Telegram voice / universal Hermes path server-side success.

### Current accepted proof

Telegram voice / universal Hermes path is complete by server-side proof:

- auth-check before voice: live_ok
- fresh_voice_seen: yes
- selected_agent_slug: runtime_apply_smoke_20260507
- voice_receive_enabled: true
- transcript_handoff_enabled: true
- internal_file_id_available: yes
- recognized: yes
- provider_call_success: yes
- answer_created: yes
- telegram_send_success: yes
- telegram_message_id: 155

Delivery to the same inbound chat_id is also proven.

### Resolved blockers

- 401 token_invalidated after universal Hermes path: resolved by official import/adopt recovery.
- false auth-check live_ok: fixed earlier; live_ok accepted only after live readiness proof.
- false auth-recover already_valid: fixed earlier.
- Cloudflare-blocked device-code UI recovery: no longer used as automatic recovery path.
- public 502: resolved by starting canonical openscript-agent-lab-ui.service.

### Remaining notes

- unrelated agent-packages/** dirty state remains present and untouched.
- if user does not visually see Telegram message_id=155, this is not reflected in server-side persisted runtime state.
- thread/topic metadata is not persisted or passed on the delivery path; no current proof of topic mismatch, but also no topic telemetry.

### Current next roadmap direction

Do not continue auth/voice/send fixes unless a new proof shows a new issue.

Possible next blocks:
1. Normal Telegram text regression proof through the same universal Hermes path.
2. Optional redacted delivery telemetry for thread/topic/message metadata if Telegram topic visibility needs future debugging.
3. Move to the next planned roadmap block after Telegram voice acceptance.

Before main feature work continues, still import:
- rules pack;
- module map / safe boundaries;
- prompt templates if needed.

<!-- ROADMAP_APPEND_END id=RM_20260516_IMPORTED_ROADMAP_V0_7_CURRENT -->

<!-- ROADMAP_APPEND_BEGIN id=RM_20260516_EXPAND_TZ_FIN_TOOL_TAB_AGENT_FARM_AND_AGENT_TOOLS source=chatgpt_inline_product_update accepted_by_user=yes -->

## 2026-05-16 — Product direction expanded: “Фин инструмент”, Agent Farm and Agent Tools

### Context

The user clarified the next project direction and corrected the UI placement.

The financial tool must not be created as a separate new tab.

The current UI tab named “Телеграмм” is already specialized around the financial agent workflow, Telegram input and voice. It should become the “Фин инструмент” tab.

This is a documentation/product-direction update only.
No implementation is included in this update.

### Current priority order

1. Re-evaluate the Telegram user_id allowlist task card:
   - include placement in the current “Телеграмм” tab, to be renamed/treated as “Фин инструмент”.

2. Close access to the Telegram bot:
   - Telegram user_id allowlist UI/access control;
   - deny unknown users before resource use;
   - use from.id/user_id, not chat_id, as identity;
   - place this in “Фин инструмент”.

3. Build the universal Agent Farm:
   - many agents;
   - separate agent tasks;
   - task runtime;
   - task assignment;
   - execution tracking;
   - monitoring of completion/failure/repair needs.

4. Add first major agent business tool:
   - Financial Agent Business Tool;
   - not just a database;
   - database + scripts + receipt ingestion + reports + safe tool contract;
   - financial agents must call this tool and must not write SQL directly;
   - product surface belongs under “Фин инструмент”.

5. Add future tool families:
   - Telegram Post Publisher Agent/Tool;
   - YouTube Parsing Agent/Tool;
   - Additional task tools TBD.

### Status

- “Фин инструмент” tab direction: PLANNED / NEEDS_TASK_CARD_REEVALUATION / NEEDS_DESIGN / NEEDS_PROOF.
- Telegram user_id allowlist: pending task-card re-evaluation.
- Agent Farm / Task Runtime: PLANNED / NEEDS_DESIGN / NEEDS_PROOF.
- Financial Agent Business Tool: PLANNED / NEEDS_DESIGN / NEEDS_PROOF.
- Telegram Post Publisher: PLANNED / NEEDS_DESIGN / NEEDS_PROOF.
- YouTube Parser: PLANNED / NEEDS_DESIGN / NEEDS_PROOF.
- Other future tools: PLANNED_PLACEHOLDER / NEEDS_SPEC.

### Rules

- Do not create a separate new tab for the financial tool if the current “Телеграмм” tab is the intended financial tool surface.
- Do not implement Agent Farm before closing bot access and completing proof/design.
- Do not implement Financial Tool as a raw DB exposed to agents.
- Do not let agents write SQL or mutate DB directly.
- Do not mix Telegram access-control with Telegram post publishing.
- Do not implement YouTube parsing without separate vendor/legal/API docs proof.
- Do not mark any new tool family DONE from this docs update.

### Next step

Still next:
- task-card re-evaluation for `telegram_user_id_allowlist_ui`;
- the re-evaluation must include the “Фин инструмент” tab placement/rename decision.

After allowlist:
- design/proof for Agent Farm / Task Runtime.

<!-- ROADMAP_APPEND_END id=RM_20260516_EXPAND_TZ_FIN_TOOL_TAB_AGENT_FARM_AND_AGENT_TOOLS -->

<!-- ROADMAP_APPEND_BEGIN id=RM_20260517_WORKFLOW_RULES_RISK_BASED_COMBINED_RUNS source=chatgpt_inline_user_clarification accepted_by_user=yes -->

## 2026-05-17 — Workflow optimization: risk-based combined runs

The project workflow is updated to reduce unnecessary Codex runs.

Old default:
- separate proof/design before most fixes.

New default:
- docs-only runs remain docs-only;
- narrow ordinary fixes may use combined proof/design/fix in one run;
- high-risk or unclear tasks still require separate design approval.

For the Telegram user_id allowlist line:
- after task-card readiness, prefer a guarded combined proof/design/fix run if scope is narrow;
- if exact affected modules are unclear or high-risk paths are involved, STOP before editing.

<!-- ROADMAP_APPEND_END id=RM_20260517_WORKFLOW_RULES_RISK_BASED_COMBINED_RUNS -->
