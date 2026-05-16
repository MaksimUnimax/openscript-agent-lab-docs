# Шаблон limited-fix-run

## RUN_ID
`<RUN_ID>`

## TASK_TYPE
`limited-fix-run`

## REQUIRED_SOURCE_OF_TRUTH
- `docs/codex_source/index.yaml`
- `<exact paths from task card>`

## RUNTIME_BASELINE
- repo: `<repo path>`
- branch: `<branch>`
- head_before: `<commit>`

## ONE TASK
- Один локальный фикс без расширения scope.

## ALLOWED
- Менять только разрешённые файлы.
- Использовать только разрешённые источники.

## FORBIDDEN
- Нельзя трогать unrelated code.
- Нельзя использовать substitute docs.

## STOP CONDITIONS
- Любой required doc status `stub`.
- Required baseline не совпадает.

## ACCEPTANCE
- Поведение исправлено.
- Тесты/проверки проходят.

## REPORT FORMAT
- RUN_ID
- RESULT
- FILES_CHANGED
- TESTS
- STOP_CONDITIONS

