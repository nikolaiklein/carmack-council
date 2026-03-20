# The Carmack Council — Python / Telegram Fork

> Форк [SamJHudson01/Carmack-Council](https://github.com/SamJHudson01/Carmack-Council), адаптированный под стек **Python 3.11+ / FastAPI / python-telegram-bot / SQLAlchemy / Pydantic v2 / pytest**.

Мультиагентный фреймворк разработки для [Claude Code](https://docs.anthropic.com/en/docs/claude-code). Философия Джона Кармака: простота важнее хитрости, конкретика важнее абстракции, экономия важнее эстетики.

## Стек

| Слой | Технология |
|------|-----------|
| Язык | Python 3.11+ (type hints, async/await) |
| HTTP | FastAPI |
| Бот | python-telegram-bot |
| Валидация | Pydantic v2 |
| ORM | SQLAlchemy async |
| БД | SQLite / Firestore |
| Авторизация | Telegram user ID |
| UI | Telegram inline keyboards |
| Деплой | Docker, Cloud Run |
| AI | Gemini via LiteLLM |
| Тесты | pytest, pytest-asyncio, httpx |
| Линтинг | ruff, pyright |

## Совет экспертов

Совет возглавляет Джон Кармак. 10 доменных экспертов:

| Эксперт | Домен | Справочник |
|---------|-------|-----------|
| Troy Hunt | Безопасность | `security.md` |
| Martin Fowler | Рефакторинг / Структура | `refactoring.md` |
| Telegram UX Expert | Качество UX бота | `quality-frontend.md` |
| Backend/Python Expert | Качество бэкенда | `quality-backend.md` |
| Brandur Leach | Качество БД | `quality-postgres.md` |
| Docker/Deploy Expert | Деплой и инфраструктура | — |
| Simon Willison | LLM-пайплайны | `quality-llm.md` |
| Karri Saarinen | Качество UI | `quality-ui.md` |
| Vitaly Friedman | Качество UX | `quality-ux.md` |
| Kent Beck | Качество тестов | `quality-testing.md` |

## Рабочий процесс

```
/spec-writer  →  /council-plan  →  /council-implement  →  /council-review
    ↑                                                           |
    └───────────────────────────────────────────────────────────┘
```

**+ `/test-architect`** — используется на любом этапе (аудит, спецификация или исправление тестов).

| Скилл | Команда | Что делает |
|-------|---------|-----------|
| Spec Writer | `/spec-writer` | Спецификация: Job Stories, Gherkin-критерии, три уровня границ |
| Council Plan | `/council-plan` | 10 экспертов планируют фичу параллельно (без кода) |
| Council Implement | `/council-implement` | Выполняет план задача за задачей, проверяя после каждой |
| Council Review | `/council-review` | 10 экспертов ревьюят код в параллельных подагентах (200k контекст каждый) |
| Test Architect | `/test-architect` | Аудит тестов по 11 принципам Бека, спецификация тестов, исправление |

## Установка

### Быстрая установка (готовые пакеты)

Скачай `.skill` файлы из папки [`dist/`](dist/) и установи в Claude Code:

```bash
# Скачай репозиторий
git clone https://github.com/nikolaiklein/carmack-council.git
cd carmack-council

# Установи нужные скиллы (можно все или по отдельности)
claude skill install dist/spec-writer.skill
claude skill install dist/council-plan.skill
claude skill install dist/council-implement.skill
claude skill install dist/council-review.skill
claude skill install dist/test-architect.skill
```

### Из исходников

```bash
git clone https://github.com/nikolaiklein/carmack-council.git
cd carmack-council
chmod +x scripts/build.sh
./scripts/build.sh

# Затем установи собранные .skill файлы
claude skill install dist/spec-writer.skill
claude skill install dist/council-plan.skill
claude skill install dist/council-implement.skill
claude skill install dist/council-review.skill
claude skill install dist/test-architect.skill
```

### Требования

- [Claude Code](https://docs.anthropic.com/en/docs/claude-code) с поддержкой скиллов
- Python 3.6+ (для скрипта сборки)

## Структура репозитория

```
carmack-council/
├── README.md
├── STACK.md              # Все стековые допущения
├── LICENSE               # MIT
├── references/           # Справочные документы (single source of truth)
│   ├── security.md
│   ├── quality-backend.md
│   ├── quality-frontend.md
│   ├── quality-postgres.md
│   ├── quality-testing.md
│   ├── quality-llm.md
│   ├── quality-ui.md
│   ├── quality-ux.md
│   ├── refactoring.md
│   └── spec-writer/
├── skills/               # Исходники скиллов
│   ├── council-review/
│   ├── council-plan/
│   ├── council-implement/
│   ├── spec-writer/
│   └── test-architect/
├── scripts/              # Сборка
│   ├── build.sh
│   └── package_skill.py
└── dist/                 # Собранные .skill пакеты
```

## conventions.md

Совет учится. После ревью он предлагает паттерны для `conventions.md` в корне твоего проекта. Все три downstream-скилла (plan, implement, review) читают этот файл — принятые конвенции не будут повторно флагнуты. С каждым ревью совет знает твою кодовую базу лучше.

## Отличия от оригинала

Этот форк адаптирован с Next.js/TypeScript → **Python/FastAPI/Telegram**:
- Заменены эксперты: Kent C. Dodds → Telegram UX Expert, Matteo Collina → Backend/Python Expert, Vercel → Docker/Deploy Expert
- Все подагентные промпты переписаны под Python-стек
- Автопроверки: `tsc/eslint/vitest` → `ruff/pyright/pytest`
- Справочники `quality-backend.md`, `quality-testing.md` адаптированы
- Добавлен 5-й скилл `test-architect` (из оригинала), адаптирован под pytest

Оригинал: [SamJHudson01/Carmack-Council](https://github.com/SamJHudson01/Carmack-Council)

## Лицензия

MIT — см. [LICENSE](LICENSE).
