# Rules

STATUS: IMPORTED_FROM_CHATGPT_UPLOAD

This directory stores the workflow contract for ChatGPT and Codex.

Current schema:
- documentation is available in-repo under `docs/codex_source/**`
- assistant must specify exact directories and files for each run
- Codex must not read everything by default
- append-only memory files are read via manifest + tail only
- vendor docs, project docs, roadmap, task cards and rules are separate layers

Current mandatory rule file:
- `repo_documentation_access_rules.md`

Current access model:
- repo-based docs access with exact `DOCS_TO_READ` paths
- no blanket inline-only requirement
- no guesswork when docs are missing or stubbed

Important change:
- the old general rule "Codex has no docs and must rely only on inline text" is no longer current
- the current rule is repo-based docs access with exact path targeting

This directory exists to prevent vague prompts and memory-based guessing.
