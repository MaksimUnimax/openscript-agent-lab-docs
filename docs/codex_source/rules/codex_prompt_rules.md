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
- `RUN_MODE` is mandatory for every technical prompt
- allowed `RUN_MODE` values are `docs_only`, `proof_only`, `design_only`, `combined_proof_design_fix`, `fix_after_approved_design`, and `repeat_proof`
- when `RUN_MODE: combined_proof_design_fix`, the prompt must include `COMBINED_RUN_GUARD`
- combined runs must include a `COMBINED_RUN` report block

Stop rules:
- if a required doc is `stub`, `needs_import`, or missing, stop with `STOP_DOCS_MISSING`
- if the prompt does not provide exact paths, ask for clarification instead of guessing
- if a task requires vendor docs, do not substitute project docs
- if a task requires project docs, do not substitute roadmap/context history
- do not infer missing task facts from memory alone
- if docs contradict each other and the prompt does not name the winning source, stop
- if `RUN_MODE: combined_proof_design_fix` is requested without `COMBINED_RUN_GUARD`, stop
- if a combined run cannot satisfy the guard, stop before editing
- task-card readiness metadata alone does not block a guarded combined run
- if a task card has stale readiness metadata, report it instead of stopping automatically
- if a task card contains a real safety contradiction with source-of-truth docs, stop

Repository docs rule:
- the docs are available under `docs/codex_source/**`
- Codex does not need to be given the entire repo tree
- Codex should be given only the files relevant to the task

Baseline modes:
- Mode A: assistant-provided baseline plus exact docs
- Mode B: exact repo-docs baseline extracted from listed files
- high-risk tasks should prefer one of these two modes

Prompt template rule:
Every technical prompt should include:

- ТЗ проверено.
- `DOCS_TO_READ`.
- `RUN_MODE`.
- `DOCUMENTATION_GATE`.
- `DOCUMENTATION_BASELINE` or instruction to extract exact baseline from listed docs.
- `RUNTIME_BASELINE`.
- `UNIVERSALITY_CHECK`.
- `ALLOWED_SCOPE`.
- `FORBIDDEN_SCOPE`.
- `CHECKS`.
- `ACCEPTANCE`.
- `REPORT`.
- If `RUN_MODE: combined_proof_design_fix`, also include `COMBINED_RUN_GUARD`.
- If combined mode is used, `REPORT` must include `COMBINED_RUN`.
- If combined mode is used, `REPORT` must also include `TASK_CARD_STATUS`.
- `TASK_CARD_STATUS` must expose `task_card_read`, `task_card_stale`, `task_card_blocked_run`, and `task_card_updated`.
