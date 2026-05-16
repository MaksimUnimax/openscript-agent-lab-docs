# Hermes bundled skills

STATUS: verified
CATEGORY: vendor/hermes/skills

SOURCE_URLS:
- https://hermes-agent.nousresearch.com/docs/guides/work-with-skills

SOURCE_PATHS:
- docs/codex_source/vendor/hermes/_raw/skills.html
- docs/codex_source/vendor/hermes/_raw/llms-full.txt

LOCAL_SOURCE_PATHS:
- /opt/openscript-agent-lab/vendor/hermes-agent/toolsets.py
- /opt/openscript-agent-lab/vendor/hermes-agent/agent/skill_utils.py

CLI_HELP:
- docs/codex_source/vendor/hermes/_raw/cli_help/hermes_tools_help.txt

APPLIES_TO:
- repo-bundled skill distribution
- bundled manifest sync

FACTS:
- bundled skills ship with Hermes and are copied into `~/.hermes/skills/`.
- the bundled manifest tracks origin hashes for sync decisions.
- bundled skills are distinct from user-created skills and hub-installed skills.

CONTRACT:
- bundled skills are not user data and are not the same as memory.

NON_GOALS:
- no installation workflow

FORBIDDEN_MISUSE:
- editing bundled skills without understanding sync behavior

OPEN_QUESTIONS:
- exact bundled-manifest edge cases belong in deeper docs

VERIFICATION:
- raw_source_saved: yes
- official_docs_checked: yes
- local_source_checked: yes
- cli_help_checked: yes
- verified_at_utc: 2026-05-16T10:33:42Z
- extraction_run_id: OPENSCRIPT_AGENT_LAB_CODEX_SOURCE_HERMES_DOCS_EXTRACTION_20260516_01
