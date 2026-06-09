# Codex Toolchain Guard Design

STATUS: DESIGN_ONLY

This document defines the future Codex Toolchain Guard for Agent Lab.
It is design-only and does not implement runtime behavior.

## Purpose

Prevent regressions where Codex-backed features break because one of the following changes:

- the resolved `codex` binary changes
- the installed Codex version changes
- the feature list changes
- the invocation contract changes
- auth becomes stale or mismatched
- the last known good image-generation path is no longer valid

The immediate motivation is the YouTube post-draft image-generation regression that was resolved by restoring the prompt-based `$imagegen` path and removing the obsolete feature-flag invocation.

## Scope

The guard is a future read-only probe and policy layer.

It should:

- observe toolchain state
- classify whether the environment is image-generation capable
- expose safe status to admin UI and backend preflight
- remember the last successful Codex image-generation shape
- support controlled update flows only when explicitly enabled

It must not:

- read or print secrets
- mutate auth files
- silently update Codex
- own image generation itself
- own Telegram dispatch
- own provider selection

## Core probe dimensions

### 1. Codex binary identity

Probe and report:

- resolved `codex` path
- all available `codex` binaries on `PATH`
- active `PATH` winner
- safe package source metadata if available
- symlink target if available

The guard should detect path drift, multiple competing binaries, and a resolved binary that differs from the last successful run.

### 2. Codex version

Probe and report:

- current `codex --version`
- version used at last successful image generation
- last known good version
- version drift from last good

The guard should treat version drift as informative, not automatically fatal, unless coupled with a failing feature or contract check.

### 3. Feature list

Probe and report:

- `codex features list`
- whether `image_generation` is present
- whether it is stable / enabled / otherwise categorized
- a safe missing-feature category

The guard should distinguish:

- feature absent
- feature present but unsupported by the current invocation contract
- feature present and contract-compatible

### 4. Invocation contract

Probe and report:

- the supported command shape for image generation
- whether `$imagegen` in the prompt is the current supported contract
- whether legacy feature flags are forbidden
- the last known good invocation contract
- the exact safe command-shape probe result when possible

The guard should preserve the distinction between:

- feature capability
- command-line contract
- prompt contract

Those are not the same thing.

### 5. Auth readiness

Probe and report only safe readiness signals:

- whether auth is live and usable
- whether the current binary can perform a live Codex action
- whether the environment appears authenticated enough for the current command path

It must not:

- read `/root/.codex/auth.json`
- print tokens
- dump raw credential material

The guard should distinguish:

- auth file exists
- auth imported
- live auth works
- live image generation works

### 6. Runtime status

The guard should retain safe status fields such as:

- `last_successful_imagegen_at`
- `last_successful_codex_version`
- `last_successful_invocation_contract`
- `last_failure_kind`
- `last_failure_safe_tail`
- `requires_toolchain_update`
- `requires_reauth`
- `requires_manual_action`

These fields are for diagnosis and safe admin visibility only.

## Proposed status model

The future status object should be stable, serializable, and safe to expose through admin APIs.

Recommended fields:

- `codex_path`
- `codex_version`
- `codex_paths_found`
- `codex_features`
- `imagegen_capable`
- `invocation_contract_ok`
- `auth_active`
- `last_good_version`
- `last_successful_imagegen_at`
- `last_successful_invocation_contract`
- `last_failure_kind`
- `last_failure_safe_tail`
- `requires_toolchain_update`
- `requires_reauth`
- `requires_manual_action`
- `last_checked_at`

All free-text fields must be redacted or truncated to avoid secret leakage.

## Admin/UI surface

The admin UI should display only safe status.

Recommended visible fields:

- `codex_path`
- `codex_version`
- `imagegen_capable`
- `invocation_contract_ok`
- `auth_active`
- `last_good_version`
- `last_successful_imagegen_at`
- `requires_toolchain_update`
- `requires_reauth`
- `last_checked_at`

The UI should not expose raw secrets, tokens, or raw auth blobs.

## Controlled auto-update policy

The default policy should be no silent auto-update.

Use an explicit config flag such as:

- `CODEX_AUTO_UPDATE_ENABLED=false`

Controlled update flow requirements:

1. no update while a generation job is running
2. capture a pre-update snapshot
3. update only through an approved official mechanism
4. re-check version, features, invocation contract, and auth readiness after update
5. run a safe smoke or controlled project retry after update
6. if post-checks fail, mark rollback/manual action required

Pre-update snapshot should include:

- path
- version
- features
- invocation contract
- auth readiness
- timestamp

Post-update checks should include:

- version check
- features check
- prompt/command contract check
- auth live probe
- safe imagegen smoke or controlled retry

The update flow must be explicit and reversible.

## Responsibility boundaries

Future modules should remain narrow:

- one future module for toolchain probing
- one future module for guard status/result modeling if needed
- admin UI only consumes safe status
- image-generation backend consumes guard result for preflight only
- auth import/adopt remains separate

The guard must not become a toolchain manager, auth importer, or provider switch.

## Future implementation slices

Recommended staged implementation order:

A. Proof-only inventory of current Codex toolchain
- enumerate binaries
- record versions
- record features
- record invocation contract
- record safe auth readiness

B. Add read-only guard probe module
- encapsulate binary/version/features/contract probes
- return a safe status object

C. Expose safe admin status
- add read-only endpoints / UI status
- show only redacted state

D. Connect imagegen preflight to guard result
- gate image-generation attempts on safe guard status
- preserve retryable failure semantics

E. Controlled update design proof
- design explicit update workflow and rollback metadata
- keep it off by default

F. Optional update implementation only after explicit user approval
- only if future evidence proves it is needed

## Current stop-point

Current image generation and moderation refresh are already working again.

The next open design problem is the future Codex Toolchain Guard, not another image-generation fix.
