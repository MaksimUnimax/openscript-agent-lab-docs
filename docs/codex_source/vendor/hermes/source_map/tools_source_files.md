# Hermes tools source files

STATUS: extracted
CATEGORY: vendor/hermes/source_map

SOURCE_URLS:
- none

SOURCE_PATHS:
- none

LOCAL_SOURCE_PATHS:
- /opt/openscript-agent-lab/vendor/hermes-agent/toolsets.py
- /opt/openscript-agent-lab/vendor/hermes-agent/model_tools.py
- /opt/openscript-agent-lab/vendor/hermes-agent/agent/skill_utils.py

CLI_HELP:
- docs/codex_source/vendor/hermes/_raw/cli_help/hermes_tools_help.txt

APPLIES_TO:
- tool registry
- toolset resolution
- skill metadata

FACTS:
- `toolsets.py` defines toolset composition and built-in sets.
- `model_tools.py` filters availability and builds tool definitions.
- `skill_utils.py` carries skill metadata such as required and fallback toolsets.

CONTRACT:
- future tool tasks should cite these exact files.

NON_GOALS:
- no tool code copying

FORBIDDEN_MISUSE:
- bypassing availability checks by editing app code

OPEN_QUESTIONS:
- none

VERIFICATION:
- raw_source_saved: no
- official_docs_checked: no
- local_source_checked: yes
- cli_help_checked: yes
- verified_at_utc: 2026-05-16T10:33:42Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_HERMES_DOCS_EXTRACTION_20260516_01
