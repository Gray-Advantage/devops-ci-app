# devops-ci-app

Учебное Flask-приложение для практической работы № 10 по дисциплине «Инструменты девопс».

CI выполняет Pylint, pytest, сборку Docker-образов и smoke-test. Каждый контейнер проверяется на нативном runner для своей архитектуры (`linux/amd64` или `linux/arm64`). После успешных проверок push в `main` публикует обе архитектуры под общими тегами полного SHA и `latest`. Pull Request проходит проверки без публикации.

- Проверка жизнеспособности — `GET /health` возвращает HTTP 200 и `{"status":"ok"}`.
- Публичный образ — `ghcr.io/gray-advantage/devops-ci-app`.
- Workflow — [ci.yml](.github/workflows/ci.yml).
