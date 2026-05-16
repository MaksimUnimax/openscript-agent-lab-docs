# Hermes custom providers

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
- named custom providers
- config.yaml provider entries

FACTS:
- Hermes supports named custom provider entries in configuration.
- custom providers use the same runtime/provider resolution path as built-ins.
- provider configuration includes base URL and api_mode resolution.

CONTRACT:
- custom providers should not require app-level routing branches.

NON_GOALS:
- no provider marketplace design

FORBIDDEN_MISUSE:
- assuming custom provider config can replace vendor docs

OPEN_QUESTIONS:
- exact custom-provider examples are omitted here on purpose

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- local_source_checked: yes
- cli_help_checked: yes
- verified_at_utc: 2026-05-16T10:33:42Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_HERMES_DOCS_EXTRACTION_20260516_01
