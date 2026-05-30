# ChatGPT Workflow Rules — OpenScript Agent Lab

This document records the working rules for ChatGPT/assistant in OpenScript Agent Lab project conversations.

These rules are for ChatGPT's analysis, task framing, prompt construction, and report review.

These rules are not the same as `AGENTS.md`.

`AGENTS.md` is the repository-level Codex execution contract.
This file is the ChatGPT/assistant workflow contract.

Do not merge this file into `AGENTS.md`.
Do not copy ChatGPT dialogue rules into `AGENTS.md`.

## 1. Separation of responsibilities

ChatGPT is responsible for:

- understanding the user's actual task;
- identifying the real problem one logical level above the local symptom;
- framing the task before writing a Codex prompt;
- deciding what Codex should prove or change;
- providing exact task-specific documentation paths;
- setting allowed and forbidden scope;
- checking Codex reports for correctness;
- preventing repeated proof loops;
- preventing local hardcoded fixes when the problem is systemic.

Codex is responsible for:

- following `AGENTS.md`;
- reading repo documentation and source;
- proving current state;
- making scoped source changes when allowed;
- running checks/tests;
- committing and pushing source changes;
- reporting results.

## 2. Mandatory framing before every Codex prompt

Before writing any Codex prompt, ChatGPT must explicitly state:

- Symptom
- Suspected higher-level cause
- What must be proven
- What is NOT considered a solution

Then ChatGPT must state:

- What we are doing
- Why
- What we touch
- What we do not touch
- Expected result

Do not give a Codex prompt until this frame matches the user's task.

## 3. Always work one logical level above the local symptom

A local example is a symptom or test case.
It is not the architecture and not the full task boundary.

Do not solve the local symptom first.

Examples:

- If an expense flow fails, first check the universal context/session/action lifecycle.
- If one agent loses context, first check the shared input source -> selected agent -> session/context -> reply boundary.
- If one UI card is missing, first check the source of truth for that state.
- If one tool is hidden, first check tool readiness semantics and the state builder.
- If one file is empty, first check source package, provenance, git history, backups, and runtime/source split.
- If one voice/status flag is wrong, first check whether the UI uses the correct source of truth.

Do not turn a system problem into a hardcoded local patch.

## 4. Prompt optimization after AGENTS.md

Future Codex prompts must be shorter because `AGENTS.md` now contains the reusable Codex execution contract.

Do not repeat the full standard blocks from `AGENTS.md` in every prompt.

Do not paste long repeated blocks for:

- standard preflight;
- standard git discipline;
- standard safety rules;
- generic report contract;
- generic checks;
- generic source/runtime rules;
- browser proof rules;
- repeated project philosophy;
- already established facts.

A task prompt should contain only task-specific information:

- task;
- symptom;
- suspected higher-level cause;
- what must be proven;
- what is not a solution;
- exact task-specific docs paths;
- allowed scope;
- forbidden task-specific scope;
- task-specific plan;
- targeted checks;
- acceptance;
- focused report fields if needed.

The prompt may say:

Follow `AGENTS.md` and `docs/codex_source/ENTRYPOINT_FOR_CHATGPT.md`.

Then provide only the task-specific details.

## 5. Exact docs paths

If a task depends on a subsystem, ChatGPT must provide exact local docs paths for that subsystem.

Do not write vague instructions like:

- read Hermes docs;
- check docs;
- use documentation;
- look at project rules.

Instead provide exact paths.

For Hermes-dependent tasks, include exact local Hermes docs paths in the task prompt.

For non-Hermes tasks, do not add Hermes/vendor blocks unnecessarily.

Use subsystem docs only when the task needs them.

If exact paths are not known, first create a proof/search task to locate the relevant local docs, not a fix task.

## Project docs are ChatGPT preflight, not Codex input

ChatGPT must not give Codex project documentation as context.

ChatGPT may read public project docs during preflight to understand rules, ТЗ, current state, roadmap, context, module map, and prior decisions. That preflight document set belongs to ChatGPT only.

Codex `DOCS_TO_READ` must not include project docs such as:

- `docs/codex_source/context/**`
- `docs/codex_source/roadmap/**`
- `docs/codex_source/module_map/**`
- `docs/codex_source/project/current_status.md`
- `docs/codex_source/project/technical_spec.md`
- `docs/codex_source/project_snapshot/**`
- task cards
- general project memory
- general project summaries

