# Hermes memory overview

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
- cross-session recall
- memory providers
- prompt context assembly

FACTS:
- Hermes has a memory layer distinct from auth and provider state.
- memory is part of the agent's long-lived state and can influence future prompts.

CONTRACT:
- memory is not a substitute for vendor docs or runtime baselines.

NON_GOALS:
- no memory provider implementation

FORBIDDEN_MISUSE:
- relying on memory to prove current runtime readiness

OPEN_QUESTIONS:
- exact provider plugins and storage details belong to deeper docs

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- local_source_checked: yes
- cli_help_checked: no
- verified_at_utc: 2026-05-16T10:33:42Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_HERMES_DOCS_EXTRACTION_20260516_01
