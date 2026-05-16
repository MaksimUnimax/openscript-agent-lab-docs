# Hermes MCP

STATUS: extracted
CATEGORY: vendor/hermes/tools

SOURCE_URLS:
- https://hermes-agent.nousresearch.com/docs/developer-guide/tools-runtime
- https://hermes-agent.nousresearch.com/docs/user-guide/features/codex-app-server-runtime

SOURCE_PATHS:
- docs/codex_source/vendor/hermes/_raw/tools_runtime.html
- docs/codex_source/vendor/hermes/_raw/codex_app_server_runtime.html

LOCAL_SOURCE_PATHS:
- /opt/openscript-agent-lab/vendor/hermes-agent/agent/transports/codex.py
- /opt/openscript-agent-lab/vendor/hermes-agent/agent/skill_utils.py

CLI_HELP:
- docs/codex_source/vendor/hermes/_raw/cli_help/hermes_tools_help.txt

APPLIES_TO:
- MCP tool exposure
- Codex runtime callback bridge

FACTS:
- Hermes tools can be exposed through MCP-style callbacks in the Codex runtime path.
- MCP tools stay behind the same registry and availability model as other tools.

CONTRACT:
- do not treat MCP tools as a separate authorization system.

NON_GOALS:
- no MCP protocol deep dive

FORBIDDEN_MISUSE:
- bypassing Hermes tool checks by calling MCP paths directly

OPEN_QUESTIONS:
- exact server/client topology depends on runtime mode

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- local_source_checked: yes
- cli_help_checked: yes
- verified_at_utc: 2026-05-16T10:33:42Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_HERMES_DOCS_EXTRACTION_20260516_01
