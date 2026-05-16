# Hermes OpenAI Codex provider

STATUS: verified
CATEGORY: vendor/hermes/providers

SOURCE_URLS:
- https://hermes-agent.nousresearch.com/docs/integrations/providers
- https://hermes-agent.nousresearch.com/docs/user-guide/features/codex-app-server-runtime

SOURCE_PATHS:
- docs/codex_source/vendor/hermes/_raw/providers.html
- docs/codex_source/vendor/hermes/_raw/codex_app_server_runtime.html
- docs/codex_source/vendor/hermes/_raw/llms-full.txt

LOCAL_SOURCE_PATHS:
- /opt/openscript-agent-lab/vendor/hermes-agent/hermes_cli/providers.py
- /opt/openscript-agent-lab/vendor/hermes-agent/hermes_cli/runtime_provider.py
- /opt/openscript-agent-lab/vendor/hermes-agent/hermes_cli/auth.py
- /opt/openscript-agent-lab/vendor/hermes-agent/agent/transports/codex.py

CLI_HELP:
- docs/codex_source/vendor/hermes/_raw/cli_help/hermes_model_help.txt
- docs/codex_source/vendor/hermes/_raw/cli_help/hermes_auth_help.txt

APPLIES_TO:
- `openai-codex`
- ChatGPT OAuth
- `codex_responses` transport

FACTS:
- the `openai-codex` provider authenticates via ChatGPT/OAuth device code flow.
- Hermes stores the provider auth state in `~/.hermes/auth.json`.
- the provider can route to `codex_responses` in the Hermes transport layer.
- this provider is distinct from the Codex app-server runtime path.

CONTRACT:
- provider docs should be used for provider auth and request routing, not for app-server runtime setup.
- keep provider auth separate from `CODEX_HOME` runtime isolation.

NON_GOALS:
- no API key semantics

FORBIDDEN_MISUSE:
- conflating Codex CLI auth with Hermes provider readiness

OPEN_QUESTIONS:
- none

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- local_source_checked: yes
- cli_help_checked: yes
- verified_at_utc: 2026-05-16T10:33:42Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_HERMES_DOCS_EXTRACTION_20260516_01
