# Hermes OpenAI Codex auth

STATUS: verified
CATEGORY: vendor/hermes/auth

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
- /opt/openscript-agent-lab/vendor/hermes-agent/agent/credential_pool.py

CLI_HELP:
- docs/codex_source/vendor/hermes/_raw/cli_help/hermes_auth_help.txt
- docs/codex_source/vendor/hermes/_raw/cli_help/hermes_auth_add_help.txt

APPLIES_TO:
- `openai-codex` provider login
- Hermes-managed OAuth/device-code flow
- Codex CLI auth import/adopt

FACTS:
- Hermes stores openai-codex credentials in `~/.hermes/auth.json`.
- the Codex CLI store at `~/.codex/auth.json` is separate.
- if Codex CLI credentials exist, Hermes can import them rather than forcing a fresh login.
- app-server runtime and provider auth are distinct concepts.
- device-code flow is used for openai-codex auth.

CONTRACT:
- use Hermes auth state for provider readiness checks.
- keep Codex CLI session state isolated from Hermes provider state.

NON_GOALS:
- no provider routing changes
- no secret values

FORBIDDEN_MISUSE:
- confusing Codex CLI auth presence with Hermes live authorization

OPEN_QUESTIONS:
- none for the auth-store boundary itself

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- local_source_checked: yes
- cli_help_checked: yes
- verified_at_utc: 2026-05-16T10:33:42Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_HERMES_DOCS_EXTRACTION_20260516_01
