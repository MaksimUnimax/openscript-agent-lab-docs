# Hermes Nous Portal provider

STATUS: extracted
CATEGORY: vendor/hermes/providers

SOURCE_URLS:
- https://hermes-agent.nousresearch.com/docs/integrations/providers

SOURCE_PATHS:
- docs/codex_source/vendor/hermes/_raw/providers.html
- docs/codex_source/vendor/hermes/_raw/llms-full.txt

LOCAL_SOURCE_PATHS:
- /opt/openscript-agent-lab/vendor/hermes-agent/hermes_cli/providers.py
- /opt/openscript-agent-lab/vendor/hermes-agent/hermes_cli/auth.py

CLI_HELP:
- docs/codex_source/vendor/hermes/_raw/cli_help/hermes_model_help.txt

APPLIES_TO:
- Nous Portal provider selection
- OAuth/device-code flows

FACTS:
- Nous Portal is a documented Hermes provider family.
- it uses Hermes' centralized provider/runtime path rather than app-local routing.

CONTRACT:
- provider family specifics should be read from Hermes docs, not from route code.

NON_GOALS:
- no account or billing instructions

FORBIDDEN_MISUSE:
- assuming Nous Portal shares auth state with unrelated providers

OPEN_QUESTIONS:
- exact endpoint mappings are outside this extraction

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- local_source_checked: yes
- cli_help_checked: yes
- verified_at_utc: 2026-05-16T10:33:42Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_HERMES_DOCS_EXTRACTION_20260516_01
