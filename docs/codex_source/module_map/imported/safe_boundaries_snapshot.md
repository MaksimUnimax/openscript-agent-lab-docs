# Safe Boundaries Snapshot - OpenScript Agent Lab

STATUS: CURRENT_SNAPSHOT_FROM_REPO_INVENTORY
SOURCE_KIND: imported project docs + bounded repo inventory
DATE: 2026-05-16

## Canonical Boundaries

These are the current safe boundaries derived from imported project docs, roadmap v0.7, rules v2 and bounded repo inventory:

- `docs/codex_source/**` is the documentation source-of-truth for ChatGPT and Codex.
- The public docs repo mirrors only `docs/codex_source/**`.
- `agent_lab/**` is application/backend/UI code and is not a docs-import target.
- `agent-packages/**` are agent source packages and unrelated dirty workspace state; do not stage accidentally.
- `vendor/hermes-agent/**` is a vendor checkout and must not be casually edited or used as a substitute for repo docs.
- `/var/lib/openscript-agent-lab/hermes/**` is runtime state, not source-of-truth.
- `/var/log/openscript-agent-lab/**` is runtime log state, not source-of-truth.
- runtime auth, memory, sessions, logs and secrets are private runtime state.
- source package != runtime profile.
- no symlinks for `SOUL.md` or `config.yaml`.
- UI edits source package, `agentctl apply` synchronizes into runtime.
- agent and provider are independent axes.
- provider selection must not silently rewrite agent documents.
- business logic owns money, DB facts and reports.
- agent/LLM owns tone, explanation and safe dialog only.
- skills are instructions and requirements, not permissions.
- tools/tool-registry are capability and permission registry layers.
- Telegram Router is separate from business logic, provider/auth and docs memory.
- Hermes Dashboard must not be exposed as the public product UI.
- public/private repo publication is a docs-only workflow; do not export code or runtime state into the public docs repo.

## Module Boundary Rules

- new features should name the affected modules before any code change;
- if a task touches more modules than named, stop and re-scope;
- if a boundary is unclear, do proof/design first, not a fix;
- no hardcoded fixed agent count;
- no hardcoded agent slug except in explicit proof fixtures;
- no hardcoded Telegram user/chat/provider assumptions unless the task explicitly allows them;
- no broad vendor-source edits without a proof/design task;
- no raw secret logging;
- no public exposure of runtime/auth/secrets;
- no direct replay of old direct-path/fallback behavior for live reply unless a new approved proof says so;
- docs-only runs must never mutate runtime state;
- docs-only runs must never touch application code, `agent_lab/**`, `agent-packages/**`, `tools/**`, `tests/**` or vendor source code.

## Proven Versus Pending

### Proven / canonical

- documentation root and public mirror boundaries;
- source package vs runtime profile split;
- runtime state is not source-of-truth;
- business layer vs agent/LLM responsibility split;
- Telegram access control uses `from.id` / `user_id` for identity, not `chat_id` alone;
- Telegram `chat_id` is delivery/context, not allowlist identity;
- Telegram voice pipeline uses controlled download, STT and transcript handoff before the Hermes reply path;
- tools are registry-backed capabilities, not skills;
- skills are instructions and requirements, not permissions.

### Pending proof / still stub in project docs

- deeper project docs such as `agent_lab_architecture`, `agent_package_vs_runtime_profile`, `telegram_router`, `telegram_voice_pipeline`, `universal_hermes_reply_path`, `llm_connection_binding`, `access_control`;
- task card readiness after this snapshot import;
- any future module boundary not visible from bounded inventory or imported docs.

## Current Safety Summary

The safest current working rule is:

1. read the exact docs listed in the prompt;
2. check the active task card or snapshot if a task is being evaluated;
3. keep docs-only runs inside `docs/codex_source/**`;
4. keep code changes outside docs runs unless the task explicitly targets code;
5. keep runtime state, auth and secrets out of git and out of public docs;
6. if a boundary is unclear, stop and seek proof instead of guessing.

