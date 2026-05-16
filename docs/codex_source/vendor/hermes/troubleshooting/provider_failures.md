# Hermes provider failures

STATUS: extracted_with_gaps
CATEGORY: vendor/hermes/troubleshooting

SOURCE_URLS:
- https://hermes-agent.nousresearch.com/docs/developer-guide/provider-runtime/
- https://hermes-agent.nousresearch.com/docs/integrations/providers

SOURCE_PATHS:
- docs/codex_source/vendor/hermes/_raw/provider_runtime.html
- docs/codex_source/vendor/hermes/_raw/providers.html
- docs/codex_source/vendor/hermes/_raw/llms-full.txt

LOCAL_SOURCE_PATHS:
- /opt/openscript-agent-lab/vendor/hermes-agent/hermes_cli/runtime_provider.py
- /opt/openscript-agent-lab/vendor/hermes-agent/hermes_cli/model_switch.py

CLI_HELP:
- docs/codex_source/vendor/hermes/_raw/cli_help/hermes_model_help.txt

APPLIES_TO:
- provider resolution failures
- api_mode mismatch

FACTS:
- provider failures often come from mismatched provider/base-url/api_mode combinations.
- Hermes resolves these centrally so the model layer can stay consistent.

CONTRACT:
- fix provider failures by checking runtime-provider resolution first.

NON_GOALS:
- no provider fallback redesign

FORBIDDEN_MISUSE:
- masking provider failures as application bugs without checking the provider layer

OPEN_QUESTIONS:
- exact provider-family error messages are outside this doc

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- local_source_checked: yes
- cli_help_checked: yes
- verified_at_utc: 2026-05-16T10:33:42Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_HERMES_DOCS_EXTRACTION_20260516_01
