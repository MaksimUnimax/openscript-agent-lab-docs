# Hermes token invalidated

STATUS: extracted_with_gaps
CATEGORY: vendor/hermes/auth

SOURCE_URLS:
- https://hermes-agent.nousresearch.com/docs/integrations/providers
- https://hermes-agent.nousresearch.com/docs/user-guide/features/codex-app-server-runtime

SOURCE_PATHS:
- docs/codex_source/vendor/hermes/_raw/providers.html
- docs/codex_source/vendor/hermes/_raw/llms-full.txt

LOCAL_SOURCE_PATHS:
- /opt/openscript-agent-lab/vendor/hermes-agent/hermes_cli/auth.py
- /opt/openscript-agent-lab/vendor/hermes-agent/agent/credential_pool.py

CLI_HELP:
- docs/codex_source/vendor/hermes/_raw/cli_help/hermes_auth_status_help.txt

APPLIES_TO:
- provider readiness checks
- stale-token rejection

FACTS:
- a token file can exist while the underlying provider is not ready.
- imported or cached credentials still need normal validity and freshness checks.
- stale token state must not be treated as a live session.

CONTRACT:
- `token_invalidated` style failures mean "not ready", not "auth file missing".
- future fix-runs must treat file metadata as insufficient without a live check.

NON_GOALS:
- no live retry logic
- no provider-specific refresh implementation

FORBIDDEN_MISUSE:
- false positives based on file presence, token shape, or old runtime markers

OPEN_QUESTIONS:
- exact user-facing wording for every provider family is outside this doc

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- local_source_checked: yes
- cli_help_checked: yes
- verified_at_utc: 2026-05-16T10:33:42Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_HERMES_DOCS_EXTRACTION_20260516_01