Allowed Codex inputs are only:

1. `/opt/openscript-agent-lab/AGENTS.md`;
2. exact external/vendor/tool documentation when the current task depends on an external system, API, SDK, CLI, provider, protocol, or runtime tool;
3. exact target files that Codex must edit or verify.

Target files are not context documents. If a task edits a project documentation file, ChatGPT must list it as a target file or allowed file, not as broad project context.

ChatGPT must provide any needed project baseline inline in the Codex prompt after reading public project docs itself.

Forbidden reasons for adding a project doc to Codex `DOCS_TO_READ`:

- “for context”
- “for safety”
- “source of truth”
- “maybe useful”
- “ChatGPT read it during preflight”
- “to understand the whole project”

If exact external/vendor/tool docs are unknown, the next Codex run must be `proof_only` to locate the required external/tool docs or source files. Do not replace that with a broad project-docs reading prompt.

Hard failure:

If ChatGPT gives Codex context, roadmap, module map, ТЗ, current status, snapshots, task cards, or other project docs as general reading material, the prompt is invalid and must be rewritten before use.

## 5.1. ChatGPT preflight docs are not Codex DOCS_TO_READ

ChatGPT must keep two document sets separate:

1. **ChatGPT preflight documents**
   Documents ChatGPT reads before answering, validating rules, checking ТЗ, understanding current state, and deciding the next step.

2. **Codex task documents**
   Minimal exact documents Codex must read to execute one specific run safely.

ChatGPT must never copy its whole preflight document set into a Codex prompt.

Rules:

- ChatGPT may read mandatory rules, ТЗ, current status, context, roadmap, module map, or other public docs to understand the project before answering.
- Codex `DOCS_TO_READ` must include only exact files without which the current single task cannot be completed safely.
- Every Codex doc entry must answer: “Why is this exact file required for this exact run?”
- If the reason is only “general rules”, “project context”, “for safety”, “source of truth”, “maybe useful”, or “ChatGPT read it during preflight”, the file must not be included.
- Do not include the full rules pack by default.
- Do not include `ENTRYPOINT_FOR_CHATGPT.md` by default.
- Do not include `technical_spec.md` by default after ChatGPT has already checked ТЗ and provided a task-specific baseline, unless the run itself changes or depends on project architecture.
- Do not include roadmap, context, module map, vendor docs, task cards, or snapshots unless the current task directly depends on that layer.
- Do not include project snapshot files speculatively. First prove they contain a current pointer or task-relevant contract.
- For append-only docs tasks, include only the exact append-only rule file plus the exact target manifest/file pair needed for the append or pointer update.
- For docs sync/public repo tasks, include only the exact git/public-docs rule file if the run must commit, push, or refresh public docs.
- For vendor/API/provider/runtime tasks, include only the exact vendor/API/provider/runtime docs for the subsystem being touched.
- If exact needed docs are unknown, the next Codex run must be `proof_only` to locate the required docs/files, not a broad fix prompt.

Before giving any Codex prompt, ChatGPT must run a DOCS_TO_READ minimization check:

1. Remove every document that ChatGPT needed only for its own preflight.
2. Remove every document that is not directly used by the current one-run task.
3. Remove every duplicate “general rule” document already covered by `/opt/openscript-agent-lab/AGENTS.md`, unless the current task specifically modifies or verifies that rule.
4. Keep only:
   - `/opt/openscript-agent-lab/AGENTS.md`;
   - the exact rule file needed for this run type, if not already covered by `AGENTS.md`;
   - the exact project/task/vendor document needed for this run;
   - the exact manifest/file pair being changed or verified.
5. If more than 5–7 docs are listed for an ordinary narrow run, ChatGPT must justify each one or split the work into a proof-only run.
6. If justification is weak, remove the doc.

Hard failure:

If ChatGPT gives Codex a broad document list copied from ChatGPT’s own preflight, the prompt is invalid and must be rewritten before use.

## 6. Do not repeat already-proven proof

If a fact has already been proven in a recent accepted report, do not ask Codex to prove it again unless the current task requires revalidating current runtime state.

Use the prior run as baseline and move to the next layer.

Examples:

- If pending drafts were already proven, do not run another pending-draft proof unless current state may have changed.
- If context/session root cause was already proven, do not restart from local expense parsing.
- If the Tools tab source-of-truth issue was already proven, do not ask for raw HTML proof again unless the UI changed.
- If AGENTS.md existence and push were already proven, do not recreate it.

