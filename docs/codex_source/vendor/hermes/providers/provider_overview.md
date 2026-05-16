# Hermes provider overview

STATUS: verified
CATEGORY: vendor/hermes/providers

SOURCE_URLS:
- https://hermes-agent.nousresearch.com/docs/integrations/providers
- https://hermes-agent.nousresearch.com/docs/reference/environment-variables

SOURCE_PATHS:
- docs/codex_source/vendor/hermes/_raw/providers.html
- docs/codex_source/vendor/hermes/_raw/environment_variables.html
- docs/codex_source/vendor/hermes/_raw/llms-full.txt

LOCAL_SOURCE_PATHS:
- /opt/openscript-agent-lab/vendor/hermes-agent/hermes_cli/providers.py
- /opt/openscript-agent-lab/vendor/hermes-agent/hermes_cli/runtime_provider.py
- /opt/openscript-agent-lab/vendor/hermes-agent/hermes_cli/model_switch.py

CLI_HELP:
- docs/codex_source/vendor/hermes/_raw/cli_help/hermes_model_help.txt

APPLIES_TO:
- provider registry
- provider selection
- api_mode selection

FACTS:
- Hermes keeps provider selection centralized in runtime/provider helpers.
- provider choices include built-ins, OpenAI-compatible paths, OAuth providers, and named custom providers.
- `openai-codex` is a built-in provider with a dedicated transport mode.

CONTRACT:
- app code should call the runtime/provider helpers, not reimplement provider resolution.
- provider selection is a runtime concern, not a docs-layer guess.

NON_GOALS:
- no exhaustive provider catalog

FORBIDDEN_MISUSE:
- hardcoding provider-specific routing in application code

OPEN_QUESTIONS:
- provider family details belong in the sibling docs

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- local_source_checked: yes
- cli_help_checked: yes
- verified_at_utc: 2026-05-16T10:33:42Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_HERMES_DOCS_EXTRACTION_20260516_01
