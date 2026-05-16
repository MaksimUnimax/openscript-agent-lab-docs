# Hermes runtime source files

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
- /opt/openscript-agent-lab/vendor/hermes-agent/agent/transports/codex.py
- /opt/openscript-agent-lab/vendor/hermes-agent/agent/auxiliary_client.py

CLI_HELP:
- docs/codex_source/vendor/hermes/_raw/cli_help/hermes_gateway_help.txt

APPLIES_TO:
- gateway runtime
- API server runtime
- Codex app-server transport

FACTS:
- `config.py` contains API server/gateway configuration parsing.
- `run.py` is the gateway runtime entrypoint.
- `api_server.py` implements the local API server surface.
- `codex.py` and `auxiliary_client.py` connect the app-server path to Hermes runtime.

CONTRACT:
- runtime docs should point at these files rather than duplicate the behavior.

NON_GOALS:
- no runtime execution instructions

FORBIDDEN_MISUSE:
- using runtime source maps to bypass docs

OPEN_QUESTIONS:
- none

VERIFICATION:
- raw_source_saved: no
- official_docs_checked: no
- local_source_checked: yes
- cli_help_checked: yes
- verified_at_utc: 2026-05-16T10:33:42Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_HERMES_DOCS_EXTRACTION_20260516_01
