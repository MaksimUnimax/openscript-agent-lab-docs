# Fin Instrument Runtime

STATUS: IMPORTED_DESIGN_PROPOSED
SOURCE_KIND: docs-only product correction
DATE: 2026-05-17

## Purpose

Define the current runtime and UI surface for the financial agent line.

The current product correction is:
- finish the financial agent / “Фин инструмент” first;
- do not move immediately to a generic Agent Farm / Task Runtime;
- keep the financial scenario runtime inside the “Фин инструмент” surface for the current stage.

## Current Correction

This design reflects the corrected product order:
- the current Telegram-facing tab is treated as “Фин инструмент”;
- the financial workflow, Telegram access, voice settings and runtime status belong there;
- Agent Farm is a future direction, not the immediate next block.

## Why Runtime Is Currently Inside “Фин инструмент”

The current product surface already carries the live financial-agent entry points:
- Telegram bot access and allowlist controls;
- voice settings for the financial workflow;
- runtime status and readiness;
- future financial tool status and storage controls.

For the current stage, this is the least surprising place for the operator to manage the financial scenario.

## Repo Proof Summary

Bounded repo proof shows:
- Telegram/router/access-control implementation already exists in `agent_lab/telegram_*` and `agent_lab/admin_server.py`;
- the visible UI tab has already been renamed to “Фин инструмент”;
- safe runtime status already exposes Telegram/polling/reply/auth readiness fields;
- there is no dedicated financial business-tool implementation yet;
- there are no active Agent Farm runtime modules that should become the next product block before the Fin Instrument line is progressed.

## Product Surface

The “Фин инструмент” runtime surface should expose:
- access control status;
- voice status;
- financial readiness status;
- storage/database readiness status;
- recent financial operations;
- pending receipt drafts;
- monthly summary preview;
- audit trail / recent operations;
- manual confirmation controls.

## Runtime Responsibilities

For the current stage, runtime inside “Фин инструмент” should:
- receive Telegram/voice inputs for the financial agent line;
- enforce access control and deny-before-resource-use rules;
- hand allowed inputs into deterministic financial business tools;
- track storage/state/readiness;
- expose concise factual status to the UI;
- preserve the existing explicit auth recovery flow for Hermes/provider readiness;
- avoid becoming a general-purpose Agent Farm task scheduler yet.

## UI Model

The UI inside “Фин инструмент” should contain:
- access-control status and allowlist summary;
- Telegram/voice readiness and last activity;
- financial tool readiness;
- storage/database health;
- recent expenses;
- pending receipt drafts;
- monthly summary preview;
- audit/recent tool operations;
- operator actions for safe confirmation and refresh.

## Storage Boundaries

Proposal for the current stage:
- source docs and contracts stay in `docs/codex_source/**`;
- deterministic tool code lives in the repo, not in runtime state;
- runtime data lives under a safe private runtime root such as `/var/lib/openscript-agent-lab/fin-instrument/`;
- SQLite or equivalent state, receipt artifacts, draft state and audit state stay outside git;
- no secrets, bot tokens or provider auth values go to git or public docs.

Runtime storage should be separate from:
- agent package source;
- Hermes runtime profile auth files;
- Telegram bot token files;
- public docs mirror.

## Safety Constraints

- Do not let agents write SQL directly.
- Do not expose the raw database as agent-owned storage.
- Do not mix the financial tool with Telegram Publisher or YouTube tooling.
- Do not move to Agent Farm before the Fin Instrument line is reviewed and progressed.
- Do not change provider credentials or auth stores in this design.
- Do not commit runtime data or secrets.

## Future Relationship To Agent Farm

Agent Farm remains a future architecture question:
- shared runtime for all agents;
- per-tool runtime tabs;
- or a hybrid.

That decision is intentionally deferred.

The current active block is finishing the Fin Instrument / Financial Tool line first.

## Open Questions

- Should the financial tool use one SQLite file or a small set of per-domain files?
- What amount precision and currency normalization should the tool enforce?
- How should receipt drafts be named and retained?
- Which operations require explicit user confirmation before final write?
- Should storage live under a single `/var/lib/openscript-agent-lab/fin-instrument/` tree or a nested profile-like structure?
- What minimum status fields must be visible in the UI before implementation starts?
