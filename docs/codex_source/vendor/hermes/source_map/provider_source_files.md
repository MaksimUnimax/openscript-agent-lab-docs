# Hermes provider source files

STATUS: extracted
CATEGORY: vendor/hermes/source_map

SOURCE_URLS:
- none

SOURCE_PATHS:
- none

LOCAL_SOURCE_PATHS:
- /opt/openscript-agent-lab/vendor/hermes-agent/hermes_cli/runtime_provider.py
- /opt/openscript-agent-lab/vendor/hermes-agent/hermes_cli/providers.py
- /opt/openscript-agent-lab/vendor/hermes-agent/hermes_cli/model_switch.py

CLI_HELP:
- docs/codex_source/vendor/hermes/_raw/cli_help/hermes_model_help.txt

APPLIES_TO:
- provider registry
- runtime provider resolution
- api_mode selection

FACTS:
- `runtime_provider.py` contains the central runtime provider resolver.
- `providers.py` carries provider/transport metadata and helper functions.
- `model_switch.py` reuses the same provider logic for `/model`.

CONTRACT:
- keep provider resolution logic centralized in these files.

NON_GOALS:
- no provider plugin implementation

FORBIDDEN_MISUSE:
- duplicating `api_mode` selection in app-layer code

OPEN_QUESTIONS:
- none

VERIFICATION:
- raw_source_saved: no
- official_docs_checked: no
- local_source_checked: yes
- cli_help_checked: yes
- verified_at_utc: 2026-05-16T10:33:42Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_HERMES_DOCS_EXTRACTION_20260516_01
