# Hermes Discord platform

STATUS: extracted_with_gaps
CATEGORY: vendor/hermes/platforms

SOURCE_URLS:
- https://hermes-agent.nousresearch.com/docs/user-guide/messaging/

SOURCE_PATHS:
- docs/codex_source/vendor/hermes/_raw/llms-full.txt

LOCAL_SOURCE_PATHS:
- /opt/openscript-agent-lab/vendor/hermes-agent/toolsets.py
- /opt/openscript-agent-lab/vendor/hermes-agent/gateway/run.py

CLI_HELP:
- docs/codex_source/vendor/hermes/_raw/cli_help/hermes_gateway_help.txt

APPLIES_TO:
- Discord gateway adapter

FACTS:
- Discord is a supported Hermes messaging platform.
- it shares the gateway/toolset architecture with other platforms.

CONTRACT:
- platform-specific docs must be read for adapter behavior.

NON_GOALS:
- no Discord Bot API tutorial

FORBIDDEN_MISUSE:
- assuming Telegram rules apply unchanged to Discord

OPEN_QUESTIONS:
- adapter-specific limits are out of scope here

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- local_source_checked: yes
- cli_help_checked: yes
- verified_at_utc: 2026-05-16T10:33:42Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_HERMES_DOCS_EXTRACTION_20260516_01
