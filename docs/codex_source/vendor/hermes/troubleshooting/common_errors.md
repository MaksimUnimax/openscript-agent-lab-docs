# Hermes common errors

STATUS: extracted_with_gaps
CATEGORY: vendor/hermes/troubleshooting

SOURCE_URLS:
- https://hermes-agent.nousresearch.com/docs/user-guide/faq/

SOURCE_PATHS:
- docs/codex_source/vendor/hermes/_raw/llms-full.txt

LOCAL_SOURCE_PATHS:
- /opt/openscript-agent-lab/vendor/hermes-agent/hermes_cli/auth.py
- /opt/openscript-agent-lab/vendor/hermes-agent/hermes_cli/runtime_provider.py

CLI_HELP:
- docs/codex_source/vendor/hermes/_raw/cli_help/hermes_help.txt

APPLIES_TO:
- generic Hermes error triage

FACTS:
- many common errors are really stale config, stale auth, or missing tool availability.
- central Hermes helpers already contain the logic that should be checked first.

CONTRACT:
- confirm the exact doc path before applying a fix.

NON_GOALS:
- no exhaustive error catalog

FORBIDDEN_MISUSE:
- patching app code before checking the vendor contract

OPEN_QUESTIONS:
- error text evolves with upstream docs

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- local_source_checked: yes
- cli_help_checked: no
- verified_at_utc: 2026-05-16T10:33:42Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_HERMES_DOCS_EXTRACTION_20260516_01
