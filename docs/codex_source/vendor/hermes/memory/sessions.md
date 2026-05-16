# Hermes sessions

STATUS: verified
CATEGORY: vendor/hermes/memory

SOURCE_URLS:
- https://hermes-agent.nousresearch.com/docs/user-guide/profiles/
- https://hermes-agent.nousresearch.com/docs/guides/tips

SOURCE_PATHS:
- docs/codex_source/vendor/hermes/_raw/profiles.html
- docs/codex_source/vendor/hermes/_raw/llms-full.txt

LOCAL_SOURCE_PATHS:
- /opt/openscript-agent-lab/vendor/hermes-agent/hermes_cli/profiles.py
- /opt/openscript-agent-lab/vendor/hermes-agent/hermes_constants.py

CLI_HELP:
- docs/codex_source/vendor/hermes/_raw/cli_help/hermes_help.txt

APPLIES_TO:
- conversation history
- session persistence

FACTS:
- sessions are per-profile runtime state.
- sessions are not vendor docs and are not the same as auth.

CONTRACT:
- session history must remain separate from docs source-of-truth layers.

NON_GOALS:
- no session database migration guide

FORBIDDEN_MISUSE:
- using session state as a substitute for documentation

OPEN_QUESTIONS:
- none

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- local_source_checked: yes
- cli_help_checked: yes
- verified_at_utc: 2026-05-16T10:33:42Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_HERMES_DOCS_EXTRACTION_20260516_01
