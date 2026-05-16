# Source vs runtime

STATUS: IMPORTED_FROM_CHATGPT_UPLOAD

Source-of-truth layers:
- vendor docs under `docs/codex_source/vendor/**`
- project docs under `docs/codex_source/project/**`
- append-only memory under `docs/codex_source/context/**`, `docs/codex_source/roadmap/**`, `docs/codex_source/module_map/**`

Source package:
- stored in git under `/opt/openscript-agent-lab/agent-packages/<agent_slug>/`
- contains `SOUL.md`, `rules.md`, `examples.md`, `provider.defaults.json`, `skills/`
- is edited by UI and git-backed workflows
- is source-of-truth for documents and defaults

Runtime profile:
- stored under `/var/lib/openscript-agent-lab/hermes/profiles/<agent_slug>/`
- contains `config.yaml`, `.env`, `auth.json`, memories, sessions, logs and other runtime state
- is not source-of-truth
- may contain secrets

Boundary rules:
- UI edits source package, not runtime profile directly
- `agentctl apply` syncs source package into runtime profile
- no symlinks for `SOUL.md` or `config.yaml`
- runtime state must not be confused with documentation state
