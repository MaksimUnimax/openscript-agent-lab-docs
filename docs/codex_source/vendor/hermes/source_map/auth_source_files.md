# Hermes auth source files

STATUS: extracted
CATEGORY: vendor/hermes/source_map

SOURCE_URLS:
- none

SOURCE_PATHS:
- none

LOCAL_SOURCE_PATHS:
- /opt/openscript-agent-lab/vendor/hermes-agent/hermes_cli/auth.py
- /opt/openscript-agent-lab/vendor/hermes-agent/agent/credential_sources.py
- /opt/openscript-agent-lab/vendor/hermes-agent/agent/credential_pool.py

CLI_HELP:
- docs/codex_source/vendor/hermes/_raw/cli_help/hermes_auth_help.txt
- docs/codex_source/vendor/hermes/_raw/cli_help/hermes_auth_add_help.txt
- docs/codex_source/vendor/hermes/_raw/cli_help/hermes_auth_status_help.txt

APPLIES_TO:
- openai-codex auth
- auth.json persistence
- credential pool sync

FACTS:
- `auth.py` owns provider auth store persistence and login flows.
- `credential_sources.py` maps removal/suppression behavior for provider credential sources.
- `credential_pool.py` syncs live tokens back to auth state.
- openai-codex helpers include `_import_codex_cli_tokens`, `_save_codex_tokens`, and `_login_openai_codex`.

CONTRACT:
- use these files as the implementation boundary for auth docs.

NON_GOALS:
- no secret inspection

FORBIDDEN_MISUSE:
- treating auth file names as proof of live readiness

OPEN_QUESTIONS:
- none

VERIFICATION:
- raw_source_saved: no
- official_docs_checked: no
- local_source_checked: yes
- cli_help_checked: yes
- verified_at_utc: 2026-05-16T10:33:42Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_HERMES_DOCS_EXTRACTION_20260516_01
