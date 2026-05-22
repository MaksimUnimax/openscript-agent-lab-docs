# PROJECT SNAPSHOT

STATUS: BOUNDED_CODEX_REPO_SNAPSHOT
SOURCE_KIND: bounded_codex_repo_snapshot
SNAPSHOT_ID: PROJECT_SNAPSHOT_20260522_YOUTUBE_SEARCH_AGENT_VISIBILITY_FIXED
DATE_UTC: 2026-05-22T05:59:40Z

## Git State

- private source repo HEAD at snapshot: `df3a3b009132ada4ff3ada75178a97e46fd2a686`
- current branch: `main`
- `origin/main` matched `HEAD` before docs edits
- working tree status: dirty outside docs only
- dirty summary: unrelated tracked/untracked changes exist outside docs; none were staged for this docs run
- docs-only snapshot scope: `docs/codex_source/**` only
- no auth files were read
- no secrets were printed

## Current Project Snapshot

- YouTube subtitles tool: implemented, UI-connected, attachable, Telegram-proven
- YouTube search/intake: implemented and operator-proven
- Full-description enrichment: implemented as separate stage over saved candidates
- Search tool attach: implemented through UI/source-package/runtime/Hermes path
- Hermes wrapper propagation: fixed universally via UI startup restore
- Final search visibility blocker: fixed in gate/profile detection
- Fix commit: `df3a3b009132ada4ff3ada75178a97e46fd2a686`
- Current validation stop point: manual Telegram acceptance test for Squidward
- Next technical block after acceptance: metadata pre-evaluation/ranking
- Session-snapshot confusion was a symptom; the actual first broken layer was the search gate/check_fn path

## Repository Shape

Bounded top-level directories observed:

- `agent-packages/`
- `agent_lab/`
- `docs/`
- `tests/`
- `tool-registry/`
- `tools/`
- `vendor/`

## docs/codex_source Status

Current docs roots:

- `docs/codex_source/project/**`
- `docs/codex_source/roadmap/**`
- `docs/codex_source/module_map/**`
- `docs/codex_source/context/**`
- `docs/codex_source/project_snapshot/**`
- `docs/codex_source/rules/**`
- `docs/codex_source/vendor/**`
- `docs/codex_source/task_cards/**`

Current imported direction:

- current technical spec remains v0.3
- roadmap append-only memory now records the YouTube search agent visibility fix as the current active block
- module map append-only memory now records the gate/profile boundary that caused the visibility bug
- current dialogue context now records the final YouTube search fix and the diagnostic lesson
- public docs repo content rule remains `docs/codex_source/**` only

## Notes

- This snapshot is intentionally lightweight.
- It records the current YouTube Research state and the final proven root cause/fix for the visibility issue.
- It does not replace the full project docs, vendor docs, or append-only memory tails.

# Project Snapshot — 2026-05-22 — YouTube Curator selection UI/runtime configuration

## Current active block

`youtube_select_candidates_curator_configuration_before_live_hermes`

## Completed since previous snapshot

- `youtube.select_candidates` contract implemented.
- Selection lifecycle storage implemented.
- `youtube_curator` package created.
- `youtube_curator` protected as system/internal agent.
- Offline selector-to-curator boundary implemented.
- Runtime profile for `youtube_curator` created through source-managed apply.
- Read-only YouTube Curator UI/status panel implemented.
- Source-policy editor for `youtube_curator/rules.md` implemented.
- Apply preview/apply controls implemented using existing runtime apply endpoints.
- Live UI verification showed apply controls are present and `/api/state` remains sanitized.

## Current stop point

The next user-facing step is manual browser verification:

- hard-refresh browser;
- open `Ютуб → Сортировка`;
- verify status panel, policy editor, and apply controls.

The next technical step after manual policy/apply verification is a separate proof/design for live Hermes-backed curator adapter.

## Current hard boundaries

- No live Hermes-backed curator call yet.
- No provider/model call.
- No Telegram API call.
- No YouTube live search.
- No next editing/formatting tool call.
- No auto-mode.
- Runtime memory remains profile-local and is not editable through current UI.
- `system_filter` remains separate and must not be reused as YouTube curator.
