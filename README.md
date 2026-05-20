# context-builder

AI-agent skill, который собирает в проекте папку `context/` — короткую базу знаний для любого кодового агента.

Он нужен, чтобы агент не начинал каждый новый чат с нуля и не спрашивал заново: кто аудитория, что в MVP, какой стек, какие ограничения и куда двигаться дальше. Вместо этого агент читает `context/INDEX.md`, открывает нужный файл и работает в рамках уже зафиксированных решений.

Скилл фиксирует три слоя проекта:

```text
context/
├── INDEX.md
├── idea/           # замысел, аудитория, MVP, принципы, риски
├── architecture/   # система, данные, стек, безопасность, roadmap
└── business/       # продукты, цены, цели, экономика, маркетинг, бренд
```

Для Claude Code скилл также добавляет в `CLAUDE.md` секцию `Project context` со ссылкой на `context/INDEX.md`. Для других агентов `context/INDEX.md` остаётся точкой входа.

## Режимы

- **Mode A:** новый проект — интервью по фазам `idea -> architecture -> business`.
- **Mode B:** существующий проект — сначала анализ README, пакетов, кода и тестов, потом вопросы только по пробелам.

Режим выбирается автоматически и подтверждается с пользователем.

## Установка

Для Claude Code скопируй папку `context-builder/`:

- глобально: `~/.claude/skills/context-builder/`
- локально: `<project>/.claude/skills/context-builder/`

Для других агентов используй `context-builder/SKILL.md` и файлы из `context-builder/stages/` как инструкцию: точка входа для результата всегда `context/INDEX.md`.

## Команды

| Задача | Пример |
|---|---|
| Собрать context | `собери context`, `build project context` |
| Обновить фазу | `обнови idea`, `обнови architecture`, `обнови business` |
| Обновить блок | `обнови context/business/economics/` |
| Добавить живую метрику | `добавь LIVE-метрику` |
| Проверить business-контекст | `аудит business` |

## Структура репозитория

```text
context-builder/
├── SKILL.md
└── stages/
    ├── idea.md
    ├── architecture.md
    └── business.md
```
