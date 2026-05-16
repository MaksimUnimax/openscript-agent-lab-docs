# Hermes Windows / WSL

STATUS: extracted_with_gaps
CATEGORY: vendor/hermes/troubleshooting

SOURCE_URLS:
- https://hermes-agent.nousresearch.com/docs/user-guide/windows-native
- https://hermes-agent.nousresearch.com/docs/user-guide/windows-wsl-quickstart

SOURCE_PATHS:
- docs/codex_source/vendor/hermes/_raw/llms-full.txt

LOCAL_SOURCE_PATHS:
- /opt/openscript-agent-lab/vendor/hermes-agent/hermes_constants.py
- /opt/openscript-agent-lab/vendor/hermes-agent/hermes_cli/profiles.py

CLI_HELP:
- docs/codex_source/vendor/hermes/_raw/cli_help/hermes_help.txt

APPLIES_TO:
- Windows installs
- WSL installs

FACTS:
- Hermes supports both native Windows and WSL-style state layouts.
- state roots and home paths are platform-sensitive but remain profile-scoped.

CONTRACT:
- Windows/WSL guidance should be used before assuming a path or shell behavior.

NON_GOALS:
- no installation script walkthrough

FORBIDDEN_MISUSE:
- assuming Linux path semantics without checking the platform doc

OPEN_QUESTIONS:
- detailed shell path mapping is intentionally omitted

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- local_source_checked: yes
- cli_help_checked: no
- verified_at_utc: 2026-05-16T10:33:42Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_HERMES_DOCS_EXTRACTION_20260516_01
