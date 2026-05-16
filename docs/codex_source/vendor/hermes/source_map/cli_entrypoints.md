# Hermes CLI entrypoints map

STATUS: extracted
CATEGORY: vendor/hermes/source_map

SOURCE_URLS:
- none

SOURCE_PATHS:
- none

LOCAL_SOURCE_PATHS:
- /opt/openscript-agent-lab/vendor/hermes-agent/hermes_cli/main.py
- /opt/openscript-agent-lab/vendor/hermes-agent/hermes_cli/auth.py
- /opt/openscript-agent-lab/vendor/hermes-agent/hermes_cli/model_switch.py
- /opt/openscript-agent-lab/vendor/hermes-agent/hermes_cli/profiles.py
- /opt/openscript-agent-lab/vendor/hermes-agent/hermes_cli/runtime_provider.py
- /opt/openscript-agent-lab/vendor/hermes-agent/cli.py

CLI_HELP:
- docs/codex_source/vendor/hermes/_raw/cli_help/hermes_help.txt

APPLIES_TO:
- CLI command dispatch
- auth/model/profile/tool entrypoints

FACTS:
- `hermes_cli/main.py` and `cli.py` are the top-level command entrypoints.
- `auth.py`, `model_switch.py`, `profiles.py`, and `runtime_provider.py` are the major command-support modules.

CONTRACT:
- use the exact local source paths when a prompt needs the implementation boundary.

NON_GOALS:
- no source-code copying

FORBIDDEN_MISUSE:
- using the source map as a substitute for code review

OPEN_QUESTIONS:
- none

VERIFICATION:
- raw_source_saved: no
- official_docs_checked: no
- local_source_checked: yes
- cli_help_checked: yes
- verified_at_utc: 2026-05-16T10:33:42Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_HERMES_DOCS_EXTRACTION_20260516_01
