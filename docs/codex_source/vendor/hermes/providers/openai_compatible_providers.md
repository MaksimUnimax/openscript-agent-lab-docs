# Hermes OpenAI-compatible providers

STATUS: extracted
CATEGORY: vendor/hermes/providers

SOURCE_URLS:
- https://hermes-agent.nousresearch.com/docs/integrations/providers
- https://hermes-agent.nousresearch.com/docs/reference/environment-variables

SOURCE_PATHS:
- docs/codex_source/vendor/hermes/_raw/providers.html
- docs/codex_source/vendor/hermes/_raw/environment_variables.html
- docs/codex_source/vendor/hermes/_raw/llms-full.txt

LOCAL_SOURCE_PATHS:
- /opt/openscript-agent-lab/vendor/hermes-agent/hermes_cli/runtime_provider.py
- /opt/openscript-agent-lab/vendor/hermes-agent/hermes_cli/providers.py

CLI_HELP:
- docs/codex_source/vendor/hermes/_raw/cli_help/hermes_model_help.txt

APPLIES_TO:
- OpenAI-compatible base URLs
- custom endpoints
- api_mode fallback

FACTS:
- Hermes supports OpenAI-compatible providers through the same runtime resolution layer.
- base URL and api_mode determine how the request is shaped.
- `determine_api_mode` and runtime helpers are the authoritative path.

CONTRACT:
- OpenAI-compatible behavior must stay centralized in Hermes provider helpers.

NON_GOALS:
- no vendor-specific API key storage

FORBIDDEN_MISUSE:
- assuming all OpenAI-compatible endpoints share the same transport mode

OPEN_QUESTIONS:
- endpoint-specific fallbacks belong in sibling provider docs

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- local_source_checked: yes
- cli_help_checked: yes
- verified_at_utc: 2026-05-16T10:33:42Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_HERMES_DOCS_EXTRACTION_20260516_01
