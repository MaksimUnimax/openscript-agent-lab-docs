# Financial Agent Business Tool

STATUS: IMPORTED_DESIGN_PROPOSED
SOURCE_KIND: docs-only product correction
DATE: 2026-05-17

## Purpose

Define the deterministic business layer for the financial agent line.

This is a business tool package, not a raw database and not an LLM-owned SQL layer.

The tool must own:
- safe reads and writes;
- calculations;
- receipt ingestion;
- reports and summaries;
- audit events;
- compact factual results returned to the agent.

The agent may explain the result, but the agent must not write SQL directly.

## Business Layer From ТЗ

The current technical spec already requires that money/date/report facts are handled by deterministic code, not by the LLM.

For the financial line this means:
- the agent interprets the user intent;
- the tool performs deterministic operations;
- the tool returns compact facts;
- the agent formats the answer.

## Financial Domain Model

Core entities to design around:

- `expense_record`
- `receipt_draft`
- `category`
- `account` or `payment_source` if needed
- `transaction_type`:
  - `expense` first
  - `income` later optional
- `report`
- `month_summary`
- `audit_event`
- `user_confirmation`
- `tool_request`
- `tool_response`

The model should remain extensible without turning it into a general Agent Farm database.

## Deterministic Scripts And Tools

The following tool family is proposed for the financial line:

- `expense_add`
- `expense_recent`
- `expense_month_summary`
- `receipt_photo_draft`
- `receipt_manual_complete`
- `cancel_pending`
- `tool_status`
- `readiness`

These are deterministic business actions, not prompt-only behaviors.

## Tool Contracts

Example request/response contracts:

```json
{
  "tool": "expense_add",
  "request": {
    "user_id": 286579139,
    "amount": "1250.00",
    "currency": "RUB",
    "category": "transport",
    "note": "Taxi to office",
    "occurred_at": "2026-05-17T09:00:00+03:00",
    "source": "telegram",
    "receipt_draft_id": "optional-draft-id"
  },
  "response": {
    "ok": true,
    "expense_id": "exp_20260517_001",
    "normalized": true,
    "audit_event_id": "aud_20260517_001",
    "warnings": []
  }
}
```

```json
{
  "tool": "expense_recent",
  "request": {
    "user_id": 286579139,
    "limit": 10
  },
  "response": {
    "ok": true,
    "items": [],
    "summary": {
      "count": 0,
      "total": "0.00",
      "currency": "RUB"
    }
  }
}
```

```json
{
  "tool": "expense_month_summary",
  "request": {
    "user_id": 286579139,
    "month": "2026-05",
    "currency": "RUB"
  },
  "response": {
    "ok": true,
    "summary": {
      "income_total": "0.00",
      "expense_total": "0.00",
      "net_total": "0.00"
    },
    "by_category": []
  }
}
```

```json
{
  "tool": "receipt_photo_draft",
  "request": {
    "user_id": 286579139,
    "receipt_file_id": "telegram-file-id",
    "source": "telegram"
  },
  "response": {
    "ok": true,
    "draft_id": "draft_20260517_001",
    "status": "pending_confirmation",
    "fields": {
      "merchant": null,
      "amount": null,
      "currency": "RUB"
    }
  }
}
```

```json
{
  "tool": "receipt_manual_complete",
  "request": {
    "user_id": 286579139,
    "draft_id": "draft_20260517_001",
    "confirm": true,
    "amount": "1250.00",
    "currency": "RUB",
    "category": "transport"
  },
  "response": {
    "ok": true,
    "expense_id": "exp_20260517_001",
    "audit_event_id": "aud_20260517_002"
  }
}
```

```json
{
  "tool": "cancel_pending",
  "request": {
    "user_id": 286579139,
    "draft_id": "draft_20260517_001"
  },
  "response": {
    "ok": true,
    "status": "cancelled"
  }
}
```

```json
{
  "tool": "tool_status",
  "request": {},
  "response": {
    "ok": true,
    "ready": false,
    "reason": "storage_not_initialized"
  }
}
```

## Receipt Draft And Confirmation Flow

Suggested flow:

1. user sends a receipt/photo/voice note in the financial flow;
2. the tool creates a draft;
3. the tool extracts or normalizes fields where safe;
4. the user confirms or corrects the draft;
5. the tool writes the final expense record;
6. the tool records an audit event;
7. the agent returns a compact factual summary.

This keeps confirmation explicit and avoids silent writes.

## Reports And Summaries

The financial tool should support:
- recent expenses;
- monthly summaries;
- category breakdowns;
- optional income later;
- operator-facing audit snapshots.

Outputs should remain factual and compact.

## Audit Model

Every write-capable action should create or update an audit event with:
- timestamp;
- user_id;
- tool name;
- request summary;
- result status;
- resource ids;
- safe failure reason if any.

Audit logs must not store secrets or raw auth data.

## Storage Proposal

Proposed runtime storage root:
- `/var/lib/openscript-agent-lab/fin-instrument/`

Proposed contents:
- `finance.sqlite3`
- `drafts/`
- `receipts/`
- `audit/`
- `status.json`
- optional `exports/`

Rules:
- deterministic scripts own storage reads/writes;
- agents do not write SQL directly;
- runtime data stays out of git;
- secrets stay out of git;
- public docs describe contracts, not live runtime values.

## Safety Rules

- agent must not write SQL
- agent must not mutate the DB directly
- agent must not invent totals
- agent must not bypass scripts
- receipt confirmation must remain explicit where needed
- no secrets in git
- no model call in tests
- no uncontrolled runtime writes
- no cross-contamination with Agent Farm or Telegram Publisher

## Future Implementation Slices

- Slice A: proof/design docs plus task card
- Slice B: source-only financial tool contracts and no-op scripts
- Slice C: SQLite schema and migration design, no live mutation
- Slice D: safe runtime storage initializer
- Slice E: deterministic `expense_add` / `expense_recent` / `expense_month_summary` scripts
- Slice F: Fin Instrument UI status/read-only surface
- Slice G: Telegram/voice integration to the financial tool with confirmation
- Slice H: old expense-bot extraction/refactor only after separate proof

## Open Questions

- what currency/precision rules should the tool enforce;
- how to normalize categories without overfitting;
- whether receipts need OCR in phase one;
- whether a single SQLite file is enough or whether receipts/artifacts need separate storage;
- whether multi-account support is required now or later;
- what minimal operator status should be visible before implementation starts.
