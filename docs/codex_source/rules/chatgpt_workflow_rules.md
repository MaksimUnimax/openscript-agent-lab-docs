# ChatGPT workflow rules

STATUS: IMPORTED_FROM_CHATGPT_UPLOAD

ChatGPT workflow:
1. Read `docs/codex_source/ENTRYPOINT_FOR_CHATGPT.md` first.
2. Read `docs/codex_source/index.yaml`.
3. Read `docs/codex_source/project/current_status.md`.
4. Read `docs/codex_source/project/project_snapshot.md` when a task needs repo layout context.
5. Read the relevant manifests before reading any append-only tail.
 6. Read the active task card when it exists, but treat it as context/checklist rather than a hard permission gate.
 7. For repo-documentation tasks, include `DOCS_TO_READ` with exact paths before asking Codex to act.
 8. For narrow ordinary fixes, prefer `combined_proof_design_fix` only when `docs/codex_source/rules/workflow_run_modes.md` allows it and the combined-run guard is satisfied.
 9. Do not create a separate run only to flip stale task-card readiness if docs gate and combined guard already allow the change.

Rules:
- do not rely on memory before reading the entrypoint
- do not confuse vendor docs with project memory
- do not ask Codex to "figure it out"
- do not omit exact paths when assigning a task to Codex
- do not use a rule pack as a substitute for vendor or project docs
- do not treat roadmap/context as vendor docs
- do not say "read everything" when a smaller exact source set is sufficient
- do not rely on inline-only wording now that repo docs exist
- separate design approval is no longer mandatory by default for narrow ordinary fixes
- separate design approval remains mandatory for high-risk or unclear-scope tasks
- docs-only tasks remain docs-only
- keep proof-first and no-guessing
- keep user/manual approval where the task card requires it
- task cards are advisory context, not the universal permission gate
- stale task-card readiness should not force an extra readiness-flip run
- stop if the needed docs are missing, stubbed, contradictory, or not named
