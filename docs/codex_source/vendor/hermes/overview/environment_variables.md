# Hermes environment variables

STATUS: verified
CATEGORY: vendor/hermes/overview

SOURCE_URLS:
- https://hermes-agent.nousresearch.com/docs/reference/environment-variables
- https://hermes-agent.nousresearch.com/docs/user-guide/features/api-server/

SOURCE_PATHS:
- docs/codex_source/vendor/hermes/_raw/environment_variables.html
- docs/codex_source/vendor/hermes/_raw/api_server.html
- docs/codex_source/vendor/hermes/_raw/llms-full.txt

LOCAL_SOURCE_PATHS:
- /opt/openscript-agent-lab/vendor/hermes-agent/hermes_constants.py
- /opt/openscript-agent-lab/vendor/hermes-agent/hermes_cli/auth.py
- /opt/openscript-agent-lab/vendor/hermes-agent/hermes_cli/runtime_provider.py
- /opt/openscript-agent-lab/vendor/hermes-agent/gateway/config.py

CLI_HELP:
- docs/codex_source/vendor/hermes/_raw/cli_help/hermes_help.txt

APPLIES_TO:
- provider selection
- auth store location
- codex app-server runtime
- API server and gateway

FACTS:
- `HERMES_INFERENCE_PROVIDER` overrides provider selection.
- `HERMES_HOME` overrides the Hermes state directory.
- `CODEX_HOME` isolates Codex app-server runtime config/auth.
- `HERMES_OAUTH_FILE` defaults to `~/.hermes/auth.json`.
- `API_SERVER_ENABLED` and `API_SERVER_KEY` gate the API server runtime.

CONTRACT:
- env vars are runtime inputs, not vendor docs substitutes.
- secret material is never printed in docs.

NON_GOALS:
- exhaustive variable catalog
- OS-specific deployment tuning

FORBIDDEN_MISUSE:
- using env docs to store credentials in repo files

OPEN_QUESTIONS:
- some platform-specific vars live in other docs and are out of scope here

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- local_source_checked: yes
- cli_help_checked: yes
- verified_at_utc: 2026-05-16T10:33:42Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_HERMES_DOCS_EXTRACTION_20260516_01
