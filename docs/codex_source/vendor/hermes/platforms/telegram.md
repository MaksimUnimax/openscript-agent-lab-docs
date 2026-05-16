# Hermes Telegram platform

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
- Telegram gateway adapter
- platform toolset

FACTS:
- Telegram is one of Hermes' supported messaging platform adapters.
- Telegram platform behavior is mediated by gateway runtime and toolset configuration.

CONTRACT:
- Telegram platform docs are not a substitute for Telegram Bot API docs.

NON_GOALS:
- no Bot API deep dive

FORBIDDEN_MISUSE:
- confusing Telegram chat routing with access control policy

OPEN_QUESTIONS:
- detailed Telegram behavior belongs in Telegram vendor docs

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- local_source_checked: yes
- cli_help_checked: yes
- verified_at_utc: 2026-05-16T10:33:42Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_HERMES_DOCS_EXTRACTION_20260516_01
