# Codex CLI import/adopt

STATUS: verified
CATEGORY: vendor/hermes/auth

SOURCE_URLS:
- https://hermes-agent.nousresearch.com/docs/integrations/providers
- https://hermes-agent.nousresearch.com/docs/user-guide/features/codex-app-server-runtime

SOURCE_PATHS:
- docs/codex_source/vendor/hermes/_raw/providers.html
- docs/codex_source/vendor/hermes/_raw/codex_app_server_runtime.html
- docs/codex_source/vendor/hermes/_raw/llms-full.txt

LOCAL_SOURCE_PATHS:
- /opt/openscript-agent-lab/vendor/hermes-agent/hermes_cli/auth.py
- /opt/openscript-agent-lab/vendor/hermes-agent/agent/credential_sources.py
- /opt/openscript-agent-lab/vendor/hermes-agent/agent/credential_pool.py

CLI_HELP:
- docs/codex_source/vendor/hermes/_raw/cli_help/hermes_auth_help.txt
- docs/codex_source/vendor/hermes/_raw/cli_help/hermes_auth_add_help.txt

APPLIES_TO:
- importing credentials from `~/.codex/auth.json`
- saving imported tokens into `~/.hermes/auth.json`
- openai-codex login bootstrap

FACTS:
- Hermes has an import/adopt path that reads the Codex CLI auth file.
- the imported tokens are written into Hermes auth storage.
- the source code contains dedicated helpers for reading Codex CLI tokens, saving Codex tokens, and starting the openai-codex login flow.
- imported tokens still need normal readiness checks; file presence alone is not enough.

CONTRACT:
- the import/adopt path is the documented bridge, not a workaround.
- do not mutate the Codex CLI store as a side effect of unrelated code.

NON_GOALS:
- no direct auth-file editing in docs
- no login execution

FORBIDDEN_MISUSE:
- using old runtime markers or token shape alone as proof of active auth

OPEN_QUESTIONS:
- the import path is clear, but live readiness still depends on provider checks

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- local_source_checked: yes
- cli_help_checked: yes
- verified_at_utc: 2026-05-16T10:33:42Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_HERMES_DOCS_EXTRACTION_20260516_01
