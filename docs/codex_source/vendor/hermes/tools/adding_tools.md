# Hermes adding tools

STATUS: extracted
CATEGORY: vendor/hermes/tools

SOURCE_URLS:
- https://hermes-agent.nousresearch.com/docs/developer-guide/tools-runtime

SOURCE_PATHS:
- docs/codex_source/vendor/hermes/_raw/tools_runtime.html
- docs/codex_source/vendor/hermes/_raw/llms-full.txt

LOCAL_SOURCE_PATHS:
- /opt/openscript-agent-lab/vendor/hermes-agent/toolsets.py
- /opt/openscript-agent-lab/vendor/hermes-agent/model_tools.py
- /opt/openscript-agent-lab/vendor/hermes-agent/agent/tools.py

CLI_HELP:
- docs/codex_source/vendor/hermes/_raw/cli_help/hermes_tools_help.txt

APPLIES_TO:
- tool registration
- custom toolsets

FACTS:
- tools are registered with a central registry and then surfaced through toolset resolution.
- availability checks and required environment variables are first-class metadata.

CONTRACT:
- new tools should plug into the registry instead of bypassing it.

NON_GOALS:
- no full SDK guide

FORBIDDEN_MISUSE:
- adding tools directly in route handlers instead of through the registry

OPEN_QUESTIONS:
- plugin packaging specifics are outside this doc

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- local_source_checked: yes
- cli_help_checked: yes
- verified_at_utc: 2026-05-16T10:33:42Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_HERMES_DOCS_EXTRACTION_20260516_01
