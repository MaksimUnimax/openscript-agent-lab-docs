# Hermes profile source files

STATUS: extracted
CATEGORY: vendor/hermes/source_map

SOURCE_URLS:
- none

SOURCE_PATHS:
- none

LOCAL_SOURCE_PATHS:
- /opt/openscript-agent-lab/vendor/hermes-agent/hermes_cli/profiles.py
- /opt/openscript-agent-lab/vendor/hermes-agent/hermes_constants.py

CLI_HELP:
- docs/codex_source/vendor/hermes/_raw/cli_help/hermes_profile_help.txt

APPLIES_TO:
- profile lifecycle
- profile filesystem layout

FACTS:
- `profiles.py` implements profile creation, cloning, update, and layout logic.
- `hermes_constants.py` owns HERMES_HOME and path helpers.

CONTRACT:
- use these files for profile-state questions, not memory or auth docs.

NON_GOALS:
- no profile distribution authoring

FORBIDDEN_MISUSE:
- hardcoding profile paths outside the profile helpers

OPEN_QUESTIONS:
- none

VERIFICATION:
- raw_source_saved: no
- official_docs_checked: no
- local_source_checked: yes
- cli_help_checked: yes
- verified_at_utc: 2026-05-16T10:33:42Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_HERMES_DOCS_EXTRACTION_20260516_01
