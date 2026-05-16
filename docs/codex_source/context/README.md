# Context

STATUS: INITIAL_FROM_CURRENT_REPO_DOCS

This directory stores append-only dialogue context for ChatGPT and Codex.

Rules:
- never rewrite historical blocks destructively
- only append new blocks
- keep the manifest updated
- Codex should read the manifest and the tail, not the whole file, for future append work
