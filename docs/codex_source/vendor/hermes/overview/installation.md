# Hermes installation

STATUS: extracted
CATEGORY: vendor/hermes/overview

SOURCE_URLS:
- https://hermes-agent.nousresearch.com/docs/
- https://hermes-agent.nousresearch.com/docs/user-guide/windows-wsl-quickstart

SOURCE_PATHS:
- docs/codex_source/vendor/hermes/_raw/docs_root.html
- docs/codex_source/vendor/hermes/_raw/llms-full.txt

LOCAL_SOURCE_PATHS:
- /opt/openscript-agent-lab/vendor/hermes-agent/hermes_constants.py
- /opt/openscript-agent-lab/vendor/hermes-agent/hermes_cli/profiles.py

CLI_HELP:
- docs/codex_source/vendor/hermes/_raw/cli_help/hermes_help.txt

APPLIES_TO:
- Hermes home layout
- profile creation

FACTS:
- Hermes uses `~/.hermes` by default and honors `HERMES_HOME`.
- profile installs and clones preserve user-owned state such as auth, memories, sessions, and logs.
- Windows and WSL installations use the same state-shape idea, with platform-specific roots.

CONTRACT:
- install docs must be read before assuming file layout.
- profile data and auth data are not vendor source of truth.

NON_GOALS:
- no code patching
- no auth flow changes

FORBIDDEN_MISUSE:
- using install docs to justify changing runtime code paths

OPEN_QUESTIONS:
- exact package-management steps are outside this extraction

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- local_source_checked: yes
- cli_help_checked: yes
- verified_at_utc: 2026-05-16T10:33:42Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_HERMES_DOCS_EXTRACTION_20260516_01
