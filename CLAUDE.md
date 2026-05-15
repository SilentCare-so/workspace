# OdeCare Workspace

## Система

OdeCare IOT — платформа удалённого мониторинга пациентов. Устройства → MQTT → backend → web/mobile/landing.
GitHub org: https://github.com/OdeCare/

## Репо

| Репо | Назначение | Slug |
|------|-----------|------|
| odecare-backend | API сервер, бизнес-логика, MQTT, устройства | OdeCare/odecare-backend |
| odecare-web | Dashboard SPA (odecare.com/app) | OdeCare/odecare-web |
| odecare-mobile | iOS/Android приложение | OdeCare/odecare-mobile |
| odecare-landing | Маркетинговый сайт (odecare.com/) | OdeCare/odecare-landing |
| odecare-platform | Инфраструктура, docker-compose, telegram-bot | OdeCare/odecare-platform |
| ec-supplier-agent | Локальный инструмент работы с поставщиками | OdeCare/ec-supplier-agent |

## Общие правила

IMPORTANT: Отвечать на русском, кроме кода и коммитов.

IMPORTANT: Никогда не использовать `gh` CLI. Для всех операций с GitHub — только MCP (`mcp__github__*`).

IMPORTANT: Никогда не добавлять строку "Co-Authored-By" в коммиты.

IMPORTANT: Формат коммитов — conventional commits (`feat:`, `fix:`, `chore:` и т.д.).

IMPORTANT: Pre-commit хуки могут переформатировать файлы. Если коммит упал — re-stage изменения и повторить.

IMPORTANT: Никогда не писать DELETE/DROP/TRUNCATE на реальных данных без явного разрешения от Никиты. При дедупликации или очистке — использовать UPDATE (обнулять поле) или переносить в архив, но не удалять строки. Если деструктивная операция неизбежна — остановиться и спросить разрешения перед написанием миграции или скрипта.

## Работа в репо

Перед началом работы в любом репо — прочитать его `CLAUDE.md` через Read:
`Read(<repo>/CLAUDE.md)` — стек, команды, специфичные ограничения.

## Принципы работы (12 правил)

**Rule 1 — Think Before Coding.** State assumptions explicitly. If uncertain, ask rather than guess. Present multiple interpretations when ambiguity exists. Push back when a simpler approach exists. Stop when confused. Name what's unclear.

**Rule 2 — Simplicity First.** Minimum code that solves the problem. Nothing speculative. No features beyond what was asked. No abstractions for single-use code. Test: would a senior engineer say this is overcomplicated? If yes, simplify.

**Rule 3 — Surgical Changes.** Touch only what you must. Clean up only your own mess. Don't "improve" adjacent code, comments, or formatting. Don't refactor what isn't broken. Match existing style.

**Rule 4 — Goal-Driven Execution.** Define success criteria. Loop until verified. Don't follow steps. Define success and iterate. Strong success criteria let you loop independently.

**Rule 5 — Use the model only for judgment calls.** Use for: classification, drafting, summarization, extraction. Do NOT use for: routing, retries, deterministic transforms. If code can answer, code answers.

**Rule 6 — Token budgets are not advisory.** Per-task: 4,000 tokens. Per-session: 30,000 tokens. If approaching budget, summarize and start fresh. Surface the breach. Do not silently overrun.

**Rule 7 — Surface conflicts, don't average them.** If two patterns contradict, pick one (more recent / more tested). Explain why. Flag the other for cleanup. Don't blend conflicting patterns.

**Rule 8 — Read before you write.** Before adding code, read exports, immediate callers, shared utilities. "Looks orthogonal" is dangerous. If unsure why code is structured a way, ask.

**Rule 9 — Tests verify intent, not just behavior.** Tests must encode WHY behavior matters, not just WHAT it does. A test that can't fail when business logic changes is wrong.

**Rule 10 — Checkpoint after every significant step.** Summarize what was done, what's verified, what's left. Don't continue from a state you can't describe back. If you lose track, stop and restate.

**Rule 11 — Match the codebase's conventions, even if you disagree.** Conformance > taste inside the codebase. If you genuinely think a convention is harmful, surface it. Don't fork silently.

**Rule 12 — Fail loud.** "Completed" is wrong if anything was skipped silently. "Tests pass" is wrong if any were skipped. Default to surfacing uncertainty, not hiding it.

## Prod сервер

**Адрес:** `193.169.239.226`
**Подключение:** `ssh -i ~/.ssh/deploy_key ubuntu@193.169.239.226`
**Рабочая директория:** `~/elder-care-iot/` (docker-compose.prod.yml, .env)
**БД (с сервера):** `docker exec -it eldercare-db psql -U eldercare -d eldercare`

### Можно делать без подтверждения

- Читать файлы (`cat .env`, `cat docker-compose.prod.yml`)
- Смотреть статус контейнеров (`docker ps`)
- Читать логи (`docker logs <container>`)
- Генерировать ключи / шифровать через `python3`
- Дописывать в `.env` новые переменные (`echo "KEY=value" >> .env`)
- Выполнять READ-only SQL-запросы (`SELECT ...`)

### Нельзя без явного подтверждения пользователя

- Перезапускать контейнеры (`docker compose up`, `docker restart`)
- Удалять данные из БД (`DELETE`, `DROP`, `TRUNCATE`)
- Запускать миграции (`alembic upgrade`)
- Удалять файлы или директории на сервере
- Менять права доступа или SSH-ключи

## Слэш-команды

- `/start` — начать задачу (определить репо, прочитать контекст, создать ветку)
- `/pr` — создать PR(s) через GitHub MCP
- `/status` — обзор открытых PR по всем репо
- `/sync` — загрузить контекст конкретного репо
