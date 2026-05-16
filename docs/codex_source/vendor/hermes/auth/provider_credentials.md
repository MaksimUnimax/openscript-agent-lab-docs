# Hermes provider credentials

STATUS: extracted
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
- /opt/openscript-agent-lab/vendor/hermes-agent/hermes_cli/runtime_provider.py
- /opt/openscript-agent-lab/vendor/hermes-agent/agent/credential_pool.py

CLI_HELP:
- docs/codex_source/vendor/hermes/_raw/cli_help/hermes_auth_help.txt
- docs/codex_source/vendor/hermes/_raw/cli_help/hermes_auth_status_help.txt

APPLIES_TO:
- provider credential lookup
- auth.json and env-based providers

FACTS:
- Hermes can read credentials from `auth.json`, `.env`, and provider-specific env vars.
- provider runtime should not duplicate credential selection logic in app code.
- some providers use OAuth/device-code, while others use API keys.

CONTRACT:
- keep credential resolution centralized in Hermes runtime code.
- future fix-runs should not hardcode provider secrets or source selection.

NON_GOALS:
- no secret examples
- no provider reimplementation

FORBIDDEN_MISUSE:
- copying credentials into repo docs or task cards

OPEN_QUESTIONS:
- provider-family specifics are documented in sibling provider docs

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- local_source_checked: yes
- cli_help_checked: yes
- verified_at_utc: 2026-05-16T10:33:42Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_HERMES_DOCS_EXTRACTION_20260516_01