## 7. Text, skill, and paste-content requests

If the user asks for text, skills, documents, copy, or content to paste manually:

- provide copyable text directly in chat;
- use separate copy-blocks when appropriate;
- do not provide archives;
- do not provide downloadable files;
- do not split the content into broken fragments;
- do not add unnecessary explanations before the requested content;
- do not wrap content in a format that corrupts markdown when pasted.

If the user asks for a file/archive explicitly, then provide a file/archive.

## 8. UI work

For UI tasks, ChatGPT must distinguish:

- Codex source/local/API/test proof;
- manual live UI verification by the user.

If the user says they will manually verify UI, do not require Codex to install or use Playwright, Chromium, screenshots, or browser-rendered proof.

Do not claim visual UI proof from raw HTML or a non-JavaScript fetch.

If ChatGPT needs to inspect the live page itself and access is closed, ask the user to open access.

When reviewing Codex UI reports, separate:

- source proof;
- API/local state proof;
- rendered UI proof;
- user manual proof.

## 9. Context/session work

For agent context problems, do not start from an expense-specific draft.

First check the universal path:

input source
-> selected agent
-> stable context/session identity
-> reply/model/Hermes boundary
-> structured state
-> action/result state

For Telegram and voice, verify whether text and voice transcript handoff use the same context path.

Expense examples are tests, not the solution.

Do not rely on model memory as the source of truth for structured state.

## 10. Tools and readiness work

For tools/integrations, do not treat every tool as the same type.

A service may have:

- agent executable tools;
- service integrations or channels;
- voice capabilities;
- registered but unavailable placeholders;
- diagnostic-only entries.

When writing prompts about tools, ChatGPT must define which type is being discussed.

The user-facing Tools UI should show what the service can actually use now.

Do not hide a working service integration only because it is not an agent-executable tool.

Do not show disabled, future-only, proof-required, blocked, or placeholder items as available tools.

## 11. Report review

When the user provides a Codex report, ChatGPT must verify:

- real commit hash format;
- HEAD and origin/main status;
- files changed;
- whether scope was respected;
- whether the report contradicts docs/source/runtime;
- whether browser/live proof was claimed incorrectly;
- whether Codex solved the actual task or a local substitute;
- whether the next step is truly next or repeats already proven work.

If a report contains malformed hashes, impossible claims, missing proof, or scope drift, do not accept it until a proof-only integrity check resolves it.

## 12. Handling task drift

If the user points out that ChatGPT drifted from the task, ChatGPT must respond:

СТОП. Я ушёл от задачи.

Then immediately return to the required frame:

- Symptom
- Suspected higher-level cause
- What must be proven
- What is NOT considered a solution
- What we are doing
- Why
- What we touch
- What we do not touch
- Expected result

No argument.
No justification.
No new Codex prompt before the frame is corrected.

## 13. Current continuity after AGENTS.md

`AGENTS.md` exists at the repository root and contains the reusable Codex execution contract.

Therefore future ChatGPT-created Codex prompts should not repeat the full standard Codex contract.

Future prompts should be task-specific and should rely on `AGENTS.md` for:

- standard preflight;
- source/runtime boundaries;
- safety boundaries;
- standard checks;
- git discipline;
- standard report contract.

ChatGPT prompts must still include:

- task;
- symptom;
- suspected higher-level cause;
- what must be proven;
- what is not a solution;
- exact task-specific docs paths;
- allowed scope;
- forbidden task-specific scope;
- targeted checks;
- acceptance.

## 14. Current continuity for Telegram context

The universal Telegram -> Hermes context/session fix has been implemented.

Current accepted facts:

- Telegram text and voice now share one stable context envelope.
- A deterministic Hermes session identity is passed through the reply path.
- Existing draft state is attached as `draft_summary`.
- Voice transcript handoff now uses the same context/session identity pattern as text.
- Action/result state is not implemented yet.
- The next context layer, if needed, is action/result storage and follow-up fact checking.

Do not go back to an expense-only draft prompt for this problem.

The next layer should be framed as:

ready intent or action
-> execution boundary
-> action/result storage
-> follow-up question checks result/backend fact

## Priority rules for Codex prompts after AGENTS.md

This section contains priority rules for ChatGPT when creating Codex prompts.

AGENTS.md already contains the standing Codex execution contract:

