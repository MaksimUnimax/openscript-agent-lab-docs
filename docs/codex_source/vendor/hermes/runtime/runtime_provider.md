# Hermes runtime provider

STATUS: verified
CATEGORY: vendor/hermes/runtime

SOURCE_URLS:
- https://hermes-agent.nousresearch.com/docs/developer-guide/provider-runtime/

SOURCE_PATHS:
- docs/codex_source/vendor/hermes/_raw/provider_runtime.html
- docs/codex_source/vendor/hermes/_raw/llms-full.txt

LOCAL_SOURCE_PATHS:
- /opt/openscript-agent-lab/vendor/hermes-agent/hermes_cli/runtime_provider.py
- /opt/openscript-agent-lab/vendor/hermes-agent/hermes_cli/providers.py

CLI_HELP:
- docs/codex_source/vendor/hermes/_raw/cli_help/hermes_model_help.txt

APPLIES_TO:
- runtime provider resolution
- api_mode derivation

FACTS:
- runtime provider helpers derive provider family, base URL, and api_mode together.
- the resolution path exists so app code does not need duplicate branching.

CONTRACT:
- use the runtime provider helper as the single source of truth for provider runtime decisions.

NON_GOALS:
- no direct model API implementation

FORBIDDEN_MISUSE:
- copying provider-resolution logic into route code or prompt text

OPEN_QUESTIONS:
- none

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- local_source_checked: yes
- cli_help_checked: yes
- verified_at_utc: 2026-05-16T10:33:42Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_HERMES_DOCS_EXTRACTION_20260516_01
