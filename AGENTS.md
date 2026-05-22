# AGENTS.md для учебного проекта OpenScript Agent Lab

## Назначение

Этот файл в `student-kit` является шаблоном правил для Codex.

`student-kit` repo - только стартовый набор документов, правил, шаблонов и заготовок.
Student-kit repo - только стартовый набор.
Рабочий repo - личный проект ученика на его сервере.

При создании проекта ученика этот файл должен быть скопирован в корень личного проекта как `AGENTS.md`.
После этого Codex работает из корня личного проекта ученика.

Если Codex находится в `student-kit` repo и получает задачу разработки проекта ученика, нужно STOP.
В `student-kit` можно работать только в задачах обновления самого учебного комплекта.

После bootstrap главным рабочим файлом становится именно `<STUDENT_PROJECT_ROOT>/AGENTS.md`.
`rules/codex/AGENTS.md` внутри `student-kit` остаётся только шаблоном для копирования.

## Главный режим работы Codex

1. Codex работает только по prompt от ChatGPT.
2. Один run = одна задача.
3. Ученик не проектирует задачу сам.
4. Если задача неясна, нужно STOP.
5. Если prompt противоречит этому файлу, нужно STOP и сообщить конфликт.
6. Перед fix нужен proof/current state.
7. Не гадать, если факт не доказан.
8. Не делать broad refactor, если задача этого не просит.

## Перед началом каждого run

1. Убедиться, что Codex находится в правильном repo.
2. Если задача про проект ученика, в корне должен быть `AGENTS.md`.
3. Прочитать `AGENTS.md` перед работой.
4. Проверить `git status` и понять, что уже изменено.
5. Проверить нужные документы и scope задачи.
6. Не начинать fix без proof/current state.
7. Если задача требует работы в `student-kit` как в рабочем repo проекта ученика, нужно STOP.
8. Если нужен public proof, сначала доказать фактический текущий state, потом менять.

## Seed-only workflow student-kit

`student-kit` скачивается как источник стартовых документов.
Student-kit repo - только seed/source документов.

Дальше:

1. все нужные файлы копируются в личный repo ученика;
2. `rules/codex/AGENTS.md` копируется в `<STUDENT_PROJECT_ROOT>/AGENTS.md`;
3. commit/push идут в личный repo ученика;
4. `student-kit` не используется как рабочий repo проекта ученика;
5. изменения в `student-kit` разрешены только в docs-maintenance задачах для самого `student-kit`.

## Секреты

Не читать и не печатать:

- `.env`;
- `auth.json`;
- tokens;
- API keys;
- Telegram bot token;
- private SSH keys;
- runtime secret files.

Private key никогда не печатать.
Public deploy key можно печатать только если prompt явно просит создать deploy key.
Токены не просить и не использовать без отдельного разрешения.

## Git и source of truth

Source живёт в git.
Runtime отдельно.

Не считать runtime-only fix финалом.
Не трогать unrelated dirty files.
Commit/push только когда prompt требует.
Отчёт должен показывать `git status` before/after.
Stage только файлы в разрешённом scope.
Не коммитить случайные изменения из соседних задач.
Если `git status` содержит неожиданное, не объяснённое изменение, нужно STOP.

## Адреса

Localhost/127.0.0.1 допустимы только для внутренней проверки Codex.
User-facing URL только:

- `http://<SERVER_PUBLIC_IP>/<PATH>`
- `http://<SERVER_PUBLIC_IP>:<PORT>/<PATH>`
- `https://<STUDENT_DOMAIN>/<PATH>`

Для `/project-structure/` использовать только шаблоны:

- `http://<SERVER_PUBLIC_IP>/project-structure/`
- `http://<SERVER_PUBLIC_IP>:<PORT>/project-structure/`

Не hardcode IP тестового сервера.

## Hermes-only agents

Агент рабочий только через Hermes.

Обязательный путь:

`agent package -> validate -> apply to Hermes runtime profile -> reply through Hermes`

Запрещено:

- direct backend reply;
- fake/template reply;
- provider call мимо Hermes;
- hardcoded one agent.

## Agent package

Агент должен быть package, а не один prompt.

Обязательные части:

- `manifest.json`;
- `SOUL.md`;
- `rules.md`;
- `examples.md`;
- `README.md`;
- `provider.defaults.json`;
- `skills/`;
- `tools.json`.

Package без обязательных частей не готов.

## Telegram

Telegram - канал общения, не business tool.

Allowlist проверять по `from.id` / `user_id`.
`chat.id` использовать только для доставки ответа.
Telegram proof должен доказывать final bot state.
Telegram не должен обходить Hermes.

## Tools и finance

Tools идут через registry/binding/tools.json.
Опасные tools blocked by default.
Finance DB writes only through deterministic financial tools.
LLM/Hermes не пишет БД напрямую.
Receipt confirmation только после подтверждения пользователя.

## Voice/photo

Voice -> transcript -> same text path.
Voice не отдельная бизнес-логика.

Photo receipt -> draft -> confirmation -> DB.
Не смешивать voice/photo/text/DB в одном fix.

## Документация

Docs-update run только по prompt ChatGPT.
Обновлять только явно указанные документы.
Не обновлять docs по памяти.
Использовать факты: отчёты Codex, `git status`, текущие файлы.

Документы состояния:

- roadmap;
- ТЗ;
- module map;
- project snapshot;
- student dialogue context;
- current status, если он есть.

## Формат отчёта

Всегда между:

`CHATGPT_REPORT_BEGIN`

`CHATGPT_REPORT_END`

## STATUS

- SUCCESS - задача выполнена и проверена;
- STOP - не хватает фактов или есть риск, изменения не продолжать;
- FAIL - попытка была, но проверка/команда/изменение не прошли.

## Обязательные поля отчёта

- RUN_ID;
- STATUS;
- WHAT_CHANGED;
- FILES_CHANGED;
- CHECKS;
- GIT;
- SAFETY;
- NEXT.

Для agent runs добавлять Hermes fields.
Для Telegram runs добавлять `user_id` / `chat_id` fields.
Для finance runs добавлять DB/tool fields.
