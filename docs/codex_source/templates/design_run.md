# Шаблон design-run

## RUN_ID
`<RUN_ID>`

## TASK_TYPE
`design-run`

## REQUIRED_SOURCE_OF_TRUTH
- `docs/codex_source/index.yaml`
- `<exact paths from task card>`

## RUNTIME_BASELINE
- repo: `<repo path>`
- branch: `<branch>`
- head_before: `<commit>`
- expected_head: `<commit>`

## ONE TASK
- Проектировать только в рамках заданных документов.

## ALLOWED
- Описывать структуру и контракты.
- Составлять карту зависимостей.

## FORBIDDEN
- Нельзя писать application code.
- Нельзя заменять vendor docs догадками.

## STOP CONDITIONS
- Любой required doc имеет status `stub`.
- Невозможно зафиксировать контракт без missing docs.

## ACCEPTANCE
- Дизайн опирается на exact paths.

## REPORT FORMAT
- RUN_ID
- RESULT
- DECISIONS
- REQUIRED_DOCS
- MISSING_DOCS

