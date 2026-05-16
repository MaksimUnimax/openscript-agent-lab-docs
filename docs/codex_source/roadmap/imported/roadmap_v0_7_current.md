# Current roadmap import - v0.7 actual state

STATUS: IMPORTED_NORMALIZED_CURRENT
CURRENT_VERSION: v0.7 append-only final Telegram voice success
SOURCE_KIND: inline roadmap content from ChatGPT prompt
IMPORTANT: This inline content is the source for this run. Do not look for uploaded files.

## 1. Roadmap lineage

### 1.1. Roadmap v0.2 - historical original product draft

Roadmap v0.2 described the original standalone "Расходы с характером" Telegram expense bot.

Original product:
- Telegram bot;
- receipt photo/OCR;
- SQLite expense storage;
- manual text expense input;
- natural-language expense questions;
- character/personality answers;
- Russian language;
- RUB currency;
- Telegram as MVP messenger.

Status:
- Historical product origin.
- Superseded by the Hermes-first Agent Lab architecture.
- Still useful as product intent for the first applied scenario.
- Not the current architecture roadmap.

Important constraints from v0.2:
- Heavy local LLM must not be mandatory for MVP.
- Voice and local LLM are later phases.
- Business logic and expense storage must not depend on one unstable AI model.
- Tokens, private data and DB files must not be stored in git.

### 1.2. Roadmap v0.3 - pivot to Hermes-first Agent Lab

Roadmap v0.3 captured the architectural pivot away from a standalone Expense Bot and unstable OpenRouter Free Pool.

Current architectural direction introduced:
- OpenScript Agent Lab becomes the main project.
- Hermes-first line accepted.
- Agent and provider are independent axes.
- Business layer remains deterministic.
- Old expense-bot becomes historical/reference unless separate extraction/refactor task says otherwise.

Canonical decisions:
- Do not build the product around OpenRouter Free Pool.
- Codex is one possible provider/resource branch, not the whole product.
- System must support unlimited agents.
- No hardcoded one-agent/four-agent architecture.
- Each agent has source package.
- Each agent has Hermes runtime profile.
- Provider switching must not rewrite agent documents such as SOUL.md.
- Agent must not write SQL, count money, mutate DB, see secrets, or run shell from user text.
- Agent may help with language, character, explanation, clarification and safe text understanding.

### 1.3. Roadmap v0.4 - product layer rebuild / Agent Management / UI correction

Roadmap v0.4 captured the rebuild after old overloaded Agent Lab UI/product paths were rejected.

Still canonical:
- Agent is a product entity.
- Source package is separate from Hermes runtime profile.
- Provider/Auth is separate from agent.
- Telegram Router is separate from diagnostics.
- Business layer is separate from LLM/agent.
- Runtime profile is not source-of-truth.
- UI edits source package.
- Runtime apply/diff syncs source package to runtime.
- Runtime must preserve auth.json, .env, memories, sessions and logs.
- No symlinks for SOUL.md/config.yaml.
- Agent Lab must never write /root/.codex/auth.json.
- API keys are write-only and must not appear in UI/logs/reports.
- Do not return simulation-response as a product path.
- Do not return response preview as product layer.
- Do not use "Проверить ответ агента" as Telegram product path.
- Offline route-test is not live Telegram routing.

### 1.4. Roadmap v0.5 - Hermes runtime / tools / voice package foundation

Roadmap v0.5 captured that Hermes was no longer only "documents in prompt"; it became a separate execution line.

Done by v0.5:
- Hermes dry-run adapter.
- Agent Lab binding mapper.
- Official Hermes auth import.
- no-tools Hermes smoke.
- response capture.
- registry-driven tools model.
- global tool registry.
- per-agent schema v2 bindings.
- runtime mirror/snapshot.
- read-only Tools tab.
- voice.telegram as registry-driven tool package.
- output sendVoice proof.
- STT plumbing proof.
- disabled input download skeleton.

