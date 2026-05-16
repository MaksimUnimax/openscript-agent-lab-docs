# Assistant / Codex workflow rules

STATUS: NEEDS_IMPORT_FROM_CHATGPT_UPLOADS

Minimal enforced workflow rules:
- read `docs/codex_source/ENTRYPOINT_FOR_CHATGPT.md` first
- read `docs/codex_source/index.yaml` before any task-specific work
- read the active task card and exact required docs
- use append-only manifests and tail reads for memory files
- do not rewrite historical roadmap/context blocks destructively
- do not change application code during docs-only runs
- do not stage `agent-packages/**` unless the scope explicitly requires it

Future import needed:
- full project-specific workflow policy
- any team conventions not already captured in repo docs
