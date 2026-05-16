# Hermes Codex skill

STATUS: verified
CATEGORY: vendor/hermes/skills

SOURCE_URLS:
- https://hermes-agent.nousresearch.com/docs/user-guide/skills/bundled/autonomous-ai-agents/autonomous-ai-agents-codex
- https://hermes-agent.nousresearch.com/docs/user-guide/features/codex-app-server-runtime

SOURCE_PATHS:
- docs/codex_source/vendor/hermes/_raw/codex_skill.html
- docs/codex_source/vendor/hermes/_raw/codex_app_server_runtime.html
- docs/codex_source/vendor/hermes/_raw/llms-full.txt

LOCAL_SOURCE_PATHS:
- /opt/openscript-agent-lab/vendor/hermes-agent/agent/skill_utils.py
- /opt/openscript-agent-lab/vendor/hermes-agent/toolsets.py

CLI_HELP:
- docs/codex_source/vendor/hermes/_raw/cli_help/hermes_tools_help.txt

APPLIES_TO:
- bundled `codex` skill
- coding delegation guidance

FACTS:
- the bundled Codex skill is a Hermes skill, not the provider named `openai-codex`.
- the skill guides autonomous coding behavior and is separate from Codex app-server runtime selection.
- skill loading happens through Hermes skill mechanics.

CONTRACT:
- future tasks must not confuse the Codex skill with provider auth or runtime transport.

NON_GOALS:
- no skill authoring details

FORBIDDEN_MISUSE:
- using the skill name as evidence of provider login state

OPEN_QUESTIONS:
- none

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- local_source_checked: yes
- cli_help_checked: yes
- verified_at_utc: 2026-05-16T10:33:42Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_HERMES_DOCS_EXTRACTION_20260516_01
