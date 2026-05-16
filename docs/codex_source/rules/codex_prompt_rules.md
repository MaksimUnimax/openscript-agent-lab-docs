# Codex prompt rules

STATUS: NEEDS_IMPORT_FROM_CHATGPT_UPLOADS

Minimal seed rules:
- read the active task card and exact required docs
- if required docs are `stub` or `needs_import`, stop with `STOP_DOCS_MISSING`
- append-only files should be read via manifest + tail only
- do not rewrite historical blocks destructively
- do not infer missing task facts from memory alone
