# Развёртывание приложения

Публичный образ GHCR поддерживает `linux/amd64` и `linux/arm64`. Для чтения пакета вход в GHCR не требуется. При развёртывании используйте полный SHA проверенной версии. Тег `latest` обновляется при публикации из `main`.

Для первого развёртывания ПР11 закреплён SHA `e87290afa237c0701caf3d71195226ed917761f7`. Docker на Linux ARM64 автоматически выбирает соответствующий образ из общего манифеста.

```sh
image=ghcr.io/gray-advantage/devops-ci-app:e87290afa237c0701caf3d71195226ed917761f7
docker pull "$image"
docker run -d --name ci-app -p 127.0.0.1:5001:5000 "$image"
curl --fail --retry 10 --retry-connrefused http://127.0.0.1:5001/health
docker exec ci-app id
docker logs ci-app
docker rm -f ci-app
```

Ожидаемый ответ `GET /health` — HTTP 200 и JSON `{"status":"ok"}`. Процесс контейнера работает как пользователь `app`. В Ansible передайте адрес узла и SSH-пользователя через inventory, закреплённый тег через переменные и настройте проброс порта к порту `5000` контейнера.
