# Hermes provider runtime resolution

STATUS: verified
CATEGORY: vendor/hermes/providers

SOURCE_URLS:
- https://hermes-agent.nousresearch.com/docs/developer-guide/provider-runtime/
- https://hermes-agent.nousresearch.com/docs/user-guide/features/codex-app-server-runtime

SOURCE_PATHS:
- docs/codex_source/vendor/hermes/_raw/provider_runtime.html
- docs/codex_source/vendor/hermes/_raw/codex_app_server_runtime.html
- docs/codex_source/vendor/hermes/_raw/llms-full.txt

LOCAL_SOURCE_PATHS:
- /opt/openscript-agent-lab/vendor/hermes-agent/hermes_cli/runtime_provider.py
- /opt/openscript-agent-lab/vendor/hermes-agent/hermes_cli/model_switch.py
- /opt/openscript-agent-lab/vendor/hermes-agent/hermes_cli/providers.py
- /opt/openscript-agent-lab/vendor/hermes-agent/hermes_cli/auth.py

CLI_HELP:
- docs/codex_source/vendor/hermes/_raw/cli_help/hermes_model_help.txt

APPLIES_TO:
- runtime provider resolution
- model switching
- api_mode derivation

FACTS:
- runtime resolution is handled centrally by Hermes helpers such as `resolve_runtime_provider` and model-switch helpers.
- explicit runtime/model requests have higher priority than stale persisted defaults.
- `config.yaml`, env vars, provider defaults, base URLs, and `api_mode` are resolved in Hermes code, not in app code.
- `ProviderProfile` and provider registry state are part of that resolution path.

CONTRACT:
- do not duplicate provider resolution in route handlers or integrations.
- if provider resolution changes, update the centralized Hermes docs first.

NON_GOALS:
- no provider plugin authoring guide

FORBIDDEN_MISUSE:
- relying on stale `api_mode` without verifying the provider family

OPEN_QUESTIONS:
- exact precedence details for every provider family remain in Hermes code and raw docs

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- local_source_checked: yes
- cli_help_checked: yes
- verified_at_utc: 2026-05-16T10:33:42Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_HERMES_DOCS_EXTRACTION_20260516_01
