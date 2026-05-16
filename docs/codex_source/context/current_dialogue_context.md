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

<!-- CONTEXT_APPEND_BEGIN id=CTX_20260516_GITHUB_DOCS_VISIBILITY source=codex_sync -->
## 2026-05-16 — Public docs repo visibility verified

Facts:
- Private source repo was pushed successfully to `git@github.com:MaksimUnimax/openscript-agent-lab.git`.
- Public docs repo was created at `https://github.com/MaksimUnimax/openscript-agent-lab-docs`.
- Public docs export contains only `docs/codex_source/**`.
- ChatGPT verified public web access to `ENTRYPOINT_FOR_CHATGPT.md`.
- A stale HEAD reference in the entrypoint was detected and corrected by this run.

Next:
- Import real ТЗ, roadmap, rules, context/handoff, and module map into append-only project docs.
- Then continue main ТЗ work using repo entrypoint and exact docs paths.

<!-- CONTEXT_APPEND_END id=CTX_20260516_GITHUB_DOCS_VISIBILITY -->
