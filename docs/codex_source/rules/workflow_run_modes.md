TITLE: Workflow Run Modes — Risk-Based Combined Runs
STATUS: IMPORTED_CURRENT_RULE
SOURCE_KIND: chatgpt_inline_user_clarification
VERSION: risk_based_combined_runs_v1
DATE: 2026-05-17

# Workflow update — risk-based combined runs

## 1. Why this update exists

The older workflow required a separate design/impact run before almost every fix-run.

That rule was useful when models were weaker and the user wanted both ChatGPT and Codex to separately inspect implementation plans before code changes.

Current observation:
- Most Codex design proposals are accepted without major changes.
- Requiring a separate design-run by default creates unnecessary prompts, extra runs, delays and circular work.
- The project still needs safety, but the workflow should be risk-based rather than mandatory-design-by-default.

This update changes the default implementation workflow.

## 2. New default rule

Separate design approval is no longer mandatory by default.

For narrow ordinary fixes, the default run mode is:

proof -> design summary -> minimal fix -> tests/checks -> git push -> report

This is called:

`combined_proof_design_fix`

In this mode Codex may proceed from proof/design summary to a minimal fix in the same run, but only if all safety conditions pass.

## 3. Combined run allowed conditions

Codex may proceed to edit in the same run only if:

- all required `DOCS_TO_READ` are provided and read;
- documentation gate passes;
- exact affected modules/files are found;
- affected scope matches `ALLOWED_SCOPE`;
- the fix is narrow and local;
- no broad refactor is needed;
- no new architecture decision is required;
- no secrets/auth files/runtime secret paths are read or touched;
- no dangerous runtime/system/deploy mutation is needed;
- no external paid-resource behavior is changed without explicit permission;
- tests/checks are available and can be run;
- working tree guard confirms unrelated dirty files will not be staged;
- Codex can explain the design summary before edits;
- Codex can report proof, design summary, files changed, tests and git push status.

If any condition fails, Codex must STOP before editing.

## 4. Separate design approval remains mandatory for high-risk tasks

Separate design/proof approval is still mandatory for:

- auth;
- secrets;
- provider configuration;
- credential handling;
- Telegram delivery/send path;
- Telegram bot token handling;
- systemd/nginx/deploy;
- runtime storage migrations;
- database schema or migration;
- paid-resource paths;
- large UI refactors;
- new architecture blocks;
- Agent Farm / Task Runtime;
- external APIs such as YouTube/Twitch;
- tasks touching more than 2-3 modules;
- tasks where docs and code appear to contradict each other;
- tasks where affected module ownership is unclear;
- tasks where implementation may expose public/private docs or source boundaries;
- tasks involving runtime destructive changes;
- tasks where manual user approval is required by task card or rules.

For these high-risk tasks the workflow remains:

proof/design -> user/ChatGPT acceptance -> minimal fix -> repeat proof

## 5. Docs-only tasks remain docs-only

Docs/import/update tasks remain docs-only and must not use combined fix mode.

Examples:
- context import/update;
- roadmap update;
- ТЗ update;
- module map update;
- task-card re-evaluation;
- vendor/project docs extraction;
- rules update.

These runs may update docs and push public docs, but must not change application code.

## 6. Task-card readiness and combined runs

Task-card re-evaluation can promote a task to:
- ready_for_proof_run;
- ready_for_design_run;
- ready_for_combined_proof_design_fix;
- ready_for_fix_run.

Task-card readiness fields are advisory metadata, not a hard permission gate.

For narrow implementation tasks:
- ready_for_combined_proof_design_fix: true is a useful hint;
- ready_for_fix_run: false does not block a guarded combined run by itself if docs gate and combined-run guard pass;
- stale readiness flags should be reported and, when appropriate, updated, but not used as automatic STOP conditions.

This lets the next run combine proof/design/fix with STOP-before-edit safeguards.

## 6.1. Task cards are not blocking gates

Task cards are:
- task summaries;
- acceptance checklists;
- planning notes;
- optional context;
- useful documentation.

Task cards are not:
- the final permission system for code changes;
- a reason to stop if docs gate and combined-run guard pass;
- a reason to require a separate run only to flip readiness flags.

Main implementation permission comes from:
- required docs are read;
- documentation gate passes;
- exact affected modules are found;
- scope matches `ALLOWED_SCOPE`;
- `COMBINED_RUN_GUARD` passes;
- high-risk conditions are absent;
- tests/checks are available.

If a task card has stale fields such as `ready_for_fix_run: false`, but current docs and combined-run guard allow proceeding:
- Codex may proceed;
- Codex must report that the task card was stale;
- Codex may update the task card in docs as part of the same run if docs update is in scope;
- Codex must not stop only because of an old readiness flag.

If a task card contains a real contradiction with current source-of-truth docs:
- current imported docs/rules/TЗ/roadmap/module map win unless prompt says otherwise;
- Codex must report the contradiction;
- if contradiction affects safety or scope, STOP before editing;
- if contradiction is only stale readiness metadata, update/report it and continue if guard passes.

For high-risk tasks, task cards may still require separate design approval, but that is because the task is high-risk, not because the task card is a universal blocker.

## 7. Required prompt field

Every implementation prompt must include:

RUN_MODE:
- docs_only
or
- proof_only
or
- design_only
or
- combined_proof_design_fix
or
- fix_after_approved_design
or
- repeat_proof

For combined mode, prompt must include:

COMBINED_RUN_GUARD:
- docs gate must pass
- exact affected modules must be found
- scope must match allowed scope
- no high-risk category
- if high-risk or unclear: STOP before editing
- design summary must be reported before describing fix
- tests/checks required
- commit/push required after edits

## 8. Report requirements for combined runs

Combined run reports must include:

COMBINED_RUN:
- run_mode:
- docs_gate_passed:
- exact_code_path_found:
- affected_modules:
- high_risk_detected:
- scope_matched_allowed_scope:
- proceeded_to_edit:
- stop_before_edit_reason:
- design_summary:
- fix_summary:
- tests_run:
- manual_test_needed:
- git_push_status:

TASK_CARD_STATUS:
- task_card_read:
- task_card_stale:
- task_card_blocked_run:
- task_card_updated:

If Codex edits without satisfying combined-run guard, the run is invalid.

## 9. Practical effect for current allowlist work

For Telegram user_id allowlist:
- after docs unblock and task-card readiness, do not automatically require separate design-only run.
- Preferred next implementation run can be:
  task-card-ready -> combined proof/design/fix
- Codex must first locate exact code path and confirm scope.
- If exact affected modules are found and scope is narrow, it may implement minimal universal allowlist fix in the same run.
- If implementation touches high-risk send/auth/provider/secrets/runtime or unclear broad modules, STOP before editing.

## 10. Priority

This workflow update supersedes older blanket rules that required separate design approval before every fix.

It does not supersede:
- documentation gate;
- no guessing;
- exact `DOCS_TO_READ`;
- no secrets;
- source/runtime boundaries;
- git push requirements;
- public docs safety requirements;
- STOP on missing/stub/contradictory docs;
- high-risk separate design approval.
