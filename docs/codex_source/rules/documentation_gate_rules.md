# Documentation gate rules

STATUS: NEEDS_IMPORT_FROM_CHATGPT_UPLOADS

Minimal gate rules:
- vendor docs are source-of-truth for vendor behavior
- project docs are source-of-truth for project-specific memory and rules
- roadmap/context are memory, not vendor docs
- if required docs are missing or stubbed, the future fix-run must stop
- do not replace missing docs with memory-based assumptions
