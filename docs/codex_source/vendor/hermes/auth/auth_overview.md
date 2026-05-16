# Hermes auth overview

STATUS: verified
CATEGORY: vendor/hermes/auth

SOURCE_URLS:
- https://hermes-agent.nousresearch.com/docs/integrations/providers
- https://hermes-agent.nousresearch.com/docs/user-guide/features/codex-app-server-runtime

SOURCE_PATHS:
- docs/codex_source/vendor/hermes/_raw/providers.html
- docs/codex_source/vendor/hermes/_raw/codex_app_server_runtime.html
- docs/codex_source/vendor/hermes/_raw/llms-full.txt

LOCAL_SOURCE_PATHS:
- /opt/openscript-agent-lab/vendor/hermes-agent/hermes_cli/auth.py
- /opt/openscript-agent-lab/vendor/hermes-agent/agent/credential_sources.py
- /opt/openscript-agent-lab/vendor/hermes-agent/agent/credential_pool.py

CLI_HELP:
- docs/codex_source/vendor/hermes/_raw/cli_help/hermes_auth_help.txt
- docs/codex_source/vendor/hermes/_raw/cli_help/hermes_auth_status_help.txt

APPLIES_TO:
- Hermes auth store
- device-code providers
- Codex CLI import/adopt

FACTS:
- Hermes persists provider auth in `~/.hermes/auth.json`.
- openai-codex uses Hermes OAuth/device-code flow, not application code auth logic.
- Codex CLI credentials may be imported from `~/.codex/auth.json` when present.

CONTRACT:
- keep Hermes auth separate from Codex app-server runtime auth.
- do not use chat memory or route logic as auth state.

NON_GOALS:
- no live login commands
- no secret inspection

FORBIDDEN_MISUSE:
- treating Codex CLI auth as proof that Hermes auth is live

OPEN_QUESTIONS:
- provider-specific auth edge cases are covered in the sibling docs

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- local_source_checked: yes
- cli_help_checked: yes
- verified_at_utc: 2026-05-16T10:33:42Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_HERMES_DOCS_EXTRACTION_20260516_01
