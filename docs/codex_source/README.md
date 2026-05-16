# Codex source-of-truth pack

Этот каталог является репозиторным источником истины для будущих Codex prompt'ов.

Что здесь важно:
- Task card должен указывать точные пути к нужным документам.
- Roadmap, continuity/handoff и ТЗ не считаются заменой vendor- или project-документации.
- Vendor docs и project docs разделены намеренно.
- Если task card требует vendor docs, а они имеют статус `stub`, будущий fix-run обязан остановиться с `STOP_DOCS_MISSING`.
- Это не application code и не место для бизнес-логики.

Правило использования:
- Сначала читается `docs/codex_source/index.yaml`.
- Потом читаются только пути, указанные в task card.
- Только после этого можно принимать решение о запуске run-класса.

Статусы документов:
- `stub` - каркас, нельзя использовать как substitute.
- `extracted` - документ заполнен из source.
- `verified` - документ проверен и пригоден как source-of-truth.
- `deprecated` - документ сохранён только для истории.

Пока Hermes/Telegram/TZ/roadmap docs не извлечены, они остаются stub и не могут подменять vendor docs для fix-run.

