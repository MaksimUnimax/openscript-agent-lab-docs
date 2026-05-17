STATUS: IMPORTED_DESIGN_PROPOSED
SOURCE_KIND: docs-only runtime storage initializer proof/design
DATE: 2026-05-17

# Fin Instrument Runtime Storage Initializer

## Scope

Design the minimal runtime storage initializer for the Fin Instrument financial tool.

This slice is only about bootstrap and readiness policy. It does not create runtime state in this run.

The initializer is the narrow bridge between:
- source-owned contracts and handlers in `agent_lab/fin_instrument/`;
- the proposed SQLite schema for the financial runtime;
- the future private runtime root that lives outside git.

## Non-Goals

- No database creation in this run.
- No runtime directory creation in this run.
- No migration implementation in this run.
- No application code changes in this run.
- No UI implementation in this run.
- No Telegram integration in this run.
- No Agent Farm integration in this run.
- No `.sql` files in this run.
- No destructive migration by default.
- No secret storage.

## Runtime Root

Proposed private runtime root:

`/var/lib/openscript-agent-lab/fin-instrument/`

This path is runtime state, not git source.

It is separate from:
- `docs/codex_source/**`
- `agent_lab/**`
- public docs export
- Telegram auth or provider stores

The runtime tree may later contain:
- SQLite database files;
- receipt drafts and attachments;
- exports and backups;
- runtime-only audit data.

## DB Path

Proposed SQLite database file:

`/var/lib/openscript-agent-lab/fin-instrument/finance.sqlite3`

The database file is not created in this run.

## Initializer Responsibilities

The future initializer should do exactly the following:

1. Create the runtime root directory if it does not exist.
2. Create the SQLite database file if it does not exist.
3. Apply the schema bootstrap in an idempotent transaction.
4. Initialize `schema_version`.
5. Insert migration history rows into `schema_migrations`.
6. Seed default categories and payment sources only if that seeding is explicitly approved.
7. Validate an existing database schema before any writes.
8. Report readiness without exposing raw SQL or secrets.
9. Refuse destructive migration behavior by default.

The initializer should not silently mutate business data.

## Source Module Plan

Preferred future module layout:

- `agent_lab/fin_instrument/storage_initializer.py`
- `agent_lab/fin_instrument/storage.py`
- `agent_lab/fin_instrument/schema.py`
- `agent_lab/fin_instrument/migrations.py`

Role split:
- `storage_initializer.py` owns bootstrap and readiness orchestration.
- `storage.py` owns safe storage entry points.
- `schema.py` owns schema constants and checksums.
- `migrations.py` owns forward-only migration definitions.

If the repo later prefers fewer files, the same responsibilities may be grouped, but the initializer entry point should stay separate from business-tool handlers.

## Bootstrap Strategy

The initializer should treat bootstrap as a deterministic, idempotent, forward-only operation.

Recommended flow:
1. Ensure the runtime root exists.
2. Open SQLite in the runtime root.
3. Apply `PRAGMA foreign_keys=ON`.
4. Use `PRAGMA journal_mode=WAL` when the runtime environment supports it.
5. Set a finite `busy_timeout`.
6. Validate the expected schema checksum/version.
7. Create `schema_version` and `schema_migrations` if they are missing.
8. Apply bootstrap migration(s) inside an explicit transaction.
9. Record the applied migration id and checksum.
10. Re-read readiness and return a compact status payload.

Bootstrap should be idempotent:
- re-running it must not duplicate seed rows or migration rows;
- re-running it must not rewrite valid schema state;
- a matching database should be reported as ready rather than recreated.

Schema checksum and version guard:
- the initializer should compare the runtime schema version and checksum against the source-owned schema definition;
- an unknown checksum should block writes and report `schema_mismatch`;
- a version gap should report `migration_required`;
- destructive repair must never happen automatically.

Transaction boundary:
- bootstrap should run in a single explicit transaction when possible;
- if the bootstrap fails, the transaction must roll back;
- partial state should not be treated as ready.

## PRAGMA And Settings

Recommended settings for the future initializer:

- `PRAGMA foreign_keys=ON`
- `PRAGMA journal_mode=WAL` when supported
- `PRAGMA busy_timeout=<finite value>`

Optional later tuning, only if needed:
- `PRAGMA synchronous=NORMAL`
- temporary store / cache tuning for read-heavy reporting

The first slice should keep the PRAGMA set small and deterministic.

## Migration Strategy

Use a forward-only migration model.

