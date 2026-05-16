# Hermes configuration

STATUS: verified
CATEGORY: vendor/hermes/overview

SOURCE_URLS:
- https://hermes-agent.nousresearch.com/docs/user-guide/configuration
- https://hermes-agent.nousresearch.com/docs/reference/environment-variables

SOURCE_PATHS:
- docs/codex_source/vendor/hermes/_raw/environment_variables.html
- docs/codex_source/vendor/hermes/_raw/llms-full.txt

LOCAL_SOURCE_PATHS:
- /opt/openscript-agent-lab/vendor/hermes-agent/hermes_constants.py
- /opt/openscript-agent-lab/vendor/hermes-agent/hermes_cli/auth.py
- /opt/openscript-agent-lab/vendor/hermes-agent/hermes_cli/runtime_provider.py

CLI_HELP:
- docs/codex_source/vendor/hermes/_raw/cli_help/hermes_help.txt

APPLIES_TO:
- config.yaml
- .env
- Hermes home layout

FACTS:
- `config.yaml` carries non-secret settings.
- `.env` carries secrets and runtime env overrides.
- `HERMES_HOME` controls where Hermes reads and writes state.
- `HERMES_OAUTH_FILE` defaults to `~/.hermes/auth.json`.

CONTRACT:
- secrets stay out of docs and index entries.
- project docs never replace configuration docs.

NON_GOALS:
- no secret values
- no file contents from auth.json

FORBIDDEN_MISUSE:
- treating config docs as runtime state

OPEN_QUESTIONS:
- exact downstream per-profile override behavior is captured in profile docs

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- local_source_checked: yes
- cli_help_checked: yes
- verified_at_utc: 2026-05-16T10:33:42Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_HERMES_DOCS_EXTRACTION_20260516_01
