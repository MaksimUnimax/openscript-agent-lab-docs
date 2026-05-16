# Rules update - repo documentation access model v2

STATUS: IMPORTED_CURRENT_RULE
SOURCE_KIND: inline prompt content
VERSION: repo_documentation_access_v2
DATE: 2026-05-16

## 1. Why this update exists

The previous working mode assumed that Codex did not reliably have access to ChatGPT-uploaded project documents.

That assumption is no longer the normal workflow.

Current workflow:
- Project documentation is stored in the private source repo under `docs/codex_source/**`.
- Codex works inside `/opt/openscript-agent-lab` and can read repo documentation from `/opt/openscript-agent-lab/docs/codex_source/**`.
- A public docs-only repo mirrors the same documentation under `docs/codex_source/**`.
- ChatGPT can read the public docs repo at `https://github.com/MaksimUnimax/openscript-agent-lab-docs`.
- Therefore, future prompts do not need to inline every large document just because Codex lacks files.

But this does not allow Codex to browse everything.

New core rule:
Codex must read only the exact docs named by ChatGPT in `DOCS_TO_READ` for the current task.

## 2. Old rule replaced

Replace this old general rule:

Codex does not have the documents, therefore assistant must inline all documentation.

With this new rule:

Codex has access to repo documentation under `/opt/openscript-agent-lab/docs/codex_source/**`, but ChatGPT must specify exact paths to read for each task. If required docs are missing, stub, contradictory, or not listed, Codex must STOP instead of guessing.

Uploaded ChatGPT file names may be used only as provenance metadata.
They are not usable sources for Codex unless their content has been imported into repo docs or pasted inline in the prompt.

## 3. `DOCS_TO_READ` is mandatory

Every Codex prompt for OpenScript Agent Lab must include `DOCS_TO_READ`.

Each entry must include:
- path;
- why this file is needed;
- whether it is required.

Example format:

```yaml
DOCS_TO_READ:
- path: docs/codex_source/ENTRYPOINT_FOR_CHATGPT.md
  why: repo docs entrypoint and read policy
  required: yes

- path: docs/codex_source/project/current_status.md
  why: current project stop-point and imported docs status
  required: yes

- path: docs/codex_source/task_cards/<task>.yaml
  why: active task contract
  required: when task card exists

- path: docs/codex_source/vendor/<vendor>/<exact_file>.md
  why: vendor/API/CLI/auth/runtime contract for this task
  required: when task depends on that vendor/API/CLI/auth/runtime

- path: docs/codex_source/project/<project_doc>.md
  why: project architecture/business contract for this task
  required: when task depends on project architecture
```

## 4. Codex report must show docs actually read

Every report must include:

```yaml
DOCS:
- docs_to_read_provided: yes/no
- docs_read:
- docs_missing:
- docs_stub:
- docs_contradictions:
- documentation_gate_passed: yes/no

BASELINE_USED:
- project_docs:
- vendor_docs:
- rules_docs:
- task_card:
```

If no docs were needed, the report must explicitly explain why.

## 5. Do not read all docs by default

Forbidden by default:
- reading all `docs/codex_source/**`;
- broad repo archaeology;
- reading full large context files for every task;
- reading all vendor docs when only one vendor contract is relevant;
- reading roadmap as replacement for vendor docs;
- reading context as replacement for task card;
- reading code first and then inventing a fix without docs.

Allowed:
- read `ENTRYPOINT_FOR_CHATGPT.md`;
- read `index.yaml`;
- read `project/current_status.md`;
- read the active task card if listed;
- read exact vendor/project/rules files named in `DOCS_TO_READ`;
- for append-only tasks, read manifest and tail/duplicate check only.

## 6. Documentation gate remains mandatory

Every proof/design/fix must be grounded in relevant documentation.

If a task depends on a vendor, API, CLI, SDK, provider, auth, runtime contract or external system, Codex must read the exact vendor/source docs listed in `DOCS_TO_READ`.

Examples:
- Hermes auth/provider task requires exact Hermes vendor docs.
- Telegram Bot API task requires exact Telegram vendor docs.
- Telegram user identity/allowlist requires Telegram identity/security docs and project access-control docs.
- Agent package/runtime profile task requires `technical_spec.md`, `source_vs_runtime.md`, `safe_boundaries.md`, task card, and exact Hermes docs if Hermes behavior is involved.
- Roadmap/context import uses manifests and exact append/import content, not application code.

