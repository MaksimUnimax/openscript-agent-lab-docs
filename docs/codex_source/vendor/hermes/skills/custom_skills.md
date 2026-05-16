# Hermes custom skills

STATUS: extracted
CATEGORY: vendor/hermes/skills

SOURCE_URLS:
- https://hermes-agent.nousresearch.com/docs/guides/work-with-skills

SOURCE_PATHS:
- docs/codex_source/vendor/hermes/_raw/skills.html
- docs/codex_source/vendor/hermes/_raw/llms-full.txt

LOCAL_SOURCE_PATHS:
- /opt/openscript-agent-lab/vendor/hermes-agent/agent/skill_utils.py
- /opt/openscript-agent-lab/vendor/hermes-agent/hermes_cli/profiles.py

CLI_HELP:
- docs/codex_source/vendor/hermes/_raw/cli_help/hermes_tools_help.txt

APPLIES_TO:
- user skills
- plugin skills

FACTS:
- custom skills live in the same skills directory structure as bundled and agent-managed skills.
- plugin skills can be loaded explicitly and are not always shown in the default skills list.

CONTRACT:
- custom skill docs belong in the skills layer, not in memory or runtime docs.

NON_GOALS:
- no plugin marketplace guide

FORBIDDEN_MISUSE:
- mixing custom skills with provider auth or gateway runtime state

OPEN_QUESTIONS:
- exact plugin registration behavior depends on the plugin type

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- local_source_checked: yes
- cli_help_checked: yes
- verified_at_utc: 2026-05-16T10:33:42Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_HERMES_DOCS_EXTRACTION_20260516_01
