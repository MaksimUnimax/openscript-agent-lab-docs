# Hermes quickstart

STATUS: extracted
CATEGORY: vendor/hermes/overview

SOURCE_URLS:
- https://hermes-agent.nousresearch.com/docs/getting-started/quickstart
- https://hermes-agent.nousresearch.com/docs/user-guide/cli/

SOURCE_PATHS:
- docs/codex_source/vendor/hermes/_raw/docs_root.html
- docs/codex_source/vendor/hermes/_raw/llms-full.txt

LOCAL_SOURCE_PATHS:
- /opt/openscript-agent-lab/vendor/hermes-agent/hermes_cli/main.py
- /opt/openscript-agent-lab/vendor/hermes-agent/hermes_cli/model_switch.py

CLI_HELP:
- docs/codex_source/vendor/hermes/_raw/cli_help/hermes_help.txt

APPLIES_TO:
- basic chat entrypoints
- model/provider selection

FACTS:
- Hermes quickstart routes a user into the CLI and then into provider/model selection.
- the quickstart path is not the same thing as Codex app-server runtime.
- model/provider resolution is centralized, not duplicated per feature.

CONTRACT:
- future prompt tasks should use runtime/provider docs for resolution details.

NON_GOALS:
- no provider implementation
- no gateway wiring

FORBIDDEN_MISUSE:
- assuming quickstart covers auth edge cases or profile isolation

OPEN_QUESTIONS:
- none

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- local_source_checked: yes
- cli_help_checked: yes
- verified_at_utc: 2026-05-16T10:33:42Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_HERMES_DOCS_EXTRACTION_20260516_01