Project docs, roadmap, context and previous reports may provide project state.
They do not replace vendor/API/CLI/auth documentation when external mechanisms are involved.

## 7. Baseline modes

Mode A - assistant-provided baseline:
- ChatGPT includes `DOCUMENTATION_BASELINE` or `VENDOR_SOURCE_OF_TRUTH_BASELINE` directly in the prompt.
- Codex uses that baseline and may read exact supporting docs listed in `DOCS_TO_READ`.

Mode B - exact repo-docs baseline:
- ChatGPT lists exact `DOCS_TO_READ` paths.
- Codex extracts the narrow baseline from those files.
- Codex reads only listed docs.
- Codex stops if required docs are missing, stub, contradictory, or insufficient.

High-risk tasks should prefer Mode A plus exact docs, or a proof-only baseline extraction run before any fix.

High-risk tasks include:
- auth;
- provider;
- secrets;
- Telegram delivery;
- runtime profile;
- systemd/nginx;
- storage mutation;
- public/private repo publication;
- any operation that can spend paid resources or leak data.

## 8. STOP conditions

Codex must STOP if:
- required `DOCS_TO_READ` is missing from the prompt;
- a required doc path does not exist;
- a required doc is marked `STUB`, `NEEDS_IMPORT`, `NEEDS_CONFIRMATION`, or similar;
- vendor docs are required but only roadmap/project/context docs are supplied;
- project docs contradict runtime facts and prompt does not say which wins;
- active task card says `ready_for_fix_run: false`;
- exact active task card is required but missing;
- the user asks for a fix but required docs are not imported yet;
- executing the task would require reading broad unrelated directories;
- Codex would need to guess.

STOP report must state:
- missing/stub/contradictory doc path;
- why it is required;
- what import/update is needed next.

## 9. Prompt template rule

Every technical prompt should include:

- ТЗ проверено.
- `DOCS_TO_READ`.
- `DOCUMENTATION_GATE`.
- `DOCUMENTATION_BASELINE` or instruction to extract exact baseline from listed docs.
- `RUNTIME_BASELINE`.
- `UNIVERSALITY_CHECK`.
- `ALLOWED_SCOPE`.
- `FORBIDDEN_SCOPE`.
- `CHECKS`.
- `ACCEPTANCE`.
- `REPORT`.

## 10. Repo directories to use

Private source repo:
- `/opt/openscript-agent-lab`

Private repo docs root:
- `/opt/openscript-agent-lab/docs/codex_source`

Public docs repo:
- `https://github.com/MaksimUnimax/openscript-agent-lab-docs`

Public docs content rule:
- public repo contains only `docs/codex_source/**`.

Important docs paths:
- `docs/codex_source/ENTRYPOINT_FOR_CHATGPT.md`
- `docs/codex_source/index.yaml`
- `docs/codex_source/project/current_status.md`
- `docs/codex_source/project/technical_spec.md`
- `docs/codex_source/project/project_overview.md`
- `docs/codex_source/project/source_vs_runtime.md`
- `docs/codex_source/project/safe_boundaries.md`
- `docs/codex_source/roadmap/roadmap_manifest.yaml`
- `docs/codex_source/roadmap/imported/roadmap_v0_7_current.md`
- `docs/codex_source/context/context_manifest.yaml`
- `docs/codex_source/module_map/module_map_manifest.yaml`
- `docs/codex_source/vendor/hermes/**`
- `docs/codex_source/vendor/telegram/**`
- `docs/codex_source/task_cards/**`
- `docs/codex_source/rules/**`

## 11. What this update does not allow

This update does not allow:
- guessing from code without docs;
- reading everything to avoid choosing correct docs;
- using roadmap as vendor docs;
- using context as task contract;
- using previous reports as source-of-truth for external API rules;
- fixing auth/provider/Telegram/runtime without relevant docs;
- marking a task ready while task card or required docs say not ready;
- staging `agent-packages/**` accidentally.

## 12. Current import state after this rules update

Expected state after this update:
- technical spec v0.3 imported;
- working context imported;
- roadmap v0.7 imported;
- Hermes vendor docs imported;
- Telegram Bot API vendor docs imported;
- repo documentation access rules imported;
- module map / safe boundaries still pending unless imported separately;
- prompt templates may need separate review if external to rules docs;
- main feature work remains paused until module map / safe boundaries and task cards are ready.
