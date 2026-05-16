# Hermes messaging overview

STATUS: extracted
CATEGORY: vendor/hermes/platforms

SOURCE_URLS:
- https://hermes-agent.nousresearch.com/docs/user-guide/messaging/
- https://hermes-agent.nousresearch.com/docs/reference/toolsets-reference/

SOURCE_PATHS:
- docs/codex_source/vendor/hermes/_raw/llms-full.txt

LOCAL_SOURCE_PATHS:
- /opt/openscript-agent-lab/vendor/hermes-agent/toolsets.py
- /opt/openscript-agent-lab/vendor/hermes-agent/gateway/run.py

CLI_HELP:
- docs/codex_source/vendor/hermes/_raw/cli_help/hermes_gateway_help.txt

APPLIES_TO:
- gateway-backed chat platforms
- messaging adapters

FACTS:
- Hermes has a messaging platform layer separate from provider/runtime selection.
- platform adapters are exposed through toolsets and the gateway runtime.

CONTRACT:
- messaging docs are platform contracts, not auth docs.

NON_GOALS:
- no platform-specific onboarding guide

FORBIDDEN_MISUSE:
- using one platform's semantics as if they applied to all

OPEN_QUESTIONS:
- exact platform list lives in sibling docs

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- local_source_checked: yes
- cli_help_checked: yes
- verified_at_utc: 2026-05-16T10:33:42Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_HERMES_DOCS_EXTRACTION_20260516_01
