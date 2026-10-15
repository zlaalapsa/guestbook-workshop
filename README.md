# Guestbook

Гостевая книга на FastAPI + PostgreSQL с CI/CD, версионированными релизами и откатом.

## Быстрый старт

```bash
git clone https://github.com/ваш-логин/guestbook-workshop.git
cd guestbook-workshop
cp .env.example .env      # впишите свой пароль в POSTGRES_PASSWORD
docker compose up --build
```

Откройте http://localhost:8000/docs.

## API

- `GET /` — приветствие
- `GET /health` — проверка работоспособности
- `GET /messages` — список сообщений
- `POST /messages` — `{"author": "...", "text": "...", "author_email": null}`

## Разработка

```bash
uv sync
uv run ruff check .
uv run pytest
```

## Релизы

Пуш в `main` публикует `ghcr.io/ваш-логин/guestbook-workshop:latest`.
Тег `vX.Y.Z` публикует образ `:X.Y.Z`. История версий в [CHANGELOG.md](CHANGELOG.md).

Запуск конкретной версии:

```bash
APP_VERSION=1.1.0 docker compose -f compose.prod.yaml up -d
```

Аварийные действия — в [RUNBOOK.md](RUNBOOK.md).