Design rules:
- `schema_migrations` is append-only history.
- `schema_version` is the current pointer.
- each migration has a stable id and checksum.
- bootstrap must refuse unknown or drifted checksums.
- no automatic downgrade path.
- no destructive migration without explicit backup and review.

If a future destructive change is ever needed:
- create a backup first;
- prove the change in a separate run;
- do not make the initializer self-modifying by default.

## Permission Strategy

The runtime tree should be owned by the runtime service user and not be world-writable.

Recommended policy:
- runtime root permissions: restrictive, typically `0700` or `0750`
- SQLite file permissions: restrictive, typically `0600` or `0640`
- backup/export directories: same ownership policy as the runtime root

Rules:
- no world-writable files;
- no secrets in the DB;
- no Telegram tokens, provider credentials, or raw auth files in runtime storage;
- audit data may be persisted, but it must be sanitized and non-secret.

## Readiness States

The future initializer should be able to report the following states:

- `storage_missing`
- `db_missing`
- `schema_uninitialized`
- `schema_ready`
- `schema_mismatch`
- `migration_required`
- `migration_failed`
- `permission_error`
- `corrupted_or_unreadable`
- `ready`

State meaning:
- `storage_missing`: runtime root is absent.
- `db_missing`: runtime root exists but the database file does not.
- `schema_uninitialized`: database exists but bootstrap has not been applied.
- `schema_ready`: schema and version are valid and writable.
- `schema_mismatch`: checksum or version drift was detected.
- `migration_required`: a safe non-destructive migration is needed.
- `migration_failed`: a migration attempted and failed.
- `permission_error`: filesystem permissions block access.
- `corrupted_or_unreadable`: SQLite file cannot be opened safely.
- `ready`: the storage layer is initialized and validated.

## Failure Behavior

Failure must be safe and explicit.

Rules:
- do not auto-repair unknown schema drift;
- do not auto-delete or rebuild a suspicious database;
- do not hide permission failures;
- do not return stack traces in user-facing responses;
- do not report `ready=true` until the schema version and checksum are validated;
- do not let business writes proceed when the runtime state is `schema_mismatch`, `migration_required`, `permission_error`, or `corrupted_or_unreadable`.

Tool-status behavior after initializer:
- before init: `tool_status` should keep `ready=false` and `storage_initialized=false`;
- after successful init: `tool_status` should report `ready=true` and `storage_initialized=true`;
- on schema mismatch: block writes and return a safe reason without destructive changes.

## Relationship To Current Contracts

The initializer must fit the current source-owned financial tool contracts:
- `expense_add`
- `expense_recent`
- `expense_month_summary`
- `receipt_photo_draft`
- `receipt_manual_complete`
- `cancel_pending`
- `tool_status`

Contract alignment:
- the handlers stay deterministic and safe;
- the initializer supplies the readiness source for those handlers later;
- the agent must still not write SQL directly;
- storage mutation remains behind deterministic storage functions.

## Test Plan

Future implementation tests should cover:

- creating the runtime root in a temporary directory;
- creating the SQLite database file in that temporary directory;
- applying schema bootstrap successfully;
- idempotent second run;
- a `schema_version` row exists after bootstrap;
- migration rows are recorded exactly once per migration;
- no writes escape the configured temp directory;
- permission failure is handled safely;
- schema mismatch is detected and blocks writes;
- no float money paths are introduced;
- no raw SQL can be passed through the agent path.

Test style:
- use temp directories and isolated SQLite files;
- never rely on production runtime state in tests;
- keep bootstrap tests deterministic and fast.

## Next Implementation Slice Recommendation

Recommended next slice:
- `runtime_storage_initializer_implementation`

Why:
- it is the smallest runtime-facing step after schema design;
- it can be tested with temp-dir fixtures without touching production storage;
- it proves the source/runtime boundary before any UI or Telegram integration;
- it keeps the work narrow and reviewable.

Suggested implementation posture:
- configurable runtime root;
- explicit initializer entry point;
- no auto-run on service startup until reviewed;
- no UI or Telegram coupling in the same run.

## Open Questions

- Should the initializer always create the runtime root, or only when an explicit admin action requests it?
- Should default category and payment source seeding happen in bootstrap or in a separate deterministic seed step?
- Should `journal_mode=WAL` be enforced everywhere or only when the environment permits it safely?
- Should `tool_status` call the initializer lazily, or remain read-only until a separate admin action runs bootstrap?
- Should backup and export directories be created eagerly or only when the first backup/export run happens?
