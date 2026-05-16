# Module Map - OpenScript Agent Lab

STATUS: CURRENT_SNAPSHOT_FROM_REPO_INVENTORY
SOURCE_KIND: repo inventory + imported docs
SCOPE: docs/proof snapshot, not a code change
DATE: 2026-05-16

This snapshot includes current safe boundaries derived from imported docs and bounded repo inventory.

## Source Of Truth

- Current `Тз v0.3` is imported and current.
- Roadmap `v0.7` is imported and current.
- Rules `repo_documentation_access_v2` is imported and current.
- This snapshot is built from bounded repo inventory and imported docs only.
- Unknowns are marked pending proof instead of guessed.

## Docs Read For This Snapshot

- `docs/codex_source/ENTRYPOINT_FOR_CHATGPT.md`
- `docs/codex_source/index.yaml`
- `docs/codex_source/project/current_status.md`
- `docs/codex_source/project/technical_spec.md`
- `docs/codex_source/project/project_overview.md`
- `docs/codex_source/project/source_vs_runtime.md`
- `docs/codex_source/project/safe_boundaries.md`
- `docs/codex_source/project/runtime_git_canon.md`
- `docs/codex_source/roadmap/roadmap_manifest.yaml`
- `docs/codex_source/roadmap/imported/roadmap_v0_7_current.md`
- `docs/codex_source/rules/repo_documentation_access_rules.md`
- `docs/codex_source/rules/documentation_gate_rules.md`
- `docs/codex_source/rules/codex_prompt_rules.md`
- `docs/codex_source/rules/runtime_git_rules.md`
- `docs/codex_source/rules/append_only_memory_rules.md`
- `docs/codex_source/module_map/module_map_manifest.yaml`
- `docs/codex_source/module_map/module_map.md`
- `docs/codex_source/context/context_manifest.yaml`
- `docs/codex_source/project/import_queue/missing_sources.yaml`

## Inventory Commands Used

Allowed bounded inventory:
- `find . -maxdepth 2 -type d` with pruning for `.git`, `__pycache__`, `.pytest_cache`, `.venv*`, runtime/cache directories
- `find agent_lab -maxdepth 2 -type f`
- `find tools -maxdepth 2 -type f`
- `find tests -maxdepth 2 -type f`
- `find docs/codex_source -maxdepth 3 -type f`
- `find agent-packages -maxdepth 2 -type f`
- `find tool-registry -maxdepth 3 -type f`
- `find vendor -maxdepth 2 -type d`

Targeted reads:
- `sed -n` on imported docs and current status files
- `rg -n '^def |^class '` on bounded application modules and CLI entrypoints

## Top-Level Tree Summary

- `agent_lab/` contains the runtime application backend, routing, Telegram integration, Hermes/provider wiring, storage, runtime apply, and static UI assets.
- `docs/` contains the repo-based documentation source-of-truth layer.
- `tests/` contains module-level regression tests.
- `tools/` contains CLI and maintenance scripts.
- `tool-registry/` contains registry data used by the runtime.
- `agent-packages/` contains agent source packages and unrelated dirty/untracked workspace state.
- `vendor/hermes-agent/` contains the local Hermes vendor source checkout.
- `.venv-hermes/` was referenced by imported docs as the local Hermes runtime environment, but it was not inventoried in the bounded tree command because it is treated as runtime/environment state.
- `agent-templates/` is not present in the current bounded inventory.

## Main Roots And Ownership

