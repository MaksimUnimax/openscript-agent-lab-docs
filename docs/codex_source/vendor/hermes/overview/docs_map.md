# Hermes docs map

STATUS: extracted
CATEGORY: vendor/hermes/overview

SOURCE_URLS:
- https://hermes-agent.nousresearch.com/docs/
- https://hermes-agent.nousresearch.com/docs/llms.txt
- https://hermes-agent.nousresearch.com/docs/llms-full.txt

SOURCE_PATHS:
- docs/codex_source/vendor/hermes/_raw/docs_root.html
- docs/codex_source/vendor/hermes/_raw/llms.txt
- docs/codex_source/vendor/hermes/_raw/llms-full.txt
- docs/codex_source/vendor/hermes/_raw/fetch_report.md

LOCAL_SOURCE_PATHS:
- /opt/openscript-agent-lab/vendor/hermes-agent/hermes_cli/main.py
- /opt/openscript-agent-lab/vendor/hermes-agent/hermes_cli/auth.py
- /opt/openscript-agent-lab/vendor/hermes-agent/hermes_cli/profiles.py

CLI_HELP:
- docs/codex_source/vendor/hermes/_raw/cli_help/hermes_help.txt

APPLIES_TO:
- future Codex prompt selection
- repo docs discovery

FACTS:
- Hermes docs are split into vendor, project, task cards, templates, and raw sources.
- exact file paths are the prompt contract, not memory or roadmap prose.
- vendor docs and project docs are separate source-of-truth layers.

CONTRACT:
- read task-card required docs first.
- if a required doc is stub, future fix-runs must stop with `STOP_DOCS_MISSING`.

NON_GOALS:
- no application behavior change
- no route logic

FORBIDDEN_MISUSE:
- using roadmap, continuity, or TZ as a substitute for vendor docs
- using this map as a runtime settings file

OPEN_QUESTIONS:
- none for the docs map itself

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- local_source_checked: yes
- cli_help_checked: yes
- verified_at_utc: 2026-05-16T10:33:42Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_HERMES_DOCS_EXTRACTION_20260516_01
