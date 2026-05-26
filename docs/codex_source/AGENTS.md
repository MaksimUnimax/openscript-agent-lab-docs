# AGENTS.md — OpenScript Agent Lab Codex Contract

This file is the standing repository contract for Codex runs in OpenScript Agent Lab.

Direct task instructions have priority over this file. If a task prompt conflicts with this file, follow the task prompt and report the conflict.

This file contains reusable execution rules. Task-specific prompts should still provide the concrete task, exact task-specific docs, allowed files, acceptance criteria, and report focus.

## 1. Repository entrypoint

For every non-trivial run, start from the repository root.

Default repository path:

/opt/openscript-agent-lab

Before changing anything, read the project documentation entrypoint:

docs/codex_source/ENTRYPOINT_FOR_CHATGPT.md

Then read only the project docs needed by that run, using the entrypoint and the task prompt.

Do not invent project behavior when docs/source do not prove it.

If required docs are missing, stub, unreadable, or contradicted by source/runtime proof, report it and STOP unless the task explicitly allows continuing.

## 2. Task-specific docs

The task prompt must specify exact docs when a run depends on a specific subsystem.

Use those exact paths.

Do not replace exact task docs with generic assumptions.

If the task depends on a vendor, integration, runtime, tool, API, or protocol, read the local project/vendor docs specified by the prompt before reasoning about that subsystem.

If task-specific docs do not prove the required behavior, report UNKNOWN/STOP instead of guessing.

## 3. Standard run order

Use this order unless the prompt explicitly says otherwise:

1. Documentation gate
2. Preflight
3. Read-only proof of current state
4. Root cause
5. Design / impact
6. Minimal source change, only if safe
7. Targeted tests
8. Relevant regression checks
9. Service restart / healthz only when needed
10. Git commit + push for source changes
11. Final report

One run = one task.

Do not mix unrelated work.

Do not make broad refactors unless the task explicitly asks for them.

## 4. Preflight

Use this standard preflight unless the task prompt provides a different one:

git rev-parse HEAD
git status -sb
git status --short
git fetch origin main
git rev-parse origin/main
git diff --stat
git diff --cached --stat

Expected default state:

- HEAD matches origin/main unless documented otherwise
- staged area is empty
- worktree is clean, or dirty files are fully classified before touching anything

STOP on unexplained dirty state outside allowed scope.

Never stage or overwrite unrelated dirty files.

## 5. Source vs runtime

Git-tracked source is the source of truth for code, docs, tests, and agent packages.

Do not make runtime-only fixes.

Do not edit runtime profiles as a shortcut.

Do not commit runtime data.

Allowed agent source package paths include:

- agent-packages/*/manifest.json
- agent-packages/*/SOUL.md
- agent-packages/*/rules.md
- agent-packages/*/examples.md
- agent-packages/*/provider.defaults.json
- agent-packages/*/tools.json
- agent-packages/*/skills/*.md
- agent-packages/*/skills/.gitkeep only if intentional

Never commit:

- secrets
- tokens
- logs
- sessions
- runtime profiles
- memories
- generated caches
- backups
- temp files
- editor swap files
- production data

If a file classification is ambiguous, STOP and report.

## 6. Safety boundaries

Do not perform these actions unless the task prompt explicitly allows them:

- Telegram API calls
- provider/model calls
- real tool execution
- real STT/TTS/voice execution
- production expense creation
- auth/login/provider changes
- token/secret reads or prints
- runtime profile mutation
- browser/live screenshot proof
- public network calls outside the required local service checks

Read-only inspection is allowed when safe and when it does not expose secrets.

Never print secrets, tokens, private credentials, or raw sensitive payloads.

## 7. UI tasks

For UI tasks, do source/local/API/test proof.

Do not require Playwright, Chromium, browser screenshots, or external visual proof unless the task prompt explicitly asks.

If the user says they will manually verify UI, do not add browser proof as acceptance.

Keep primary UI user-facing:

