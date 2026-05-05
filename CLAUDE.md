# SilentCare Workspace

## Система

HomeCare IoT — платформа удалённого мониторинга пациентов. Устройства → MQTT → backend → web/mobile/landing.
GitHub org: https://github.com/SilentCare-so/

## Репо

| Репо | Назначение | Slug |
|------|-----------|------|
| homecare-backend | API сервер, бизнес-логика, MQTT, устройства | SilentCare-so/homecare-backend |
| homecare-web | Dashboard SPA (silentcare.co/app) | SilentCare-so/homecare-web |
| homecare-mobile | iOS/Android приложение | SilentCare-so/homecare-mobile |
| homecare-landing | Маркетинговый сайт (silentcare.co/) | SilentCare-so/homecare-landing |
| homecare-platform | Инфраструктура, docker-compose, telegram-bot | SilentCare-so/homecare-platform |
| ec-supplier-agent | Локальный инструмент работы с поставщиками | SilentCare-so/ec-supplier-agent |

## Общие правила

IMPORTANT: Отвечать на русском, кроме кода и коммитов.

IMPORTANT: Никогда не использовать `gh` CLI. Для всех операций с GitHub — только MCP (`mcp__github__*`).

IMPORTANT: Никогда не добавлять строку "Co-Authored-By" в коммиты.

IMPORTANT: Формат коммитов — conventional commits (`feat:`, `fix:`, `chore:` и т.д.).

IMPORTANT: Pre-commit хуки могут переформатировать файлы. Если коммит упал — re-stage изменения и повторить.

## Работа в репо

Перед началом работы в любом репо — прочитать его `CLAUDE.md` через Read:
`Read(<repo>/CLAUDE.md)` — стек, команды, специфичные ограничения.

## Принципы работы

- Подумать перед кодингом, сформулировать что значит "готово"
- Минимум кода решающего задачу
- Только хирургические правки — только то что просили

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
