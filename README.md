# Процесс работы пайплайна

## Где посмотреть статус
Вкладка Actions в репозитории

## Описание Workflow
Pipeline состоит из двух основных задач:

### 1. lint
<div style="border-left: 2px solid #ccc; padding-left: 10px;">
Проверяет код на ошибки линтинга с помощью super-linter.

Когда запускается:
* При пушах в любые ветки, кроме main
* При pull request'ах в ветку main

Что делает:

* Загружает репозиторий
* Выполняет проверку линтинга всего проекта
* Отмечает статус проверки в UI GitHub (Checks → Lint Code) 
</div>

### 2. fix-lint-issues
<div style="border-left: 2px solid #ccc; padding-left: 10px;">
Автоматически исправляет некоторые ошибки линтинга, если возможно (с помощью black, isort, ruff).

Когда запускается:

* Всегда вместе с задачей lint

Что делает:

* Загружает код
* Исправляет возможные проблемы линтинга (только Python)
* Если это pull request, делает commit с исправлениями в ту же ветку
</div>

## Как отслеживать статус CI

1. Перейдите во вкладку Pull Requests и выберите нужный PR.
2. Вверху или снизу страницы будет отображён CI-статус:

    * Успешно — линтинг прошёл
    
    * Ошибка — найдены ошибки линтинга

3. Кликните на Details рядом с задачей Lint Code, чтобы посмотреть лог.
4. Если были исправления, они автоматически появятся как новый commit в pull request.
## Что поддерживается

Проверка:
* Python (black, isort, ruff)
* Можно включить другие линтеры, изменив переменные окружения в lint-задаче

Автоисправление:
* black — автоформатирование Python-кода
* isort — сортировка импортов
* ruff — быстрые линт-фиксы