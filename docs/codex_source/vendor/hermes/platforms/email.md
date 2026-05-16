# Hermes email platform

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
- email adapter

FACTS:
- Hermes includes an email messaging adapter family.
- gateway and toolset mechanics are shared with the broader messaging layer.

CONTRACT:
- email adapter behavior should be read from platform docs before changes.

NON_GOALS:
- no SMTP/IMAP walkthrough

FORBIDDEN_MISUSE:
- using email docs as a substitute for general runtime docs

OPEN_QUESTIONS:
- exact adapter integration is out of scope

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- local_source_checked: yes
- cli_help_checked: yes
- verified_at_utc: 2026-05-16T10:33:42Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_HERMES_DOCS_EXTRACTION_20260516_01
