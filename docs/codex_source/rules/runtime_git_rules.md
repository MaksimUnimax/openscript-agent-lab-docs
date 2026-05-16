# Runtime git rules

STATUS: IMPORTED_FROM_CHATGPT_UPLOAD

Rules captured from current repo state and current docs workflow:
- branch baseline is `main`
- keep commits scoped to the requested docs layer
- do not stage unrelated `agent-packages/**` changes
- use non-destructive git operations only
- report empty remote honestly instead of inventing push targets
- if a repo has a configured origin, verify `origin/main` before changing docs baselines
- do not force push unless explicitly authorized
- for docs sync runs, stage only `docs/codex_source/**`
- keep the private source repo and public docs repo separate in reports
- after private docs changes are committed and pushed, refresh the public docs repo mirror
- public docs repo must contain only `docs/codex_source/**`
- never export application code, runtime files, secrets, or `agent-packages/**` to the public docs repo
