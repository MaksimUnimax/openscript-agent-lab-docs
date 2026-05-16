# Шаблон proof-run

## RUN_ID
`<RUN_ID>`

## TASK_TYPE
`proof-run`

## REQUIRED_SOURCE_OF_TRUTH
- `docs/codex_source/index.yaml`
- `<exact paths from task card>`

## RUNTIME_BASELINE
- repo: `<repo path>`
- branch: `<branch>`
- head_before: `<commit>`
- expected_head: `<commit>`
- dirty_scope: `<allowed or blocked>`

## ONE TASK
- Одна проверяемая гипотеза.
- Один результат.

## ALLOWED
- Читать только exact paths из task card.
- Проводить только доказательство заявленного поведения.

## FORBIDDEN
- Нельзя подменять vendor docs памятью.
- Нельзя расширять scope.
- Нельзя использовать roadmap как substitute.

## STOP CONDITIONS
- Любой required doc имеет status `stub`.
- Базовый commit не совпадает.
- Для доказательства нужен неразрешённый scope.

## ACCEPTANCE
- Факты подтверждены.
- Источник каждого факта ясен.

## REPORT FORMAT
- RUN_ID
- RESULT
- SOURCES
- FACTS
- STOP_IF_ANY

