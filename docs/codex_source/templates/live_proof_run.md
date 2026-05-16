# Шаблон live-proof-run

## RUN_ID
`<RUN_ID>`

## TASK_TYPE
`live-proof-run`

## REQUIRED_SOURCE_OF_TRUTH
- `docs/codex_source/index.yaml`
- `<exact paths from task card>`

## RUNTIME_BASELINE
- repo: `<repo path>`
- branch: `<branch>`
- service: `<service name>`
- healthz: `<expected status>`

## ONE TASK
- Подтвердить поведение на живом runtime без расширения scope.

## ALLOWED
- Читать live state.
- Проверять health.

## FORBIDDEN
- Нельзя менять application code.
- Нельзя подменять vendor docs памятью.

## STOP CONDITIONS
- required doc status `stub`.
- service unhealthy.

## ACCEPTANCE
- live proof получен.

## REPORT FORMAT
- RUN_ID
- RESULT
- LIVE_CHECKS
- SOURCES

