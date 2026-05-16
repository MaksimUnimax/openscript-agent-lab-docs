# Current dialogue context

STATUS: INITIAL_FROM_CURRENT_REPO_DOCS

This file is append-only.

Do not rewrite historical blocks destructively.

<!-- CONTEXT_APPEND_BEGIN id=CTX_20260516_0001 source=chatgpt -->
Project memory / docs foundation created:
- `docs/codex_source/**` exists as the repo source-of-truth layer
- Hermes vendor docs have been extracted into `docs/codex_source/vendor/hermes/**`
- Telegram vendor docs have been extracted into `docs/codex_source/vendor/telegram/**`
- a project docs / memory layer is now being created

Current next step:
- import project docs, roadmap, rules, and module-map content into append-only files
- set up GitHub push visibility before resuming any further main ТЗ work

Known repo state:
- unrelated `agent-packages/**` dirty/untracked work exists and must not be staged
- the docs layer must stay separate from application code and vendor source
<!-- CONTEXT_APPEND_END id=CTX_20260516_0001 -->