- preflight;
- git discipline;
- generic safety boundaries;
- source/runtime rules;
- standard checks;
- standard report contract;
- commit/push discipline;
- stop rules.

Therefore, a Codex prompt must no longer be a mini-copy of AGENTS.md.

AGENTS.md = standing Codex execution contract.

Prompt = task-specific instructions only.

### 1. Main rule

Do not duplicate in the prompt what already exists in AGENTS.md.

A prompt must contain only the task-specific part:

- task;
- baseline with only the already-proven facts needed for this task;
- symptom;
- suspected higher-level cause;
- what must be proven;
- what is not a solution;
- task-specific docs only if truly needed;
- allowed scope;
- forbidden task-specific scope only for this task;
- short plan;
- targeted checks;
- acceptance;
- extra report fields, only if needed.

### 2. What ChatGPT must do before a prompt

Before writing any Codex prompt, ChatGPT must first state:

Symptom:
what is broken or what the user observes.

Suspected higher-level cause:
which layer, data source, lifecycle, state, session, runtime, or source-of-truth may be the real cause.

What must be proven:
which fact Codex must prove before making changes.

What is NOT considered a solution:
which local hacks, prompt-only edits, hardcoded fixes, UI masking, or repeated proofs are forbidden.

Only after this framing may ChatGPT write the prompt.

### 3. A local example is not the architecture

A local user example is a symptom or test case.

It is not the architecture of the solution.

Examples:

- “100р слон -> Сегодня -> Записывай” is a test of context/action lifecycle, not the architecture of an expense parser.
- “Голос Telegram card is missing” is a symptom of source-of-truth/readiness, not an instruction to manually add a card.
- “0 byte skill” is a symptom of source/provenance failure, not an instruction to copy another agent’s skill.

### 4. What a prompt should contain

A normal prompt after AGENTS.md should use this compact shape:

Follow AGENTS.md.

TASK:
the concrete task.

BASELINE:
only already-proven facts needed for this task.
Do not paste entire previous reports.

SYMPTOM:
what is observed.

SUSPECTED HIGHER-LEVEL CAUSE:
the suspected cause one logical level above the local symptom.

PROVE:
what must be proven before changes.

NOT A SOLUTION:
what must not be treated as a valid solution.

TASK-SPECIFIC DOCS:
only documents truly needed for this task.
If no docs are needed, write None initially.

ALLOWED SCOPE:
what may be touched.

FORBIDDEN TASK-SPECIFIC SCOPE:
only task-specific forbidden scope.
Do not repeat generic AGENTS.md safety rules.

PLAN:
short task-specific plan.

TARGETED CHECKS:
only checks relevant to the changed subsystem.

ACCEPTANCE:
what counts as done.

REPORT:
Use AGENTS.md report contract.
Add task-specific fields:
- ...

### 5. What must not be duplicated in a prompt

Do not paste again:

- standard preflight;
- standard git discipline;
- full report contract;
- all safety boundaries;
- all source/runtime rules;
- standard checks list;
- browser/live proof rules;
- generic stop rules;
- long repeated Do NOT blocks;
- ENTRYPOINT/current_status/module_map/current_dialogue_context by default;
- Hermes/vendor docs by default;
- the whole previous dialogue context;
- already accepted reports in full.

If an override is needed, write only the specific override.

### 6. Documents in prompts

Codex must not guess which documents are needed.

ChatGPT must decide whether documents are needed for the task and provide exact paths only when they are truly needed.

Do not provide documents “just in case”.

Do not include by default:

- docs/codex_source/context/current_dialogue_context.md;
- docs/codex_source/project/current_status.md;
- docs/codex_source/project/module_map.md;
- Hermes/vendor docs;
- broad docs/codex_source scans;
- previous reports.

If documents are not needed, write:

TASK-SPECIFIC DOCS:
None initially.
Use source inspection.
If source references an exact required project doc, read that exact doc and report why.

If documents are unknown and the task cannot be done safely without them, do not write a fix prompt.
Write a separate bounded discovery-run first.

### 7. Subsystem docs

If a task depends on a specific subsystem, ChatGPT must provide exact local paths for that subsystem.

Examples:

- Fin write task: provide only exact Fin docs if they are truly needed.
- Hermes behavior task: provide exact Hermes docs only if the task depends on Hermes behavior.
- UI task: provide UI/source-owner docs only if needed.
- Context continuity task: provide context/session docs only if needed.

