# PROJECT SNAPSHOT

STATUS: PARTIAL_SNAPSHOT

Generated from repo tree inspection only.

Source directories:
- `agent_lab/`
- `tests/`
- `tools/`
- `tool-registry/`
- `vendor/hermes-agent/`

Runtime directories:
- `.venv-hermes/`
- `agent_lab/static/`

Docs source-of-truth:
- `docs/codex_source/vendor/hermes/**`
- `docs/codex_source/vendor/telegram/**`
- `docs/codex_source/project/**`

Project memory:
- `docs/codex_source/context/**`
- `docs/codex_source/roadmap/**`
- `docs/codex_source/module_map/**`
- `docs/codex_source/project_snapshot/**`
- `docs/codex_source/rules/**`

Agent packages:
- `agent-packages/`
- contains unrelated dirty/untracked work

Touch policy:
- do not edit `agent-packages/**` without explicit scope
- do not read auth/secrets here
- do not confuse snapshot with source-of-truth

Refresh policy:
- rerun safe tree inspection only
- keep this file lightweight
