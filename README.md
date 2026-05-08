# OdeCare Workspace

IoT-платформа удалённого мониторинга пациентов. Устройства → MQTT → backend → web/mobile/landing.

**Сайт:** [odecare.com](https://odecare.com) · **GitHub org:** [github.com/OdeCare](https://github.com/OdeCare)

---

## Репозитории

| Репо | Назначение | Стек |
|------|-----------|------|
| [odecare-backend](https://github.com/OdeCare/odecare-backend) | API сервер, бизнес-логика, MQTT, устройства | Python, FastAPI, PostgreSQL, Redis |
| [odecare-web](https://github.com/OdeCare/odecare-web) | Dashboard SPA (`odecare.com/app`) | React 18, TypeScript, Vite |
| [odecare-mobile](https://github.com/OdeCare/odecare-mobile) | iOS/Android приложение | Expo, React Native |
| [odecare-landing](https://github.com/OdeCare/odecare-landing) | Маркетинговый сайт (`odecare.com`) | Astro, TypeScript |
| [odecare-platform](https://github.com/OdeCare/odecare-platform) | Инфраструктура, docker-compose, Telegram-бот | Docker, Python aiogram |
| [ec-supplier-agent](https://github.com/OdeCare/ec-supplier-agent) | Локальный инструмент работы с поставщиками | — |

---

## Продовый сервер

| | |
|-|--|
| **IP** | `193.169.239.226` |
| **SSH** | `ssh -i ~/.ssh/deploy_key ubuntu@193.169.239.226` |
| **Рабочая директория** | `~/elder-care-iot/` |
| **Конфиги** | `docker-compose.prod.yml`, `.env` |
| **БД** | `docker exec -it eldercare-db psql -U eldercare -d eldercare` |
| **Логи** | `docker logs <container> --tail 100 -f` |
| **Статус** | `docker ps` |

### Сервисы

| Контейнер | Назначение |
|-----------|-----------|
| `eldercare-backend` | FastAPI API |
| `eldercare-web` | React SPA |
| `eldercare-db` | PostgreSQL |
| `eldercare-redis` | Redis |
| `eldercare-mqtt` | Mosquitto MQTT |
| `eldercare-bot` | Telegram-бот |
| `eldercare-nginx` | Reverse proxy |

### Деплой

```bash
ssh -i ~/.ssh/deploy_key ubuntu@193.169.239.226
cd ~/elder-care-iot
git pull origin main
docker compose -f docker-compose.prod.yml up -d
```

---

## Telegram-боты

| Бот | Username | Назначение |
|-----|----------|-----------|
| Продуктовый | `@odecare_bot` | Алерты для пользователей |
| Деплой | *(приватный)* | CI/CD уведомления |

---

## Локальная разработка

Каждое репо независимо. Перед работой читай `CLAUDE.md` внутри репо — там стек, команды, ограничения.

```bash
# Backend
cd odecare-backend && cp .env.example .env && uvicorn src.main:app --reload

# Web
cd odecare-web && npm ci && npm run dev

# Mobile
cd odecare-mobile && npm ci && npx expo start

# Landing
cd odecare-landing && npm ci && npm run dev
```

---

## Ребрендинг

Активный процесс: [REBRAND.md](./REBRAND.md)
