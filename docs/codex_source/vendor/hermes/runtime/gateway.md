# Hermes gateway

STATUS: verified
CATEGORY: vendor/hermes/runtime

SOURCE_URLS:
- https://hermes-agent.nousresearch.com/docs/user-guide/features/api-server/
- https://hermes-agent.nousresearch.com/docs/reference/environment-variables

SOURCE_PATHS:
- docs/codex_source/vendor/hermes/_raw/api_server.html
- docs/codex_source/vendor/hermes/_raw/environment_variables.html
- docs/codex_source/vendor/hermes/_raw/llms-full.txt

LOCAL_SOURCE_PATHS:
- /opt/openscript-agent-lab/vendor/hermes-agent/gateway/run.py
- /opt/openscript-agent-lab/vendor/hermes-agent/gateway/config.py

CLI_HELP:
- docs/codex_source/vendor/hermes/_raw/cli_help/hermes_gateway_help.txt

APPLIES_TO:
- gateway startup
- profile-scoped runtime
- messaging platform backends

FACTS:
- `hermes gateway` is the entrypoint for the runtime server side.
- gateway behavior is profile-aware and honors Hermes home scope.
- API server mode can back other frontends and proxy deployments.

CONTRACT:
- gateway docs should be read before changing any server-side runtime assumption.

NON_GOALS:
- no platform adapter implementation details

FORBIDDEN_MISUSE:
- treating gateway startup as provider auth bootstrap

OPEN_QUESTIONS:
- exact backend topology varies by platform

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- local_source_checked: yes
- cli_help_checked: yes
- verified_at_utc: 2026-05-16T10:33:42Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_HERMES_DOCS_EXTRACTION_20260516_01
