# Hermes getting started

STATUS: extracted
CATEGORY: vendor/hermes/overview

SOURCE_URLS:
- https://hermes-agent.nousresearch.com/docs/
- https://hermes-agent.nousresearch.com/docs/getting-started/quickstart

SOURCE_PATHS:
- docs/codex_source/vendor/hermes/_raw/docs_root.html
- docs/codex_source/vendor/hermes/_raw/llms-full.txt

LOCAL_SOURCE_PATHS:
- /opt/openscript-agent-lab/vendor/hermes-agent/hermes_cli/main.py
- /opt/openscript-agent-lab/vendor/hermes-agent/hermes_constants.py

CLI_HELP:
- docs/codex_source/vendor/hermes/_raw/cli_help/hermes_help.txt

APPLIES_TO:
- first-run setup
- choosing the right exact doc path

FACTS:
- Hermes exposes chat, gateway, model, profile, tools, skills, and auth flows through the CLI.
- first-run docs are split between quickstart, configuration, and feature pages.
- HERMES_HOME is the root for Hermes state on disk.

CONTRACT:
- use the docs map and task cards before doing a run.
- do not infer vendor contracts from project docs alone.

NON_GOALS:
- no installation wizard implementation
- no credential persistence logic

FORBIDDEN_MISUSE:
- treating getting-started prose as a substitute for runtime docs

OPEN_QUESTIONS:
- none

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- local_source_checked: yes
- cli_help_checked: yes
- verified_at_utc: 2026-05-16T10:33:42Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_HERMES_DOCS_EXTRACTION_20260516_01
