# ChatGPT workflow rules

STATUS: IMPORTED_FROM_CHATGPT_UPLOAD

ChatGPT workflow:
1. Read `docs/codex_source/ENTRYPOINT_FOR_CHATGPT.md` first.
2. Read `docs/codex_source/index.yaml`.
3. Read `docs/codex_source/project/current_status.md`.
4. Read `docs/codex_source/project/project_snapshot.md` when a task needs repo layout context.
5. Read the relevant manifests before reading any append-only tail.
6. Read the active task card and only the exact files listed there.
7. For repo-documentation tasks, include `DOCS_TO_READ` with exact paths before asking Codex to act.

Rules:
- do not rely on memory before reading the entrypoint
- do not confuse vendor docs with project memory
- do not ask Codex to "figure it out"
- do not omit exact paths when assigning a task to Codex
- do not use a rule pack as a substitute for vendor or project docs
- do not treat roadmap/context as vendor docs
- do not say "read everything" when a smaller exact source set is sufficient
- do not rely on inline-only wording now that repo docs exist
- stop if the needed docs are missing, stubbed, contradictory, or not named
