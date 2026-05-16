# Hermes memory providers

STATUS: extracted_with_gaps
CATEGORY: vendor/hermes/memory

SOURCE_URLS:
- https://hermes-agent.nousresearch.com/docs/user-guide/features/overview
- https://hermes-agent.nousresearch.com/docs/guides/tips

SOURCE_PATHS:
- docs/codex_source/vendor/hermes/_raw/llms-full.txt

LOCAL_SOURCE_PATHS:
- /opt/openscript-agent-lab/vendor/hermes-agent/agent/memory_provider.py
- /opt/openscript-agent-lab/vendor/hermes-agent/agent/prompt_builder.py

CLI_HELP:
- docs/codex_source/vendor/hermes/_raw/cli_help/hermes_help.txt

APPLIES_TO:
- memory backend selection
- memory provider plugins

FACTS:
- memory providers are part of Hermes' broader agent architecture.
- memory content feeds prompt construction, but it is separate from auth and provider resolution.

CONTRACT:
- memory provider docs should be consulted before changing long-lived context behavior.

NON_GOALS:
- no memory schema rewrite

FORBIDDEN_MISUSE:
- using memory provider state as a routing rule

OPEN_QUESTIONS:
- detailed provider list is omitted here

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- local_source_checked: yes
- cli_help_checked: no
- verified_at_utc: 2026-05-16T10:33:42Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_HERMES_DOCS_EXTRACTION_20260516_01