- no diagnostic wall in the main view
- no raw runtime/debug state as primary content
- technical diagnostics belong in collapsed or secondary sections
- preserve unrelated tabs and controls

## 8. Tool and integration semantics

Do not treat all tools or integrations as one type.

A service may have:

- agent executable tools
- service integrations or channels
- voice capabilities
- registered but unavailable placeholders
- diagnostic-only entries

A user-facing tools surface should show what the service can actually use now.

Do not show disabled, future-only, proof-required, blocked, or placeholder items as available tools.

Do not hide a working service integration only because it is not an agent-executable tool.

Use the task prompt and source-of-truth state to decide exact behavior.

## 9. Context/session work

For context or memory tasks, first prove the actual handoff path.

Map:

input source
-> selected agent
-> stable context/session identity
-> reply/model/Hermes boundary
-> structured state
-> action/result state

Do not solve a universal context problem with a hardcoded local parser patch.

Do not rely on model memory as the source of truth for structured state.

Expense flows, voice flows, and agent-specific examples are test cases, not the whole architecture.

## 10. Checks

Run targeted tests first.

Then run the smallest relevant regression suite.

Do not run unrelated expensive checks unless the risk justifies them.

For Python/source changes, normally run:

python -m compileall agent_lab tests

For JavaScript/static UI changes, normally run:

node --check agent_lab/static/app.js

For service changes, restart only after tests pass and then check healthz:

systemctl restart openscript-agent-lab-ui.service
systemctl is-active openscript-agent-lab-ui.service
curl -sS -o /tmp/agent_lab_healthz.out -w '%{http_code}\n' http://127.0.0.1:18765/healthz

If a test module named in a task does not exist, report it and run the nearest relevant existing tests.

## 11. Git discipline

For any source change:

1. Run git diff --check
2. Run git diff --stat
3. Stage only allowed files
4. Run git diff --cached --name-only
5. Run git diff --cached --stat
6. STOP if staged files include forbidden or unrelated scope
7. Commit with a clear message
8. Push to origin main
9. Prove HEAD == origin/main
10. End with clean git status

No source change is complete without commit and push unless the task explicitly says no commit.

For proof-only runs:

- do not commit
- do not push
- final git status must be clean

## 12. Minimal change policy

Change only files required by the task.

Do not do opportunistic cleanup.

Do not rewrite unrelated modules.

Do not change behavior outside the stated scope.

Do not hide bad source-of-truth state in UI.

Do not copy one agent’s content into another agent without proven source/authorization.

Do not invent missing document, skill, tool, runtime, or vendor behavior.

## 13. Standard report

Every run must end with:

CHATGPT_REPORT_BEGIN
run_id:
run_mode:
docs_read:
docs_missing:
docs_stub:
docs_contradictions:
documentation_gate_passed:
preflight_head:
origin_main_equals_head:
preflight_git_status:
current_state_proof:
root_cause:
classification:
design_or_fix_summary:
files_changed:
tests_run:
service_restart:
healthz_status:
git_private_commit:
git_private_push_status:
final_git_status:
security_block:
forbidden_scope_touched:
stop_or_success:
next_recommended_step:
CHATGPT_REPORT_END

Also include a compact block:

CHATGPT_PASTE_BEGIN
FINAL SUMMARY:
RUN_ID:
STATUS:
ROOT_CAUSE:
FIX:
FILES:
TESTS:
COMMIT:
PUSH:
NEXT:
CHATGPT_PASTE_END

For proof-only runs, use:

git_private_commit: none
git_private_push_status: not_run_no_source_changes

For UI tasks where the user manually verifies the page, use:

browser_rendered_proof: not_required_user_will_verify_ui_manually

## 14. Stop rules

STOP instead of guessing when:

- docs/source do not prove required behavior
- source/runtime truth is contradictory
- scope would require secrets, runtime profiles, production data, or live external calls
- staged files include forbidden scope
- required current state cannot be proven safely
- implementing the task would require a broader design than requested

When stopping, report:

- what was proven
- exact blocker
- files inspected
- what data or decision is needed next
- git status
