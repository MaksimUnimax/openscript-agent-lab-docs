# YouTube search tool

Эта инструкция описывает использование `youtube.search_candidates` как агентского инструмента.
Инструмент доступен только если у агента есть явное разрешение в `tools.json`.

## Правила использования

- Используй инструмент только когда пользователь просит искать YouTube-видео, собирать кандидатов или показать результат поиска.
- Инструмент использует сохранённый UI-профиль поиска.
- Не придумывай raw query, language, region или provider parameters вручную.
- В первой версии допускаются только saved profile, bounded `target_new_candidates` override и bounded `preview_limit`, если это явно безопасно и нужно.
- После поиска инструмент может дополнительно собрать полные описания для уже сохранённых кандидатов.
- В ответе опирайся на result summary, candidate preview и `description_full_length`.
- Не утверждай, что собирал субтитры, занимался ranking, editorial evaluation или публикацией.
- Не используй YouTube Data API, OAuth, cookies, proxies, yt-dlp, pytubefix или download/stream paths.
- Skill сам по себе не выдаёт permission.
- После изменения source package может понадобиться отдельное применение в Hermes runtime.
