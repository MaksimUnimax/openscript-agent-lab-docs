# Hermes gateway source files

STATUS: extracted
CATEGORY: vendor/hermes/source_map

SOURCE_URLS:
- none

SOURCE_PATHS:
- none

LOCAL_SOURCE_PATHS:
- /opt/openscript-agent-lab/vendor/hermes-agent/gateway/config.py
- /opt/openscript-agent-lab/vendor/hermes-agent/gateway/run.py
- /opt/openscript-agent-lab/vendor/hermes-agent/gateway/platforms/api_server.py

CLI_HELP:
- docs/codex_source/vendor/hermes/_raw/cli_help/hermes_gateway_help.txt

APPLIES_TO:
- gateway configuration
- API server behavior
- platform adapters

FACTS:
- `config.py` parses gateway and API server env vars.
- `run.py` starts the gateway runtime.
- `api_server.py` owns the API server contract and auth/CORS behavior.

CONTRACT:
- gateway docs should cite these files directly.

NON_GOALS:
- no transport-layer source reproduction

FORBIDDEN_MISUSE:
- treating the gateway source map as a deployment script

OPEN_QUESTIONS:
- none

VERIFICATION:
- raw_source_saved: no
- official_docs_checked: no
- local_source_checked: yes
- cli_help_checked: yes
- verified_at_utc: 2026-05-16T10:33:42Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_HERMES_DOCS_EXTRACTION_20260516_01
