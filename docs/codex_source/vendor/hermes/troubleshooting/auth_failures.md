# Hermes auth failures

STATUS: verified
CATEGORY: vendor/hermes/troubleshooting

SOURCE_URLS:
- https://hermes-agent.nousresearch.com/docs/integrations/providers
- https://hermes-agent.nousresearch.com/docs/user-guide/features/codex-app-server-runtime

SOURCE_PATHS:
- docs/codex_source/vendor/hermes/_raw/providers.html
- docs/codex_source/vendor/hermes/_raw/codex_app_server_runtime.html
- docs/codex_source/vendor/hermes/_raw/llms-full.txt

LOCAL_SOURCE_PATHS:
- /opt/openscript-agent-lab/vendor/hermes-agent/hermes_cli/auth.py
- /opt/openscript-agent-lab/vendor/hermes-agent/agent/credential_sources.py

CLI_HELP:
- docs/codex_source/vendor/hermes/_raw/cli_help/hermes_auth_help.txt
- docs/codex_source/vendor/hermes/_raw/cli_help/hermes_auth_status_help.txt

APPLIES_TO:
- token invalidation
- device-code login failures
- Codex CLI import/adopt

FACTS:
- auth failures can occur even when token files exist.
- device-code login and Codex CLI import are explicit auth flows.
- `auth status` is the right place to check state before assuming readiness.

CONTRACT:
- auth failures must be handled as provider readiness issues, not as app-route issues.

NON_GOALS:
- no credential repair automation

FORBIDDEN_MISUSE:
- treating stale file presence as success

OPEN_QUESTIONS:
- provider-specific errors are documented in sibling docs

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- local_source_checked: yes
- cli_help_checked: yes
- verified_at_utc: 2026-05-16T10:33:42Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_HERMES_DOCS_EXTRACTION_20260516_01