Still canonical:
- Hermes runtime path must stay separate from direct Codex fallback.
- Tools are permissions.
- Skills are instructions/requirements.
- Skills never grant tool access.
- Unknown tools are blocked.
- New tools are disabled by default.
- agent-packages/** dirty state is user/pre-existing and must not be staged without explicit decision.

Superseded:
- v0.5 active next step "Slice B getFile/download proof gate" is now historical and no longer active. The project moved far beyond it.

### 1.5. Roadmap v0.6 - Telegram voice / universal Hermes / auth UI

Roadmap v0.6 captured the state after Telegram voice work had reached universal Hermes path but was blocked by auth.

Important v0.6 facts:
- Telegram voice input was no longer skeleton.
- Internal raw Telegram file_id was saved privately.
- Public file_id was masked.
- Real download was proven.
- .oga -> .ogg normalization was added.
- Real local STT through proven venv was proven.
- Transcript object was proven.
- Transcript handoff adapter was proven.
- Polling voice branch was proven.
- Real reply boundary no-send proof happened.
- Telegram text send connection was connected.
- Old voice path reached Telegram send.

Universal Hermes path state in v0.6:
voice → download → STT → selected agent → profile → skills → memory/history → Hermes provider call

v0.6 active blocker at that time:
openai-codex provider call → 401 token_invalidated

v0.6 process/auth rules remain canonical:
- DOCUMENTATION_BASELINE is mandatory in every Codex prompt.
- Abstract prompts are forbidden.
- Codex CLI auth and Hermes OAuth are different stores.
- Codex CLI store: /root/.codex/auth.json
- Hermes auth store: /root/.hermes/auth.json
- metadata found is not active auth.
- token shape is not active auth.
- auth file exists is not active auth.
- Codex CLI auth alone is not Hermes active.
- 401 token_invalidated means not active.
- Live auth active means the same Hermes/openai-codex provider path used by live reply succeeds without 401.
- Old direct path and fallback are forbidden for live reply.

Superseded:
- v0.6 active auth blocker is superseded by v0.7 because official import/adopt recovery fixed it and final voice proof succeeded.

### 1.6. Roadmap v0.7 - current actual roadmap state

Roadmap v0.7 is the current actual roadmap state.

Current version:
Roadmap v0.7 - append-only final Telegram voice success

Status:
- Current.
- Supersedes v0.6 as active status.
- Telegram voice / universal Hermes path block is complete by server-side proof.
- Do not continue auth/voice/send fixes unless a new proof shows a new issue.

## 2. v0.7 - Hermes openai-codex auth blocker resolved

Design decision:
OFFICIAL_IMPORT_PATH_AVAILABLE

Fix run:
OPENSCRIPT_AGENT_LAB_HERMES_CODEX_AUTH_RECOVER_IMPORT_ADOPT_FIX_20260516_01

Result:
SUCCESS

Commit:
1cbd08a4230e812c8b05024f7c4a4c72a524c761
Refine Hermes auth recover import adopt

What changed:
- auth-recover now uses official Hermes import/adopt path from existing Codex CLI auth.
- Cloudflare-blocked device-code start is no longer used as automatic recovery path.

Recovery path:
- /root/.codex/auth.json
- official Hermes import/adopt
- /root/.hermes/auth.json
- live Hermes/openai-codex readiness probe

Proof after fix:
auth-recover:
- ok=true
- status=recovered
- imported_from_codex_cli=true
- live_auth_ok=true

auth-check:
- status=live_ok
- status_label=Авторизация активна
- live_auth_ok=true

Checks:
- python3 -m compileall /opt/openscript-agent-lab/agent_lab
- python3 -m unittest -q tests.test_admin_server
- openscript-agent-lab-ui.service active
- /healthz 200 OK

Status:
Hermes/openai-codex auth blocker RESOLVED by proof.

## 3. v0.7 - Final Telegram voice through universal Hermes path accepted

Final voice proof run:
OPENSCRIPT_AGENT_LAB_FINAL_VOICE_AFTER_AUTH_SUCCESS_NO_REPLY_DIAGNOSIS_20260516_01

Result:
SUCCESS

Proven:
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

State evidence:
- last_seen_update_id: 255681809
- last_processed_update_id: 255681809
- last_route.decision: eligible_for_voice_pipeline
- last_reply.reply_generated: true
- last_send.delivered: true
- answer_sent_to_Telegram: true

Conclusion:
Fresh voice after auth success completed end-to-end in persisted runtime state.

## 4. v0.7 - Delivery visibility proof

Delivery proof run:
OPENSCRIPT_AGENT_LAB_TELEGRAM_DELIVERED_BUT_USER_NOT_VISIBLE_DIAGNOSIS_20260516_01

Result:
PASS

Inbound voice:
- update_id: 255681809
- message_id: 154
- chat_id: 286...139
- selected_agent_slug: runtime_apply_smoke_20260507

Outbound send:
- telegram_send_success: true
- delivered: true
- telegram_message_id: 155
- same inbound chat_id by construction:
  _send_message(token, safe_update.get("chat_id"), reply_text)

Additional facts:
- No duplicate suppression involved.
- No thread/topic metadata persisted or passed.
- No discrepancy found in persisted runtime state.

Conclusion:
- Server-side delivery to same chat_id is proven.
- If the user still does not see message_id=155, remaining gap is Telegram client/chat view, not local voice/STT/Hermes/auth/send pipeline.

## 5. Current status after v0.7

Done / accepted by proof:
- Telegram voice is received.
- Internal raw file_id is available.
- Public file_id remains masked.
- Download/STT path works.
- Transcript reaches the same text path.
- Universal selected-agent Hermes path is used.
- Selected agent runtime_apply_smoke_20260507 was used for the proof case.
- Package/profile/skills/memory load.
- Provider openai-codex succeeds after official import/adopt auth recovery.
- answer_created=yes.
- Telegram send succeeds.
- telegram_message_id=155 is recorded.
- Delivery to same inbound chat_id is proven.

Resolved blockers:
- 401 token_invalidated after universal Hermes path: resolved by official import/adopt recovery.
- false auth-check live_ok: fixed earlier; live_ok now accepted only after live readiness proof.
- false auth-recover already_valid: fixed earlier.
- Cloudflare-blocked device-code UI recovery: no longer used as automatic recovery path.
- public 502: resolved by starting canonical openscript-agent-lab-ui.service.

Remaining notes / not active blockers:
- unrelated agent-packages/** dirty state remains present and untouched.
- If user does not visually see Telegram message_id=155, that is not reflected in server-side persisted runtime state.
- Thread/topic metadata is not persisted or passed on this delivery path; no current proof of topic mismatch, but also no topic telemetry.

## 6. Current next roadmap direction

Current Telegram voice / universal Hermes path block is complete by server-side proof.

Next technical step should not be another auth/voice/send fix unless a new proof shows a new issue.

Possible next blocks:
1. Normal Telegram text regression proof through the same universal Hermes path.
2. Optional delivery telemetry improvement: persist redacted thread/topic/message delivery metadata if Telegram topic visibility needs future debugging.
3. Move to the next planned roadmap block after Telegram voice acceptance.

Important:
- Do not send Codex a roadmap update task by default.
- Assistant should update roadmap/context append-only in chat/files.
- Codex should receive only the next narrow technical task when needed.

## 7. Current import status after this run

After this roadmap import, the following should be true:
- actual roadmap is imported;
- current roadmap version is v0.7;
- actual ТЗ v0.3 is already imported;
- normalized working context is already imported;
- Hermes vendor docs are already imported;
- Telegram vendor docs are already imported;
- rules pack is still pending import;
- module map/safe boundaries is still pending import;
- prompt templates are still pending import if needed;
- main feature work still paused until rules and module map imports are complete;
