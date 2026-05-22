# Project snapshot

STATUS: CURRENT

This lightweight snapshot reflects the current YouTube Research state.

Current snapshot:

- source-of-truth docs: `docs/codex_source/**`
- vendor source: `docs/codex_source/vendor/**`
- project memory: `docs/codex_source/project/**`, `docs/codex_source/context/**`, `docs/codex_source/roadmap/**`, `docs/codex_source/module_map/**`, `docs/codex_source/project_snapshot/**`, `docs/codex_source/rules/**`
- application tree: `agent_lab/`
- tests: `tests/`
- utility tools: `tools/`
- registry: `tool-registry/`
- local Hermes vendor source: `vendor/hermes-agent/`
- package workspace: `agent-packages/`

Current YouTube Research state:

- `youtube.subtitles_get` is implemented, UI-connected, attachable, and Telegram-proven.
- `youtube.search_candidates` is implemented, attachable, and now visible to Hermes after the gate/profile fix.
- full-description enrichment is implemented as a separate metadata-only stage over saved candidates.
- the test candidate DB was cleaned after proof runs while preserving the saved search profile.
- Hermes wrapper propagation is fixed universally via UI startup restore.
- the final visibility blocker was the search gate/profile detection path using the wrong Hermes-home resolution.
- fix commit: `df3a3b009132ada4ff3ada75178a97e46fd2a686`.

Current stop point:

- manual Telegram acceptance test for Squidward.

Next technical block after acceptance:

- metadata pre-evaluation/ranking for saved and enriched candidates.

Important debugging lesson:

- compare the working tool and broken tool through gate/check_fn/discovery before blaming sessions, runtime apply, wrapper propagation, or Telegram routing.
