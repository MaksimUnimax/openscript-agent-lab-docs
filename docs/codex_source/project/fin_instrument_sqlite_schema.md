# Fin Instrument SQLite Schema

STATUS: IMPORTED_DESIGN_PROPOSED
SOURCE_KIND: docs-only schema proof/design
DATE: 2026-05-17

## Scope

Define the first SQLite schema for the Fin Instrument financial tool.

This design is a source-of-truth proposal for future runtime storage work.
It aligns with the source-owned financial tool contracts that already exist in `agent_lab/fin_instrument/`.

The schema is intentionally narrow:
- it supports deterministic financial writes and reads;
- it preserves auditability;
- it keeps the agent out of SQL and storage mutation;
- it does not create a database file in this run.

## Non-Goals

- No database creation.
- No migration execution.
- No runtime storage initializer.
- No UI implementation.
- No Telegram integration.
- No Agent Farm integration.
- No raw SQL execution by the agent.
- No secret storage.

## Runtime Storage Root

Proposed private runtime root:

`/var/lib/openscript-agent-lab/fin-instrument/`

This is runtime state only:
- it is not git source;
- it is not public docs;
- it is not agent package source;
- it may contain SQLite state, drafts, receipts and audit data later.

## Database Path

Proposed SQLite database file:

`/var/lib/openscript-agent-lab/fin-instrument/finance.sqlite3`

The `.db` file is not created in this run.

## Schema Overview

### 1. `schema_version`

Purpose:
- keep the current schema pointer in one place;
- let bootstrap code verify the expected version quickly.

Proposed columns:
- `id` INTEGER PRIMARY KEY CHECK (`id` = 1)
- `version` INTEGER NOT NULL
- `migration_id` TEXT NOT NULL
- `applied_at_utc` TEXT NOT NULL
- `checksum` TEXT NOT NULL

Notes:
- single-row table;
- this is the runtime "current version" pointer.

### 2. `schema_migrations`

Purpose:
- keep append-only migration history;
- let future initializer code detect replay or drift.

Proposed columns:
- `migration_id` TEXT PRIMARY KEY
- `from_version` INTEGER NOT NULL
- `to_version` INTEGER NOT NULL
- `applied_at_utc` TEXT NOT NULL
- `checksum` TEXT NOT NULL
- `applied_by` TEXT NOT NULL
- `status` TEXT NOT NULL

Recommended `status` values:
- `applied`
- `skipped`
- `failed`

### 3. `categories`

Purpose:
- normalize financial categories;
- keep stable keys and readable titles.

Proposed columns:
- `id` INTEGER PRIMARY KEY AUTOINCREMENT
- `key` TEXT NOT NULL UNIQUE
- `title` TEXT NOT NULL
- `parent_id` INTEGER NULL REFERENCES `categories(id)`
- `is_active` INTEGER NOT NULL DEFAULT 1
- `created_at_utc` TEXT NOT NULL
- `updated_at_utc` TEXT NOT NULL

Recommended checks:
- `is_active` is `0` or `1`
- `key` is non-empty and lower snake case

### 4. `payment_sources`

Purpose:
- normalize payment source labels;
- support cash/card/bank/wallet style breakdowns.

Proposed columns:
- `id` INTEGER PRIMARY KEY AUTOINCREMENT
- `key` TEXT NOT NULL UNIQUE
- `title` TEXT NOT NULL
- `type` TEXT NOT NULL
- `is_active` INTEGER NOT NULL DEFAULT 1
- `created_at_utc` TEXT NOT NULL
- `updated_at_utc` TEXT NOT NULL

Recommended `type` values:
- `cash`
- `card`
- `bank`
- `wallet`
- `other`

### 5. `receipt_drafts`

Purpose:
- store draft receipt extraction and confirmation state;
- let the user confirm or cancel before an expense becomes final.

Proposed columns:
- `id` TEXT PRIMARY KEY
- `created_at_utc` TEXT NOT NULL
- `updated_at_utc` TEXT NOT NULL
- `status` TEXT NOT NULL
- `source` TEXT NOT NULL
- `attachment_ref` TEXT NOT NULL
- `source_message_id` INTEGER NULL
- `extracted_amount_minor` INTEGER NULL
- `extracted_currency` TEXT NULL
- `extracted_currency_exponent` INTEGER NULL
- `extracted_date_utc` TEXT NULL
- `extracted_merchant` TEXT NULL
- `extracted_category_key` TEXT NULL
- `raw_text_preview` TEXT NULL
- `confirmation_id` TEXT NULL UNIQUE
- `expires_at_utc` TEXT NULL
- `metadata_json` TEXT NOT NULL DEFAULT '{}'

