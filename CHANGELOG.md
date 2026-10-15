# Changelog

Формат: [Keep a Changelog](https://keepachangelog.com/ru/1.1.0/), версии по [SemVer](https://semver.org/lang/ru/).

## [1.0.0] - 2026-10-15
### Added
- Гостевая книга на FastAPI + PostgreSQL, запуск через Docker Compose.
- CI (Ruff, pytest) и публикация образа в ghcr.io.

## [1.1.0] - 2026-10-16
### Added
- Необязательное поле `author_email` у сообщений (nullable-колонка, миграция обратно совместима).