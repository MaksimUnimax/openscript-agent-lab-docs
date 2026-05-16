# Hermes toolsets

STATUS: verified
CATEGORY: vendor/hermes/tools

SOURCE_URLS:
- https://hermes-agent.nousresearch.com/docs/reference/toolsets-reference/
- https://hermes-agent.nousresearch.com/docs/developer-guide/tools-runtime

SOURCE_PATHS:
- docs/codex_source/vendor/hermes/_raw/tools_reference.html
- docs/codex_source/vendor/hermes/_raw/tools_runtime.html
- docs/codex_source/vendor/hermes/_raw/llms-full.txt

LOCAL_SOURCE_PATHS:
- /opt/openscript-agent-lab/vendor/hermes-agent/toolsets.py
- /opt/openscript-agent-lab/vendor/hermes-agent/model_tools.py

CLI_HELP:
- docs/codex_source/vendor/hermes/_raw/cli_help/hermes_tools_help.txt

APPLIES_TO:
- toolset composition
- platform presets
- plugin toolsets

FACTS:
- toolsets can include tools or other toolsets.
- plugin-registered toolsets are resolved through the same registry path.
- Hermes provides platform-specific toolset presets, including messaging backends.

CONTRACT:
- toolsets are the control surface for tool availability.

NON_GOALS:
- no per-tool authorization scheme

FORBIDDEN_MISUSE:
- hardcoding toolset membership in app code

OPEN_QUESTIONS:
- exact preset composition is in the reference docs

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- local_source_checked: yes
- cli_help_checked: yes
- verified_at_utc: 2026-05-16T10:33:42Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_HERMES_DOCS_EXTRACTION_20260516_01
