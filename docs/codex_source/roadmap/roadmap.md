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