Recommended `status` values:
- `pending_confirmation`
- `confirmed`
- `cancelled`
- `expired`
- `rejected`

Notes:
- `attachment_ref` is a safe attachment/file reference, not a secret.
- `raw_text_preview` should be short and sanitized.
- draft retention is a storage policy decision, not an agent decision.

### 6. `expense_records`

Purpose:
- store final deterministic expense rows;
- support recent expense reads and monthly summaries.

Proposed columns:
- `id` TEXT PRIMARY KEY
- `occurred_at_utc` TEXT NOT NULL
- `created_at_utc` TEXT NOT NULL
- `updated_at_utc` TEXT NOT NULL
- `amount_minor` INTEGER NOT NULL
- `currency` TEXT NOT NULL
- `currency_exponent` INTEGER NOT NULL DEFAULT 2
- `category_id` INTEGER NOT NULL REFERENCES `categories(id)`
- `category_key_snapshot` TEXT NOT NULL
- `description` TEXT NOT NULL
- `payment_source_id` INTEGER NULL REFERENCES `payment_sources(id)`
- `payment_source_key_snapshot` TEXT NULL
- `receipt_draft_id` TEXT NULL REFERENCES `receipt_drafts(id)` ON DELETE SET NULL
- `source` TEXT NOT NULL
- `source_message_id` INTEGER NULL
- `status` TEXT NOT NULL
- `metadata_json` TEXT NOT NULL DEFAULT '{}'
- `deleted_at_utc` TEXT NULL

Recommended `status` values:
- `active`
- `cancelled`
- `deleted`

Money precision decision:
- use integer minor units in `amount_minor`;
- do not use float;
- keep `currency_exponent` so the storage layer can reconstruct the display value exactly;
- this is deterministic and safer than decimal floating point storage.

Notes:
- `category_key_snapshot` and `payment_source_key_snapshot` preserve history if labels later change.
- `source_message_id` stays nullable because manual entry does not need it.
- `metadata_json` is supplemental, not the primary source of truth.

### 7. `operation_log`

Purpose:
- record safe tool request/response trace;
- support debugging, replay analysis and operator inspection.

Decision for v1:
- a dedicated `tool_requests` table is not required yet;
- `operation_log` is enough for the request/response trace because the tool surface is narrow and deterministic;
- if queueing, retry orchestration or multi-stage replay is added later, a separate `tool_requests` table can be introduced.

Proposed columns:
- `id` TEXT PRIMARY KEY
- `created_at_utc` TEXT NOT NULL
- `actor_type` TEXT NOT NULL
- `actor_id_hash` TEXT NULL
- `operation` TEXT NOT NULL
- `tool_name` TEXT NOT NULL
- `request_id` TEXT NOT NULL UNIQUE
- `entity_type` TEXT NULL
- `entity_id` TEXT NULL
- `status` TEXT NOT NULL
- `safe_summary` TEXT NOT NULL
- `request_json` TEXT NOT NULL DEFAULT '{}'
- `response_json` TEXT NOT NULL DEFAULT '{}'
- `metadata_json` TEXT NOT NULL DEFAULT '{}'
- `error_code` TEXT NULL

Recommended `actor_type` values:
- `user`
- `system`
- `tool`
- `job`

Recommended `status` values:
- `accepted`
- `rejected`
- `completed`
- `blocked`
- `error`

### 8. `audit_events`

Purpose:
- record durable write audit events;
- keep a separate safety log from the broader request trace.

Proposed columns:
- `id` TEXT PRIMARY KEY
- `created_at_utc` TEXT NOT NULL
- `actor_type` TEXT NOT NULL
- `actor_id_hash` TEXT NULL
- `operation` TEXT NOT NULL
- `tool_name` TEXT NOT NULL
- `request_id` TEXT NOT NULL
- `entity_type` TEXT NULL
- `entity_id` TEXT NULL
- `status` TEXT NOT NULL
- `safe_summary` TEXT NOT NULL
- `metadata_json` TEXT NOT NULL DEFAULT '{}'
- `error_code` TEXT NULL

Recommended `status` values:
- `success`
- `failed`
- `blocked`

Notes:
- `audit_events` is for write-capable actions and safety auditing.
- `operation_log` is the broader request/response trace.
- both tables must avoid raw secrets and raw SQL.

### 9. `monthly_summaries_cache`

Decision for v1:
- not included in v1.

Why:
- monthly summaries can be computed from indexed `expense_records`;
- caching adds invalidation complexity before the storage path is proven;
- the first slice should keep the schema small and predictable.

Future option:
- add `monthly_summaries_cache` only after profiling or if read volume proves it necessary.

