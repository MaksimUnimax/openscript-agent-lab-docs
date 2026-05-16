# Hermes fallback providers

STATUS: extracted_with_gaps
CATEGORY: vendor/hermes/providers

SOURCE_URLS:
- https://hermes-agent.nousresearch.com/docs/integrations/providers
- https://hermes-agent.nousresearch.com/docs/reference/environment-variables

SOURCE_PATHS:
- docs/codex_source/vendor/hermes/_raw/providers.html
- docs/codex_source/vendor/hermes/_raw/llms-full.txt

LOCAL_SOURCE_PATHS:
- /opt/openscript-agent-lab/vendor/hermes-agent/hermes_cli/runtime_provider.py
- /opt/openscript-agent-lab/vendor/hermes-agent/hermes_cli/model_switch.py

CLI_HELP:
- docs/codex_source/vendor/hermes/_raw/cli_help/hermes_model_help.txt

APPLIES_TO:
- provider fallback resolution
- stale config avoidance

FACTS:
- Hermes has fallback behavior when the requested provider cannot be resolved as configured.
- runtime helpers avoid blindly reusing stale provider/api_mode combinations.

CONTRACT:
- fallback docs should be read before assuming a direct provider switch is safe.

NON_GOALS:
- no exhaustive fallback matrix

FORBIDDEN_MISUSE:
- hardcoding fallback semantics in app routes

OPEN_QUESTIONS:
- exact fallback precedence can vary by provider family and needs live code/context

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- local_source_checked: yes
- cli_help_checked: yes
- verified_at_utc: 2026-05-16T10:33:42Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_HERMES_DOCS_EXTRACTION_20260516_01
