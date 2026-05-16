# Hermes runtime profiles

STATUS: verified
CATEGORY: vendor/hermes/profiles

SOURCE_URLS:
- https://hermes-agent.nousresearch.com/docs/user-guide/profiles/
- https://hermes-agent.nousresearch.com/docs/user-guide/features/api-server/

SOURCE_PATHS:
- docs/codex_source/vendor/hermes/_raw/profiles.html
- docs/codex_source/vendor/hermes/_raw/api_server.html
- docs/codex_source/vendor/hermes/_raw/llms-full.txt

LOCAL_SOURCE_PATHS:
- /opt/openscript-agent-lab/vendor/hermes-agent/hermes_cli/profiles.py
- /opt/openscript-agent-lab/vendor/hermes-agent/hermes_constants.py

CLI_HELP:
- docs/codex_source/vendor/hermes/_raw/cli_help/hermes_profile_help.txt

APPLIES_TO:
- multiple independent Hermes agents
- profile-specific state isolation

FACTS:
- each profile has its own Hermes home subtree, config, auth, memory, sessions, skills, logs, workspace, and cron state.
- `HERMES_HOME` can point at a profile root.
- profile copies preserve user-owned state while cloning distribution-owned config.

CONTRACT:
- profiles are the isolation boundary for stateful Hermes runs.
- do not confuse profile state with vendor docs or app-level configuration.

NON_GOALS:
- no distribution packaging instructions

FORBIDDEN_MISUSE:
- sharing memories or auth as if they were distribution content

OPEN_QUESTIONS:
- platform-specific profile details are handled in later docs

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- local_source_checked: yes
- cli_help_checked: yes
- verified_at_utc: 2026-05-16T10:33:42Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_HERMES_DOCS_EXTRACTION_20260516_01
