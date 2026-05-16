# Hermes OpenRouter provider

STATUS: extracted
CATEGORY: vendor/hermes/providers

SOURCE_URLS:
- https://hermes-agent.nousresearch.com/docs/integrations/providers
- https://hermes-agent.nousresearch.com/docs/reference/environment-variables

SOURCE_PATHS:
- docs/codex_source/vendor/hermes/_raw/providers.html
- docs/codex_source/vendor/hermes/_raw/environment_variables.html

LOCAL_SOURCE_PATHS:
- /opt/openscript-agent-lab/vendor/hermes-agent/hermes_cli/providers.py
- /opt/openscript-agent-lab/vendor/hermes-agent/hermes_cli/runtime_provider.py

CLI_HELP:
- docs/codex_source/vendor/hermes/_raw/cli_help/hermes_model_help.txt

APPLIES_TO:
- OpenRouter provider selection
- OpenRouter env vars

FACTS:
- Hermes exposes OpenRouter as a first-class provider family.
- OpenRouter setup is resolved through the same central provider logic as the rest of Hermes.
- response caching and base-url overrides are documented as environment-variable controls.

CONTRACT:
- use the provider docs for exact env names and base URL semantics.

NON_GOALS:
- no OpenRouter account setup instructions

FORBIDDEN_MISUSE:
- copying API keys or assuming an env var is always required

OPEN_QUESTIONS:
- exact model mappings are provider specific

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- local_source_checked: yes
- cli_help_checked: yes
- verified_at_utc: 2026-05-16T10:33:42Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_HERMES_DOCS_EXTRACTION_20260516_01