## Indexes

Proposed indexes:
- `expense_records(occurred_at_utc)`
- `expense_records(category_id)`
- `expense_records(payment_source_id)`
- `expense_records(receipt_draft_id)`
- expression index for month queries on `substr(occurred_at_utc, 1, 7)` or an equivalent month key
- `expense_records(status)`
- `receipt_drafts(status)`
- `receipt_drafts(expires_at_utc)`
- `receipt_drafts(confirmation_id)` unique
- `categories(key)` unique
- `categories(parent_id)`
- `payment_sources(key)` unique
- `payment_sources(type)`
- `operation_log(created_at_utc)`
- `operation_log(tool_name, status)`
- `operation_log(request_id)` unique
- `audit_events(created_at_utc)`
- `audit_events(tool_name, status)`
- `audit_events(request_id)`
- `schema_migrations(applied_at_utc)`
- `schema_version(version)`

## Constraints

Recommended constraints:
- `amount_minor > 0`
- currency normalized to uppercase 3-letter code
- `currency_exponent` in a safe integer range
- category/payment source keys unique and non-empty
- status columns use `CHECK` constraints instead of free text
- JSON columns use `CHECK (json_valid(...))` when JSON1 is available
- foreign keys enabled and enforced
- `receipt_draft_id` nullable because drafts may be absent for manual entry
- no raw SQL or query text columns are introduced

## Migration Strategy

Design only, not implemented in this run.

Recommended strategy:
- forward-only migrations;
- one migration id per schema change;
- idempotent bootstrap checks;
- `schema_version` as the current pointer;
- `schema_migrations` as the append-only history;
- no destructive migration without explicit backup and review;
- runtime bootstrap should refuse to apply an unknown checksum.

Practical rule:
- a bootstrapper may create the database and apply migrations later;
- this docs-only run does not do that work yet.

## Audit Strategy

Principles:
- every write-capable action produces an audit record;
- every validated tool call can produce an operation log entry;
- write results are recorded as factual summaries, not free-form user text;
- actor references should be hashed or otherwise safe;
- no secrets, tokens or auth payloads are stored.

Recommended write flow:
1. validate the contract payload;
2. normalize the request;
3. write the target row or rows;
4. write the `operation_log` row;
5. write the `audit_events` row;
6. return a compact factual response to the agent.

## Privacy And Safety Rules

- The agent must not write SQL directly.
- The agent must not read raw DB rows directly.
- Deterministic storage functions own all reads and writes.
- All user-facing payloads must be sanitized before persistence.
- Telegram user ids should only be stored if needed as a safe actor reference or hash.
- Do not store bot tokens, provider credentials, raw auth files or other secrets.
- Do not store raw Telegram messages unless a future slice explicitly requires it.
- `metadata_json` is supplemental only and must never become the primary truth source.

## Relationship To Current Contracts

This schema is shaped to fit the current skeleton contracts:
- `expense_add`
- `expense_recent`
- `expense_month_summary`
- `receipt_photo_draft`
- `receipt_manual_complete`
- `cancel_pending`
- `tool_status`

Alignment notes:
- `expense_add` maps to `expense_records` plus `operation_log` and `audit_events`.
- `expense_recent` reads from indexed `expense_records`.
- `expense_month_summary` reads from indexed `expense_records` and does not need a cache table in v1.
- `receipt_photo_draft` maps to `receipt_drafts`.
- `receipt_manual_complete` consumes a draft and emits a final expense record.
- `cancel_pending` can cancel a draft or a pending operation depending on later storage policy.
- `tool_status` should report storage readiness from the runtime initializer, not from business logic alone.

## Next Implementation Slice Recommendation

Recommended next slice:
- `runtime_storage_initializer_proof_design`

Why:
- it is still a proof/design slice;
- it can validate the runtime root, file layout, PRAGMA policy and bootstrap checks without mutating business data;
- it keeps schema and runtime concerns separated;
- it is narrower than jumping straight to UI or Telegram integration.

Alternative next slice:
- `source_sql_migration_skeleton`

That would also be valid later, but the runtime initializer proof/design is the smallest next step that exercises the storage boundary without creating data.

## Open Questions

- Should `categories` start as a fixed seed set or remain user-extensible from day one?
- Should `payment_sources.type` include separate values for debit and credit cards?
- Should `currency_exponent` be fixed at 2 for the first runtime slice, or should the storage layer already read a currency precision map?
- Does `operation_log` need response snapshots for read-only calls, or only for write-capable operations?
- Should `cancel_pending` cancel drafts only, or also cancel pending write operations if a queue is later introduced?
- Should monthly summaries later become cached rows or remain computed views?
