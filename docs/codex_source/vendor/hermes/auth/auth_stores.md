# Hermes auth stores

STATUS: verified
CATEGORY: vendor/hermes/auth

SOURCE_URLS:
- https://hermes-agent.nousresearch.com/docs/integrations/providers
- https://hermes-agent.nousresearch.com/docs/reference/environment-variables

SOURCE_PATHS:
- docs/codex_source/vendor/hermes/_raw/providers.html
- docs/codex_source/vendor/hermes/_raw/environment_variables.html
- docs/codex_source/vendor/hermes/_raw/llms-full.txt

LOCAL_SOURCE_PATHS:
- /opt/openscript-agent-lab/vendor/hermes-agent/hermes_cli/auth.py
- /opt/openscript-agent-lab/vendor/hermes-agent/agent/credential_sources.py
- /opt/openscript-agent-lab/vendor/hermes-agent/agent/credential_pool.py

CLI_HELP:
- docs/codex_source/vendor/hermes/_raw/cli_help/hermes_auth_help.txt
- docs/codex_source/vendor/hermes/_raw/cli_help/hermes_auth_status_help.txt

APPLIES_TO:
- `~/.hermes/auth.json`
- credential pool persistence
- refresh and invalidation semantics

FACTS:
- Hermes auth state is persisted under the Hermes home directory.
- auth pool entries can be synchronized from file-backed state and written back after refresh.
- Codex device-code entries are special because Hermes also mirrors them against the Codex CLI store.

CONTRACT:
- auth store docs are the canonical place for provider token persistence.
- do not use profile memory or chat history as auth storage.

NON_GOALS:
- no runtime provider resolution logic

FORBIDDEN_MISUSE:
- assuming file existence alone means live readiness

OPEN_QUESTIONS:
- exact refresh semantics for each provider family belong in provider-specific docs

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- local_source_checked: yes
- cli_help_checked: yes
- verified_at_utc: 2026-05-16T10:33:42Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_HERMES_DOCS_EXTRACTION_20260516_01
