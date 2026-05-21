# Project snapshot

STATUS: PARTIAL_SNAPSHOT

This is a lightweight summary of the repo shape, generated from repo tree inspection only.

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
- local virtual environment: `.venv-hermes/`

Source directories:
- `agent_lab/` - runtime application code and static assets
- `tests/` - automated tests
- `tools/` - utility scripts
- `tool-registry/` - tool registry data
- `vendor/hermes-agent/` - local Hermes source checkout

Runtime directories:
- `.venv-hermes/` - local runtime environment
- `agent_lab/static/` - static UI assets

Agent packages:
- `agent-packages/` exists and currently contains unrelated dirty/untracked work
- do not stage or modify it unless the scope explicitly requires it

Hermes profiles:
- NEEDS_MAPPING

Telegram runtime state:
- NEEDS_MAPPING

Docs source-of-truth:
- `docs/codex_source/index.yaml`

Vendor docs:
- `docs/codex_source/vendor/hermes/**`
- `docs/codex_source/vendor/telegram/**`

Project docs:
- `docs/codex_source/project/**`
- append-only memory files under `docs/codex_source/context/**`, `docs/codex_source/roadmap/**`, `docs/codex_source/module_map/**`

Things not to touch without explicit scope:
- `agent-packages/**`
- secrets and auth files
- runtime config files
- vendor source trees
- generated caches

How to refresh this snapshot:
- re-run safe tree inspection only
- update this file and `docs/codex_source/project_snapshot/project_snapshot_manifest.yaml`
- do not paste full file contents here

## 2026-05-21 — Snapshot update: YouTube subtitles tool MVP completed

The project now includes a working first implementation of the “Ютуб” tool family.

Implemented tool:

- `youtube.subtitles_get`

Current status:

- deterministic executor implemented;
- vendor mechanism: `youtube-transcript-api`;
- operator UI tab `Ютуб` implemented;
- manual subtitle test route implemented;
- language fallback `ru -> en -> any available transcript` implemented;
- tool can be attached to selected agents through UI;
- Squidward was used as the first manual Telegram proof agent;
- user confirmed that Telegram returned subtitles.

Important boundary:

- The tool remains a Hermes-visible agent tool.
- It is not a standalone script.
- It is not an app-local-only shortcut.
- It is not globally enabled for all agents.
- Agent attachment is controlled through UI/source-package flow.

Current next work should not restart YouTube design. Future YouTube work is optional extension/polish only unless a regression appears.

## 2026-05-21 — Snapshot update: next direction after YouTube subtitles MVP

The next product direction is a future Telegram AI/Vibecoding Publisher Agent.

Goal:

- help prepare Telegram public-channel content about neural networks, AI tools, coding agents, and vibe coding.

The next technical block is the YouTube Research pipeline.

Initial planned stages:

- `youtube.search_candidates`
- `youtube.collect_subtitles_for_candidates`
- `youtube.rank_candidates`
- `youtube.editorial_evaluate`

The completed `youtube.subtitles_get` tool is a dependency for the collection stage.

The first next implementation topic is YouTube video search/provider selection and candidate storage design.

Publishing, image generation, and Telegram post sending remain future separate blocks.
