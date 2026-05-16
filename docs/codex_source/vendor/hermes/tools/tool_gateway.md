# Hermes tool gateway

STATUS: extracted
CATEGORY: vendor/hermes/tools

SOURCE_URLS:
- https://hermes-agent.nousresearch.com/docs/user-guide/features/api-server/
- https://hermes-agent.nousresearch.com/docs/developer-guide/tools-runtime

SOURCE_PATHS:
- docs/codex_source/vendor/hermes/_raw/api_server.html
- docs/codex_source/vendor/hermes/_raw/tools_runtime.html

LOCAL_SOURCE_PATHS:
- /opt/openscript-agent-lab/vendor/hermes-agent/gateway/run.py
- /opt/openscript-agent-lab/vendor/hermes-agent/model_tools.py

CLI_HELP:
- docs/codex_source/vendor/hermes/_raw/cli_help/hermes_gateway_help.txt

APPLIES_TO:
- gateway-exposed tools
- frontend/tool bridge

FACTS:
- the gateway is the runtime side that publishes Hermes tools to frontends.
- tool exposure is mediated by the central registry and toolset selection.

CONTRACT:
- keep tool-gateway decisions in Hermes runtime, not in app-local route code.

NON_GOALS:
- no frontend protocol design

FORBIDDEN_MISUSE:
- flattening tool gateway and provider runtime into one concern

OPEN_QUESTIONS:
- exact gateway behavior differs by platform backend

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- local_source_checked: yes
- cli_help_checked: yes
- verified_at_utc: 2026-05-16T10:33:42Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_HERMES_DOCS_EXTRACTION_20260516_01
