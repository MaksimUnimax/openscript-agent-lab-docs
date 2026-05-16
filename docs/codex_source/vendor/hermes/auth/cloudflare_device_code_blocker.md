# Cloudflare device-code blocker

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
- /opt/openscript-agent-lab/vendor/hermes-agent/agent/credential_sources.py

CLI_HELP:
- docs/codex_source/vendor/hermes/_raw/cli_help/hermes_auth_help.txt

APPLIES_TO:
- device-code login failure handling
- openai-codex auth bootstrap

FACTS:
- project runtime evidence recorded an HTTP 403 Cloudflare challenge against the OpenAI device-auth endpoint.
- this is an environment-specific blocker, not a normal success path.
- blind automatic retries are not a valid recovery contract.

CONTRACT:
- do not retry the same device-code start blindly as if it were a harmless UI recovery.
- mark the event as project runtime evidence, not as Hermes vendor docs.

NON_GOALS:
- no change to auth provider internals
- no credential mutation

FORBIDDEN_MISUSE:
- presenting the blocker as an official Hermes-only semantic without evidence

OPEN_QUESTIONS:
- whether the exact endpoint behavior is transient or policy-driven is outside this extraction

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- local_source_checked: yes
- cli_help_checked: no
- verified_at_utc: 2026-05-16T10:33:42Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_HERMES_DOCS_EXTRACTION_20260516_01