| Path | Classification | Responsibility | Docs-run edit policy | Fix-run edit policy | Forbidden changes | Proof status |
| --- | --- | --- | --- | --- | --- | --- |
| `docs/codex_source/**` | private docs source-of-truth | ChatGPT/Codex repo memory, vendor docs, task cards, append-only context/roadmap/module map | yes | yes, only docs tasks | no code/runtime/secrets | proven |
| public docs repo mirror | public mirror of `docs/codex_source/**` | public read path for ChatGPT and public docs-only publication | mirror refresh only | no direct app edits | no app code, runtime, secrets, agent packages | proven |
| `agent_lab/**` | application/backend/UI code | admin server, Telegram routing, Hermes/provider wiring, runtime apply, storage, UI assets | no | only with exact code scope | no broad docs-run edits | proven from inventory |
| `tools/**` | utility / maintenance scripts | `agentctl`, vendor restore helpers | no | only with exact script scope | no docs-run edits outside docs tasks | proven from inventory |
| `tests/**` | regression tests | module-level proof and regression coverage | no | only with exact test scope | no docs-run edits | proven from inventory |
| `agent-packages/**` | agent source packages and dirty workspace | per-agent documents, defaults, skills, README files | no | only with explicit package scope | do not stage accidentally in unrelated runs | proven from inventory |
| `tool-registry/**` | registry data | tool definitions and tool capability metadata | no | only with explicit registry scope | do not confuse with code or docs | proven from inventory |
| `vendor/hermes-agent/**` | local vendor source checkout | Hermes upstream source tree used by runtime/docs | no | only with explicit vendor scope | do not casually edit or read internals in docs runs | proven top-level only |
| `/var/lib/openscript-agent-lab/**` | private runtime state | runtime state, profiles, memories, sessions, runtime auth, apply artifacts | no | only with explicit runtime scope | no git, no public export | inferred from imported docs |
| `/var/log/openscript-agent-lab/**` | private runtime logs | runtime logs and diagnostics | no | only with explicit runtime scope | no git, no public export | inferred from imported docs |
| `/var/lib/openscript-agent-lab/hermes/**` | private Hermes runtime state | Hermes profiles, auth, memories, sessions, logs | no | only with explicit runtime scope | no source-of-truth mixing | inferred from imported docs |

## Current Code Modules

### Application / backend / UI layer

| File | Responsibility | Proof status |
| --- | --- | --- |
| `agent_lab/admin_server.py` | HTTP admin server, route wiring, API endpoints, UI serving, Hermes auth recovery helpers | proven by imports/routes |
| `agent_lab/agentctl_core.py` | backend orchestration for agents, provider state, Telegram config, apply/dry-run, execution helpers | proven by exported functions |
| `agent_lab/agent_reply.py` | universal agent reply construction and Hermes reply execution | proven by exported functions |
| `agent_lab/routing.py` | agent selection and route resolution | proven by exported functions |
| `agent_lab/runtime_apply.py` | source package to runtime profile sync, diff, backup and apply flow | proven by exported functions |
| `agent_lab/storage.py` | source package and runtime profile persistence, manifests, docs, skills and defaults | proven by exported functions |
| `agent_lab/paths.py` | canonical repo/runtime path helpers and slug/doc/skill validation | proven by exported functions |
| `agent_lab/request_cache.py` | request-scope cache helpers | proven by exported functions |
| `agent_lab/response_shapes.py` | compact response DTO helpers for UI/API output | proven by exported functions |

### Hermes / provider / auth / binding layer

| File | Responsibility | Proof status |
| --- | --- | --- |
| `agent_lab/hermes_binding.py` | agent-to-Hermes binding mapper and execution context assembly | proven by imports/classes |
| `agent_lab/hermes_execution.py` | Hermes vendor inspection, auth readiness, execution adapter, smoke/proof runs | proven by exported functions |
| `agent_lab/hermes_status.py` | auth metadata, config metadata, profile status, provider auth status | proven by exported functions |
| `agent_lab/llm_connections.py` | LLM connection registry, agent bindings, model catalog, connection secrets metadata | proven by exported functions |
| `agent_lab/tool_registry.py` | tool registry data, tool capability registry, voice dependency status | proven by exported functions |

### Telegram / voice / access-control layer

| File | Responsibility | Proof status |
| --- | --- | --- |
| `agent_lab/telegram_bot_api.py` | Telegram API request wrapper and command sync | proven by exported functions |
| `agent_lab/telegram_commands.py` | command normalization, uniqueness, and route command generation | proven by exported functions |
| `agent_lab/telegram_connector.py` | Telegram router state, access control, voice gates, update normalization, routing | proven by exported functions |
| `agent_lab/telegram_polling.py` | polling loop, update fetch, message send, reply summaries, voice pipeline orchestration | proven by exported functions |
| `agent_lab/telegram_runtime.py` | runtime thread gating and polling enablement | proven by exported functions |
| `agent_lab/telegram_voice_transport.py` | voice metadata, controlled download, STT, send-voice proof, sanitization | proven by exported functions |
| `agent_lab/system_filter_hooks.py` | input/output inspection hooks and voice status snapshots | proven by exported functions |

