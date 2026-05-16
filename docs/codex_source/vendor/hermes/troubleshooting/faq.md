# Hermes FAQ

STATUS: extracted_with_gaps
CATEGORY: vendor/hermes/troubleshooting

SOURCE_URLS:
- https://hermes-agent.nousresearch.com/docs/user-guide/faq/

SOURCE_PATHS:
- docs/codex_source/vendor/hermes/_raw/llms-full.txt

LOCAL_SOURCE_PATHS:
- /opt/openscript-agent-lab/vendor/hermes-agent/hermes_cli/auth.py
- /opt/openscript-agent-lab/vendor/hermes-agent/hermes_cli/runtime_provider.py
- /opt/openscript-agent-lab/vendor/hermes-agent/hermes_cli/profiles.py

CLI_HELP:
- docs/codex_source/vendor/hermes/_raw/cli_help/hermes_help.txt

APPLIES_TO:
- common Hermes failure triage

FACTS:
- FAQ content is a quick reference, not a substitute for vendor docs.
- common problems cluster around auth, provider resolution, profiles, and platform setup.

CONTRACT:
- use FAQ docs for triage, then read the exact underlying vendor doc.

NON_GOALS:
- no support desk policy

FORBIDDEN_MISUSE:
- treating FAQ answers as authoritative for code changes

OPEN_QUESTIONS:
- exact FAQ coverage may change with upstream docs

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- local_source_checked: yes
- cli_help_checked: no
- verified_at_utc: 2026-05-16T10:33:42Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_HERMES_DOCS_EXTRACTION_20260516_01
