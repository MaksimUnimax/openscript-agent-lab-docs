# Hermes profile isolation

STATUS: verified
CATEGORY: vendor/hermes/profiles

SOURCE_URLS:
- https://hermes-agent.nousresearch.com/docs/user-guide/profiles/

SOURCE_PATHS:
- docs/codex_source/vendor/hermes/_raw/profiles.html
- docs/codex_source/vendor/hermes/_raw/llms-full.txt

LOCAL_SOURCE_PATHS:
- /opt/openscript-agent-lab/vendor/hermes-agent/hermes_cli/profiles.py
- /opt/openscript-agent-lab/vendor/hermes-agent/hermes_constants.py

CLI_HELP:
- docs/codex_source/vendor/hermes/_raw/cli_help/hermes_profile_help.txt

APPLIES_TO:
- separate Hermes installations
- user-owned state isolation

FACTS:
- profile isolation prevents memory/session/auth collisions between agents.
- profiles can run separate gateways and keep their own state roots.
- cloned profiles preserve user-owned state while replacing distribution-owned content.

CONTRACT:
- use profiles when state must not leak across agents.

NON_GOALS:
- no feature-specific routing

FORBIDDEN_MISUSE:
- assuming a profile clone copies secrets into source control

OPEN_QUESTIONS:
- none

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- local_source_checked: yes
- cli_help_checked: yes
- verified_at_utc: 2026-05-16T10:33:42Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_HERMES_DOCS_EXTRACTION_20260516_01