### CLI / maintenance / UI assets

| File or directory | Responsibility | Proof status |
| --- | --- | --- |
| `tools/agentctl` | CLI wrapper for backend and admin-server commands | proven by exported functions |
| `tools/restore_hermes_vendor.py` | vendor checkout inspection/restore helper | proven by exported functions |
| `agent_lab/static/app.js` | browser UI logic for admin/editor views | inferred from file name and imports |
| `agent_lab/static/index.html` | UI shell | inferred from file name |
| `agent_lab/static/style.css` | UI styling | inferred from file name |

### Tests

| File group | Responsibility | Proof status |
| --- | --- | --- |
| `tests/test_admin_server.py` | admin server regression coverage | proven by file name |
| `tests/test_agent_reply.py` | reply pipeline regression coverage | proven by file name |
| `tests/test_execution_dry_run.py` | execution dry-run coverage | proven by file name |
| `tests/test_hermes_execution.py` | Hermes execution coverage | proven by file name |
| `tests/test_hermes_status.py` | Hermes status coverage | proven by file name |
| `tests/test_llm_connections.py` | LLM connection and binding coverage | proven by file name |
| `tests/test_paths.py` | path helper and slug validation coverage | proven by file name |
| `tests/test_restore_hermes_vendor.py` | vendor restore coverage | proven by file name |
| `tests/test_routing.py` | routing coverage | proven by file name |
| `tests/test_runtime_apply.py` | runtime apply coverage | proven by file name |
| `tests/test_storage.py` | storage/persistence coverage | proven by file name |
| `tests/test_system_filter_hooks.py` | filter hook coverage | proven by file name |
| `tests/test_telegram_bot_api.py` | Telegram API wrapper coverage | proven by file name |
| `tests/test_telegram_commands.py` | Telegram command normalization coverage | proven by file name |
| `tests/test_telegram_connector.py` | Telegram connector/access control coverage | proven by file name |
| `tests/test_telegram_polling.py` | Telegram polling coverage | proven by file name |
| `tests/test_telegram_voice_transport.py` | Telegram voice pipeline coverage | proven by file name |

## Key Boundaries

- `docs/codex_source/**` is the project documentation source-of-truth for ChatGPT and Codex.
- The public docs repo mirrors only `docs/codex_source/**`.
- `agent_lab/**` is application/backend/UI code.
- `agent-packages/**` are git-tracked agent source packages and an unrelated dirty workspace that must not be accidentally staged.
- `vendor/hermes-agent/**` is the local Hermes vendor source checkout; it is separate from repo docs.
- `/var/lib/openscript-agent-lab/hermes/**` is runtime state, not source-of-truth.
- runtime auth, memories, sessions, logs and similar generated state must not go to git or public docs.
- source package != runtime profile.
- no symlinks for `SOUL.md` or `config.yaml`.
- UI edits source package, `agentctl apply` synchronizes into runtime.
- business logic owns money, DB facts and reports; agent/LLM owns language, tone and explanation only.
- skills are instructions and requirements, not tool permissions.
- tool registry data defines capabilities and permission bindings.
- Telegram Router, business layer, provider/auth, tools and runtime apply are separate concerns.
- `/opt/openscript-expense-bot`, `/opt/ai-starter-community` and `/opt/autopostmanager` stay out of scope unless a task explicitly names them.

## Pending Proof

- exact granular ownership inside `agent_lab/` may need a later deeper proof for some modules;
- `agent-templates/` is absent in the current bounded inventory;
- task card readiness still needs re-evaluation after this snapshot import;
- project docs `agent_lab_architecture`, `agent_package_vs_runtime_profile`, `telegram_router`, `telegram_voice_pipeline`, `universal_hermes_reply_path`, `llm_connection_binding` and `access_control` remain stub/placeholder docs and must not be used as substitute proof.
