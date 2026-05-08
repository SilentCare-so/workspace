# Ребрендинг SilentCare → OdeCare

**Как работаем:** отмечаешь шаг как сделанный `[x]`, говоришь Клоду "делаем шаг X" — он читает этот файл и выполняет.

---

## Таблица замен

| Старое | Новое |
|--------|-------|
| `SilentCare` | `OdeCare` |
| `silentcare` | `odecare` |
| `HomeCare IoT` | `OdeCare IOT` |
| `silentcare.co` | `odecare.com` |
| `api.silentcare.co` | `api.odecare.com` |
| `SilentCare-so` (GitHub org) | `OdeCare` ✓ |
| `homecare-backend` / `homecare-web` и т.д. | `odecare-backend` / `odecare-web` и т.д. |
| `@silentcare_bot` | `@odecare_bot` |
| `@silentcare_alert_bot` | `@odecare_alert_bot` |
| `@silentcareco` (Twitter) | `@odecareco` |
| `*@silentcare.co` (все email) | `*@odecare.com` |
| `com.silentcare.app` | `com.odecare.app` |
| `silentcare-cy` (EAS owner) | новый owner |

---

## ФАЗА 1 — Подготовка (ручные действия, только ты)

> Сделать **первыми** — всё остальное зависит от этих шагов.

- [x] **1.1** Зарегистрировать домен `odecare.com`, настроить DNS
- [] **1.2** Настроить email на `odecare.com` (noreply, privacy, legal, hi)
- [x] **1.3** Переименовать GitHub org `SilentCare-so` → новый slug (Settings → Profile)
- [x] **1.4** Переименовать GitHub репо:
  - [x] `homecare-backend` → `odecare-backend`
  - [x] `homecare-web` → `odecare-web`
  - [x] `homecare-mobile` → `odecare-mobile`
  - [x] `homecare-landing` → `odecare-landing`
  - [x] `homecare-platform` → `odecare-platform`
- [x] **1.5** Переименовать Telegram бот `@silentcare_bot` → `@odecare_bot` (через @BotFather)
- [x] **1.6** Деплой-бот обновлён, токен в GitHub Secrets поменян
- [ ] **1.7** Переименовать Twitter/X аккаунт `@silentcareco` → `@odecareco`
- [x] **1.8** Переименовать EAS проект: expo.dev → проект `silentcare` → `odecare`
- [x] **1.9** Подготовить новые иконки: `favicon.svg`, `apple-touch-icon.png`, `icon-192.png`, `icon-512.png`

---

## ФАЗА 2 — Продовый сервер

> Клод выполняет сам через SSH (`deploy_key`). Сервер: `193.169.239.226`, dir: `~/elder-care-iot/`

- [x] **2.1** Обновить `.env` на сервере:
  - [x] `BACKEND_IMAGE`: `ghcr.io/silentcare-so/homecare-backend:latest` → `ghcr.io/odecare/odecare-backend:latest` ✓
  - [x] `RESEND_FROM_EMAIL`: `hi@silentcare.co` → `hi@odecare.com` ✓
- [ ] **2.2** Переименовать директорию `~/elder-care-iot/` → `~/odecare/` *(опционально, после перезапуска)*

---

## ФАЗА 3 — Workspace (локальные файлы)

> Клод выполняет сам.

- [x] **3.1** Обновить корневой `CLAUDE.md` — заголовок, GitHub org slug, URL, имена репо ✓
- [ ] **3.2** Переименовать локальную папку `SilentCare` → `OdeCare` *(после — переоткрыть workspace)*
- [ ] **3.3** Обновить memory-файлы Claude (пути изменятся при переименовании папки)

---

## ФАЗА 4 — `homecare-platform`

> Критично: docker-compose с image URL. Делать **до перезапуска контейнеров**.

