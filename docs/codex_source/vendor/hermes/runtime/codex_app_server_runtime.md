# Hermes Codex app-server runtime

STATUS: verified
CATEGORY: vendor/hermes/runtime

SOURCE_URLS:
- https://hermes-agent.nousresearch.com/docs/user-guide/features/codex-app-server-runtime
- https://hermes-agent.nousresearch.com/docs/reference/environment-variables

SOURCE_PATHS:
- docs/codex_source/vendor/hermes/_raw/codex_app_server_runtime.html
- docs/codex_source/vendor/hermes/_raw/environment_variables.html
- docs/codex_source/vendor/hermes/_raw/llms-full.txt

LOCAL_SOURCE_PATHS:
- /opt/openscript-agent-lab/vendor/hermes-agent/agent/transports/codex.py
- /opt/openscript-agent-lab/vendor/hermes-agent/agent/auxiliary_client.py
- /opt/openscript-agent-lab/vendor/hermes-agent/hermes_cli/auth.py

CLI_HELP:
- docs/codex_source/vendor/hermes/_raw/cli_help/hermes_model_help.txt
- docs/codex_source/vendor/hermes/_raw/cli_help/hermes_auth_help.txt

APPLIES_TO:
- optional Codex app-server runtime
- `openai/*` and `openai-codex/*` turns

FACTS:
- Hermes can hand selected turns to the Codex CLI app-server instead of running its own tool loop.
- terminal commands, file edits, sandboxing, and MCP tool calls then execute inside Codex runtime.
- Hermes still owns sessions, gateway, memory, and skill review.
- Codex app-server auth is separate from Hermes provider auth and is gated by `CODEX_HOME`.

CONTRACT:
- do not mix app-server runtime state with Hermes provider auth state.
- app-server runtime is optional and must remain opt-in.

NON_GOALS:
- no provider auth implementation

FORBIDDEN_MISUSE:
- assuming app-server runtime means Hermes provider auth is already live

OPEN_QUESTIONS:
- live runtime behavior can differ slightly by Codex CLI version

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- local_source_checked: yes
- cli_help_checked: yes
- verified_at_utc: 2026-05-16T10:33:42Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_HERMES_DOCS_EXTRACTION_20260516_01
