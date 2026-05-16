# Hermes profile state layout

STATUS: verified
CATEGORY: vendor/hermes/profiles

SOURCE_URLS:
- https://hermes-agent.nousresearch.com/docs/user-guide/profiles/
- https://hermes-agent.nousresearch.com/docs/reference/environment-variables

SOURCE_PATHS:
- docs/codex_source/vendor/hermes/_raw/profiles.html
- docs/codex_source/vendor/hermes/_raw/environment_variables.html
- docs/codex_source/vendor/hermes/_raw/llms-full.txt

LOCAL_SOURCE_PATHS:
- /opt/openscript-agent-lab/vendor/hermes-agent/hermes_cli/profiles.py
- /opt/openscript-agent-lab/vendor/hermes-agent/hermes_constants.py

CLI_HELP:
- docs/codex_source/vendor/hermes/_raw/cli_help/hermes_profile_help.txt

APPLIES_TO:
- per-profile config.yaml
- .env
- SOUL.md
- sessions
- memory
- logs
- workspace
- cron

FACTS:
- profiles keep user-owned data separate from distribution-owned files.
- `config.yaml` and `.env` live inside the profile directory.
- memories, sessions, logs, state DBs, workspace, and home subpaths are profile-local runtime state.

CONTRACT:
- profile layout is the canonical place to look for runtime state boundaries.

NON_GOALS:
- no profile migration scripts

FORBIDDEN_MISUSE:
- storing vendor docs inside profile state

OPEN_QUESTIONS:
- Docker and Windows specifics live in sibling docs

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- local_source_checked: yes
- cli_help_checked: yes
- verified_at_utc: 2026-05-16T10:33:42Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_HERMES_DOCS_EXTRACTION_20260516_01
