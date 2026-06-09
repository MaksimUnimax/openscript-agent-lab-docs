# Public docs refresh workflow

PURPOSE:
Synchronize the public docs mirror from the private source repo so ChatGPT can read current project memory from GitHub.

SOURCE:
- private repo: /opt/openscript-agent-lab
- source docs tree: /opt/openscript-agent-lab/docs/codex_source/

DESTINATION:
- public docs repo: /opt/openscript-agent-lab-docs
- destination docs tree: /opt/openscript-agent-lab-docs/docs/codex_source/

PUBLIC REPO CONTENT RULE:
The public docs repo must contain only docs/codex_source/** and normal .git metadata.

SAFE REFRESH STEPS:
1. Verify private repo HEAD equals origin/main.
2. Verify public docs repo HEAD equals origin/main.
3. Verify private docs contain the expected current append ids.
4. Verify public repo is clean or only has intended docs changes.
5. Verify public repo contains no files outside docs/codex_source/**.
6. Replace public docs/codex_source/** with private docs/codex_source/** using a local file sync that copies only this subtree.
7. Do not copy runtime files, secrets, application code, tests, tools, agent packages, databases, .env, auth files, or logs.
8. Run diff/checks.
9. Stage only public docs/codex_source/**.
10. Commit and push public docs repo.
11. Verify public origin/main == HEAD.
12. Verify public docs include current append ids and active block.

FORBIDDEN:
- no files outside docs/codex_source/**
- no runtime files
- no secrets/auth/env
- no application code
- no Telegram/Hermes/provider/model calls
- no service restart
- no destructive operation outside the public docs repo
- no private source code changes
