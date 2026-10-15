# Runbook

## Сервис не отвечает
1. `docker compose -f compose.prod.yaml ps` — какие контейнеры живы.
2. `curl http://localhost:8000/health` — ожидаем `{"status":"ok"}`.
3. `docker compose -f compose.prod.yaml logs app --tail 100`.

## После выката ошибки: откат
1. Узнать предыдущую версию: раздел Packages на GitHub или `CHANGELOG.md`.
2. Выполнить (PowerShell): 
   `$env:APP_VERSION="1.0.0"; docker compose -f compose.prod.yaml up -d`
   (bash: `APP_VERSION=1.0.0 docker compose -f compose.prod.yaml up -d`)
3. Проверить `/health` и `GET /messages`.

Откат безопасен: миграции добавляют только необязательные колонки, поэтому старая версия работает с новой схемой.

## База недоступна
1. `docker compose -f compose.prod.yaml logs db --tail 100`.
2. `docker compose -f compose.prod.yaml restart db`; приложение переподключится при следующем запросе.
3. Данные лежат в volume `pgdata`. **Не** запускать `docker compose down -v`: это удалит данные.

## Приложение не стартует: «password authentication failed»
Пароль в `.env` не совпадает с паролем, с которым создана база. Либо верните прежний пароль, либо (если данные не нужны) пересоздайте том: `docker compose down -v`.

## Где что лежит
- Конфиг: `.env` (не в git), шаблон `.env.example`.
- Образы: ghcr.io/ваш-логин/guestbook-workshop.
- Логи: `docker compose logs`.