# Hermes skills overview

STATUS: verified
CATEGORY: vendor/hermes/skills

SOURCE_URLS:
- https://hermes-agent.nousresearch.com/docs/guides/work-with-skills
- https://hermes-agent.nousresearch.com/docs/user-guide/skills/bundled/autonomous-ai-agents/autonomous-ai-agents-codex

SOURCE_PATHS:
- docs/codex_source/vendor/hermes/_raw/skills.html
- docs/codex_source/vendor/hermes/_raw/codex_skill.html
- docs/codex_source/vendor/hermes/_raw/llms-full.txt

LOCAL_SOURCE_PATHS:
- /opt/openscript-agent-lab/vendor/hermes-agent/agent/skill_utils.py
- /opt/openscript-agent-lab/vendor/hermes-agent/toolsets.py
- /opt/openscript-agent-lab/vendor/hermes-agent/model_tools.py

CLI_HELP:
- docs/codex_source/vendor/hermes/_raw/cli_help/hermes_tools_help.txt

APPLIES_TO:
- skills_list
- skill_view
- skill_manage

FACTS:
- Hermes skills are first-class documents loaded from the skills library.
- skills are separate from memory: they encode procedures, not session recall.
- skills can be bundled, user-managed, or agent-managed.

CONTRACT:
- future prompt tasks should read skill docs when the task depends on procedural behavior.

NON_GOALS:
- no skill content authoring here

FORBIDDEN_MISUSE:
- using memory docs as a substitute for skills

OPEN_QUESTIONS:
- some bundle-specific skills are documented in sibling docs

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- local_source_checked: yes
- cli_help_checked: yes
- verified_at_utc: 2026-05-16T10:33:42Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_HERMES_DOCS_EXTRACTION_20260516_01
