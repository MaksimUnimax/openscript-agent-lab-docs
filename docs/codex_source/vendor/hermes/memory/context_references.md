# Hermes context references

STATUS: extracted_with_gaps
CATEGORY: vendor/hermes/memory

SOURCE_URLS:
- https://hermes-agent.nousresearch.com/docs/guides/tips

SOURCE_PATHS:
- docs/codex_source/vendor/hermes/_raw/llms-full.txt

LOCAL_SOURCE_PATHS:
- /opt/openscript-agent-lab/vendor/hermes-agent/agent/prompt_builder.py
- /opt/openscript-agent-lab/vendor/hermes-agent/agent/memory_provider.py

CLI_HELP:
- docs/codex_source/vendor/hermes/_raw/cli_help/hermes_help.txt

APPLIES_TO:
- prompt context assembly
- memory-backed references

FACTS:
- context references are part of Hermes' prompt building flow.
- they should be treated as runtime context, not as vendor documentation.

CONTRACT:
- do not use context references as a substitute for extracted docs.

NON_GOALS:
- no citation system design

FORBIDDEN_MISUSE:
- promoting runtime context into docs without extraction

OPEN_QUESTIONS:
- exact memory reference format is omitted here

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- local_source_checked: yes
- cli_help_checked: no
- verified_at_utc: 2026-05-16T10:33:42Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_HERMES_DOCS_EXTRACTION_20260516_01
