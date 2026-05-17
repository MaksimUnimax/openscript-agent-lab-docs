# Documentation gate rules

STATUS: IMPORTED_FROM_CHATGPT_UPLOAD

Gate rules:
- vendor docs are source-of-truth for vendor behavior
- project docs are source-of-truth for project-specific memory and rules
- roadmap and context are memory, not vendor docs
- rules pack tells Codex how to read docs; it does not replace the docs themselves
- if required docs are missing or stubbed, the future fix-run must stop
- do not replace missing docs with memory-based assumptions
- do not rely on "Codex cannot see files" as a general rule

New access model:
- docs are available in the repo under `docs/codex_source/**`
- assistant must point Codex to exact paths
- Codex should not read all docs by default
- Codex should read only the exact sources required by the task card and prompt
- passing the docs gate is required but not sufficient for a combined edit
- a combined edit also requires exact affected modules, allowed scope match, and the combined-run guard

DOCS_TO_READ rule:
- if a prompt does not list exact docs to read, Codex must stop or request clarification
- `DOCS_TO_READ` must name the repo files and explain why each is needed

STOP conditions:
- required docs are missing, stub, contradictory, or not listed in `DOCS_TO_READ`
- project docs contradict runtime facts and the prompt does not define which source wins
- guessing from memory, code or previous reports is forbidden
- if the docs gate fails, STOP before editing
- if the combined-run guard fails, STOP before editing
- task-card stale readiness is not a docs gate failure
- task cards are planning/context docs, not the primary permission gate
