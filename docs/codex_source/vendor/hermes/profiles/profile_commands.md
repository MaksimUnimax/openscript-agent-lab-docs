# Hermes profile commands

STATUS: verified
CATEGORY: vendor/hermes/profiles

SOURCE_URLS:
- https://hermes-agent.nousresearch.com/docs/user-guide/profiles/

SOURCE_PATHS:
- docs/codex_source/vendor/hermes/_raw/profiles.html
- docs/codex_source/vendor/hermes/_raw/llms-full.txt

LOCAL_SOURCE_PATHS:
- /opt/openscript-agent-lab/vendor/hermes-agent/hermes_cli/profiles.py

CLI_HELP:
- docs/codex_source/vendor/hermes/_raw/cli_help/hermes_profile_help.txt

APPLIES_TO:
- profile create/update/delete/list/info
- profile clone and install flows

FACTS:
- `hermes profile` owns the profile lifecycle.
- profile commands read and write the per-profile Hermes home layout.
- update flows preserve user-owned state unless explicitly forced.

CONTRACT:
- use profile commands for profile lifecycle; do not reimplement them in app code.

NON_GOALS:
- no CLI UX copywriting

FORBIDDEN_MISUSE:
- treating profile commands as a substitute for docs extraction

OPEN_QUESTIONS:
- none

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- local_source_checked: yes
- cli_help_checked: yes
- verified_at_utc: 2026-05-16T10:33:42Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_HERMES_DOCS_EXTRACTION_20260516_01
