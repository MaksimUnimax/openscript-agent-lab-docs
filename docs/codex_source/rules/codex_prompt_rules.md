# Codex prompt rules

STATUS: IMPORTED_FROM_CHATGPT_UPLOAD

Prompt contract:
- every prompt must name the exact docs Codex should read
- every prompt must name the exact directories if several files are involved
- every prompt must include the active task card when a task card exists
- every prompt must include the minimal source set, not "read everything"
- for append-only files, Codex reads manifest + tail only
- `DOCS_TO_READ` is mandatory for OpenScript Agent Lab technical tasks
- each `DOCS_TO_READ` entry must include path, why, and required yes/no

Stop rules:
- if a required doc is `stub`, `needs_import`, or missing, stop with `STOP_DOCS_MISSING`
- if the prompt does not provide exact paths, ask for clarification instead of guessing
- if a task requires vendor docs, do not substitute project docs
- if a task requires project docs, do not substitute roadmap/context history
- do not infer missing task facts from memory alone
- if docs contradict each other and the prompt does not name the winning source, stop
- if the active task card says `ready_for_fix_run: false`, do not force a fix run

Repository docs rule:
- the docs are available under `docs/codex_source/**`
- Codex does not need to be given the entire repo tree
- Codex should be given only the files relevant to the task

Baseline modes:
- Mode A: assistant-provided baseline plus exact docs
- Mode B: exact repo-docs baseline extracted from listed files
- high-risk tasks should prefer one of these two modes