- [ ] **4.1** `docker-compose.prod.yml` — 4 image URL (GHCR), `CORS_ORIGINS`, `RESEND_FROM_EMAIL`, `FRONTEND_URL`
- [ ] **4.2** `docker-compose.dev.yml` — комментарий
- [ ] **4.3** `.env.example` — комментарий
- [ ] **4.4** `CONTRIBUTING.md` — заголовок
- [ ] **4.5** `CLAUDE.md` — заголовок, image names, health check URL
- [ ] **4.6** `README.md` — описание, image URLs, ссылки на репо
- [ ] **4.7** `scripts/deploy-server.sh` — комментарии, `git clone` URL
- [ ] **4.8** `.github/workflows/ci-cd.yml` — `BOT_IMAGE`, `SIMULATOR_IMAGE`, Telegram-уведомление
- [ ] **4.9** `telegram-bot/env.example` — комментарий
- [ ] **4.10** `telegram-bot/src/bot.py` — docstring
- [ ] **4.11** `telegram-bot/src/main.py` — docstring, лог-строка

---

## ФАЗА 5 — `homecare-backend`

- [ ] **5.1** `src/core/config.py` — `app_name`, все URL, email адреса, CORS origins
- [ ] **5.2** `src/main.py` — docstring, описание API, `<title>` HTML
- [ ] **5.3** `src/services/email_service.py` — темы и заголовки писем (EN / RU / HE)
- [ ] **5.4** `src/services/auth_service.py` — docstring
- [ ] **5.5** `scripts/seed_demo.py` — demo email адреса, лог-строки
- [ ] **5.6** `scripts/seed_data.py` — лог-строка
- [ ] **5.7** `scripts/init-db.sql` — комментарий
- [ ] **5.8** `.env.example` — все URL и email
- [ ] **5.9** `pyproject.toml` — `description`
- [ ] **5.10** `README.md` — URL, образы, ссылки
- [ ] **5.11** `CLAUDE.md` — prod URL, образы
- [ ] **5.12** `.github/workflows/ci-cd.yml` — `IMAGE_NAME`, `environment.url`, Telegram-уведомление

---

## ФАЗА 6 — `homecare-web`

- [ ] **6.1** `index.html` — `<title>`, `<meta description>`
- [ ] **6.2** `public/site.webmanifest` — `name`, `short_name`
- [ ] **6.3** `public/sw.js` — push-уведомление title
- [ ] **6.4** `src/pages/Login.tsx` — лого H1, ссылка на privacy
- [ ] **6.5** `src/pages/Register.tsx` — лого H1, ссылка на privacy
- [ ] **6.6** `src/pages/ForgotPassword.tsx` — лого H1
- [ ] **6.7** `src/components/Layout.tsx` — лого в сайдбаре
- [ ] **6.8** `src/components/FamilyLayout.tsx` — лого в хедере
- [ ] **6.9** `src/i18n/en.json` — `auth.register.subtitle`, `telegramStep1`
- [ ] **6.10** `src/i18n/ru.json` — те же ключи
- [ ] **6.11** `src/i18n/es.json` — те же ключи
- [ ] **6.12** `src/i18n/he.json` — те же ключи
- [ ] **6.13** `package.json` — `name`
- [ ] **6.14** `README.md` — URL, образы
- [ ] **6.15** `CLAUDE.md` — URL, образы
- [ ] **6.16** `.github/workflows/ci-cd.yml` — `IMAGE_NAME`, `url`, Telegram-уведомление

---

## ФАЗА 7 — `homecare-landing`

### 7а — Конфиги и SEO
- [ ] **7.1** `package.json` — `name`
- [ ] **7.2** `astro.config.mjs` — `site` URL
- [ ] **7.3** `public/robots.txt` — комментарий, `Sitemap` URL
- [ ] **7.4** `public/site.webmanifest` — `name`, `short_name`
- [ ] **7.5** `src/layouts/Base.astro` — OG-теги, canonical, hreflang, schema.org, twitter handle, RSS title, form `_subject` (3 языка)
- [ ] **7.6** `src/layouts/BlogPost.astro` — schema.org, breadcrumbs, URLs, title
- [ ] **7.7** `src/pages/feed.xml.ts` — RSS title

