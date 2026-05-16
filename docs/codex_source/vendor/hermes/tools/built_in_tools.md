# Hermes built-in tools

STATUS: verified
CATEGORY: vendor/hermes/tools

SOURCE_URLS:
- https://hermes-agent.nousresearch.com/docs/reference/tools-reference/

SOURCE_PATHS:
- docs/codex_source/vendor/hermes/_raw/tools_reference.html
- docs/codex_source/vendor/hermes/_raw/llms-full.txt

LOCAL_SOURCE_PATHS:
- /opt/openscript-agent-lab/vendor/hermes-agent/toolsets.py
- /opt/openscript-agent-lab/vendor/hermes-agent/model_tools.py

CLI_HELP:
- docs/codex_source/vendor/hermes/_raw/cli_help/hermes_tools_help.txt

APPLIES_TO:
- built-in tool catalog
- toolset defaults

FACTS:
- built-in tools are exposed through the same registry and toolset filtering system.
- tool availability can depend on config, env, platform, or credentials.

CONTRACT:
- use the tool reference docs for tool naming and gating semantics.

NON_GOALS:
- no full tool catalog mirror in this doc

FORBIDDEN_MISUSE:
- assuming every tool is always available

OPEN_QUESTIONS:
- tool-by-tool details remain in the reference docs

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- local_source_checked: yes
- cli_help_checked: yes
- verified_at_utc: 2026-05-16T10:33:42Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_HERMES_DOCS_EXTRACTION_20260516_01