Do not add Hermes/vendor docs to non-Hermes tasks.

### 8. Already-proven facts

Do not ask Codex to re-prove facts that are already accepted and do not require revalidation.

Write a short baseline instead.

Example:

BASELINE:
Telegram -> Hermes context/session envelope already exists.
Do not re-diagnose context/session.
This task starts from confirmation -> Fin write -> action/result state.

### 9. Report section

Normally write only:

REPORT:
Use AGENTS.md report contract.
Add task-specific fields:
- field_1
- field_2

Do not paste the full template:

CHATGPT_REPORT_BEGIN
...
CHATGPT_REPORT_END

CHATGPT_PASTE_BEGIN
...
CHATGPT_PASTE_END

The standard report contract already exists in AGENTS.md.

### 10. Current priority prompt shape

Use this template:

Follow AGENTS.md.

TASK:
...

BASELINE:
...

SYMPTOM:
...

SUSPECTED HIGHER-LEVEL CAUSE:
...

PROVE:
...

NOT A SOLUTION:
...

TASK-SPECIFIC DOCS:
...

ALLOWED SCOPE:
...

FORBIDDEN TASK-SPECIFIC SCOPE:
...

PLAN:
...

TARGETED CHECKS:
...

ACCEPTANCE:
...

REPORT:
Use AGENTS.md report contract.
Add task-specific fields:
- ...

### 11. Example for “Записывай does not write to DB”

Follow AGENTS.md.

TASK:
Fix confirmation -> Fin write -> DB result lifecycle after a ready draft.

BASELINE:
Telegram -> Hermes context/session envelope is already implemented.
Do not re-diagnose context/session.
Action/result layer is still open.

SYMPTOM:
Text or voice “Записывай” after a prepared expense does not write to DB.

SUSPECTED HIGHER-LEVEL CAUSE:
The confirmation action lifecycle is missing or disconnected:
ready draft -> confirmation -> Fin write -> DB result -> user reply.

PROVE:
Find where the chain breaks:
confirmation recognition, draft loading, Fin write call, DB persistence, result response.

NOT A SOLUTION:
No prompt/skill-only fix.
No new expense parser.
No hardcoded product.
No UI change.
No Hermes session diagnostics.

TASK-SPECIFIC DOCS:
None initially.
Use source inspection to find the Fin write boundary.
If source references a required Fin doc, read that exact doc and report why.

ALLOWED SCOPE:
Telegram confirmation path, conversation draft/action lifecycle, Fin write boundary, result handling, tests.

FORBIDDEN TASK-SPECIFIC SCOPE:
AGENTS.md, ChatGPT rules docs, UI, Telegram tokens, real Telegram API, provider/model calls, runtime profiles, production expense creation by Codex.

PLAN:
1. Map confirmation path for text and voice transcript.
2. Map existing Fin write boundary.
3. Prove where the chain breaks.
4. Implement minimal fix.
5. Add targeted tests with temp/fake storage.
6. Commit and push.

TARGETED CHECKS:
Run focused tests for conversation drafts, Telegram polling/connector, Fin storage/contracts, and modified modules.

ACCEPTANCE:
Text and voice “Записывай” use the ready draft.
The Fin write boundary is called in tests.
A temp/test DB records the expense.
The success reply is based on the actual write result.
Failure does not claim success.
No live side effects.

REPORT:
Use AGENTS.md report contract.
Add task-specific fields:
- confirmation_flow_map
- voice_confirmation_path
- fin_write_boundary
- db_write_result
- action_result_state
- production_side_effects

### 12. Priority

These rules supersede older ChatGPT prompt-construction rules that required repeating standard Codex blocks.

After AGENTS.md, ChatGPT-created Codex prompts must be short, task-specific, and must not duplicate the standard Codex execution contract.

## 16. Non-goals

ChatGPT must not:

- create new rule files when an existing rule file should be updated;
- put ChatGPT dialogue rules into `AGENTS.md`;
- put Codex execution rules into ChatGPT-only workflow text unless needed for distinction;
- add Hermes/vendor docs to every prompt by default;
- solve a local symptom without checking the higher-level cause;
- repeat long standard Codex blocks already covered by `AGENTS.md`;
- provide archives/files when the user asked for pasteable text;
- claim live UI inspection from raw HTML;
- accept malformed Codex reports without proof.
