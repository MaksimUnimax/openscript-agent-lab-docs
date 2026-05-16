# Hermes tools runtime

STATUS: verified
CATEGORY: vendor/hermes/tools

SOURCE_URLS:
- https://hermes-agent.nousresearch.com/docs/developer-guide/tools-runtime
- https://hermes-agent.nousresearch.com/docs/reference/toolsets-reference

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
- tool registry
- toolsets
- availability checks

FACTS:
- Hermes tools are registry-backed and grouped into toolsets.
- `check_fn` gating removes unavailable tools before the model sees them.
- toolset resolution happens centrally and supports plugin-registered toolsets.

CONTRACT:
- future tasks should read the tool runtime docs before editing tool routing.

NON_GOALS:
- no tool implementation details

FORBIDDEN_MISUSE:
- bypassing registry availability checks

OPEN_QUESTIONS:
- none

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- local_source_checked: yes
- cli_help_checked: yes
- verified_at_utc: 2026-05-16T10:33:42Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_HERMES_DOCS_EXTRACTION_20260516_01