### 7б — Компоненты
- [ ] **7.8** `src/components/Header.astro` — лого-текст, пункт меню "Почему SilentCare"
- [ ] **7.9** `src/components/Footer.astro` — лого-текст
- [ ] **7.10** `src/components/BlogCTA.astro` — CTA текст
- [ ] **7.11** `src/i18n/ui.ts` — `footer.disclaimer` × 4 локали (8 строк)
- [ ] **7.12** `src/pages/blog/index.astro` — H1, schema.org

### 7в — Юридические страницы
- [ ] **7.13** `src/pages/privacy.astro` — title, meta, весь правовой текст (~15 мест)
- [ ] **7.14** `src/pages/terms.astro` — title, meta, весь текст (~8 мест), email
- [ ] **7.15** `src/pages/delete-account.astro` — title, meta, текст, alt-теги, URLs

### 7г — Blog-статьи (~22 файла)
- [ ] **7.16** `src/pages/blog/*.astro` — упоминания бренда в контенте статей *(выполняется скриптом)*

### 7д — Иконки (ручное)
- [ ] **7.17** Заменить `public/favicon.svg`
- [ ] **7.18** Заменить `public/apple-touch-icon.png`, `icon-192.png`, `icon-512.png`

---

## ФАЗА 8 — `homecare-mobile`

- [ ] **8.1** `app.json` — `name`, `slug`, `scheme`, `bundleIdentifier`, `android.package`, `owner` ⚠️ критично для App Store/Play
- [ ] **8.2** `eas.json` — `EXPO_PUBLIC_API_URL` (3 окружения) ⚠️ критично
- [ ] **8.3** `package.json` — `name`
- [ ] **8.4** `.env.example` — комментарий, URL
- [ ] **8.5** `src/i18n/en.json` — `auth.appName`, `telegramStep1`, `onboarding` (2 строки)
- [ ] **8.6** `src/i18n/ru.json` — те же ключи
- [ ] **8.7** `src/i18n/he.json` — те же ключи
- [ ] **8.8** `src/i18n/es.json` — те же ключи
- [ ] **8.9** `README.md` — описание, URL, ссылки
- [ ] **8.10** `CLAUDE.md` — URL
- [ ] **8.11** `.github/workflows/ci.yml` — Telegram-уведомление
- [ ] **8.12** `.github/workflows/build.yml` — EAS project URL
- [ ] **8.13** `scripts/pre-build-check.js` — комментарий

---

## ФАЗА 9 — YouTube канал (ручное)

- [ ] **9.1** Переименовать канал → OdeCare
- [ ] **9.2** Обновить описание канала (убрать SilentCare, silentcare.co)
- [ ] **9.3** Обновить аватар/баннер канала
- [ ] **9.4** Обновить ссылки в шапке канала (сайт → odecare.com)
- [ ] **9.5** Пройтись по описаниям видео — заменить `silentcare.co` на `odecare.com`
- [ ] **9.6** Обновить pinned-комментарии и водяные знаки если есть

---

## ФАЗА 10 — Финальная проверка

- [ ] **10.1** Smoke-тест: `odecare.com` — лендинг работает
- [ ] **10.2** Smoke-тест: `odecare.com/app` — дашборд работает, лого OdeCare
- [ ] **10.3** Smoke-тест: мобильное приложение — название OdeCare, онбординг без SilentCare
- [ ] **10.4** Email: тестовый reset-password — тема и заголовок OdeCare
- [ ] **10.5** Push-уведомления — title OdeCare
- [ ] **10.6** Telegram-бот работает под новым username
- [ ] **10.7** CI/CD — деплой проходит с новыми image URL
- [ ] **10.8** Финальный поиск по коду — не должно остаться `silentcare` / `SilentCare` / `HomeCare` в prod-файлах
