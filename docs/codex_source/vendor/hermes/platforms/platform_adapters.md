# Hermes platform adapters

STATUS: extracted_with_gaps
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
- adapter registration
- platform toolsets

FACTS:
- platform adapters are surfaced through toolset and gateway machinery.
- the adapter layer is distinct from provider/runtime resolution.

CONTRACT:
- adapter docs should be used for platform-specific routing and limits.

NON_GOALS:
- no adapter SDK docs

FORBIDDEN_MISUSE:
- collapsing all platform behavior into a single code path without docs

OPEN_QUESTIONS:
- platform registration specifics can vary by plugin/backend

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- local_source_checked: yes
- cli_help_checked: yes
- verified_at_utc: 2026-05-16T10:33:42Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_HERMES_DOCS_EXTRACTION_20260516_01
