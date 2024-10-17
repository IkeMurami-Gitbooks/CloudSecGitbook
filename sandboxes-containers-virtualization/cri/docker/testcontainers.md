# Testcontainers

Это библиотека под разные языки, которая позволяет из кода поднимать контейнеры для тестового окружения (базы и тп)

site: [https://testcontainers.com/](https://testcontainers.com/)

### Testcontainers & Сolima

Чтобы библиотека testcontainers работала с colima точно также как с Docker Desktop необходимо указать переменные окружения:

```
export DOCKER_HOST=unix://$HOME/.colima/docker.sock
export TESTCONTAINERS_DOCKER_SOCKET_OVERRIDE=/var/run/docker.sock
```

где вместо`$HOME` подставить домашнюю директорию
