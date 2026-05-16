# Runtime git rules

STATUS: INITIAL_FROM_CURRENT_REPO_DOCS

Rules captured from current repo state and current docs workflow:
- branch baseline is `main`
- keep commits scoped to the requested docs layer
- do not stage unrelated `agent-packages/**` changes
- use non-destructive git operations only
- report empty remote honestly instead of inventing push targets
