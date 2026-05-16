# Шаблон docs-extraction-run

## RUN_ID
`<RUN_ID>`

## TASK_TYPE
`docs-extraction-run`

## REQUIRED_SOURCE_OF_TRUTH
- `docs/codex_source/index.yaml`
- `docs/codex_source/vendor/*`
- `docs/codex_source/project/*`

## RUNTIME_BASELINE
- repo: `<repo path>`
- branch: `<branch>`
- head_before: `<commit>`

## ONE TASK
- Извлечь и зафиксировать факты из источников без смешивания с application code.

## ALLOWED
- Создавать/обновлять docs only.
- Заполнять extracted docs.

## FORBIDDEN
- Нельзя писать продуктовый код.
- Нельзя подменять source memory.

## STOP CONDITIONS
- Источник недоступен.
- Факт нельзя подтвердить.

## ACCEPTANCE
- docs marked extracted/verified.

## REPORT FORMAT
- RUN_ID
- RESULT
- SOURCES_READ
- FACTS_EXTRACTED
- FACTS_NOT_FOUND
- NEXT_STEPS

