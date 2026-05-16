# Hermes agent-managed skills

STATUS: extracted
CATEGORY: vendor/hermes/skills

SOURCE_URLS:
- https://hermes-agent.nousresearch.com/docs/guides/work-with-skills

SOURCE_PATHS:
- docs/codex_source/vendor/hermes/_raw/skills.html
- docs/codex_source/vendor/hermes/_raw/llms-full.txt

LOCAL_SOURCE_PATHS:
- /opt/openscript-agent-lab/vendor/hermes-agent/agent/skill_utils.py
- /opt/openscript-agent-lab/vendor/hermes-agent/agent/tools.py

CLI_HELP:
- docs/codex_source/vendor/hermes/_raw/cli_help/hermes_tools_help.txt

APPLIES_TO:
- `skill_manage`
- agent-written procedural memory

FACTS:
- Hermes can create and update skills through the agent loop.
- agent-managed skills are procedural memory, not session history.

CONTRACT:
- use `skill_manage` for reusable procedures after validation.

NON_GOALS:
- no skill lifecycle policy

FORBIDDEN_MISUSE:
- using agent-managed skills as a replacement for docs extraction

OPEN_QUESTIONS:
- agent-managed skill governance can vary by workflow

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- local_source_checked: yes
- cli_help_checked: yes
- verified_at_utc: 2026-05-16T10:33:42Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_HERMES_DOCS_EXTRACTION_20260516_01
