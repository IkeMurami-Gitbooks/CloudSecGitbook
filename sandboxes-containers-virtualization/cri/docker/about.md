# About

Контейнерный движок. Есть и другие, например, rkt. У OpenShift свой — CRI-O.

## Установка

Можно поставить Docker Desktop, а можно отдельно нужные консольные инструменты:

```
brew install docker
brew install docker-compose
```

Настраиваем docker-compose как плагин к docker (позволит писать `docker compose`)

```
mkdir -p ~/.docker/cli-plugins
ln -sfn $(brew --prefix)/opt/docker-compose/bin/docker-compose ~/.docker/cli-plugins/docker-compose
```

Настраиваем docker buildx:

```
brew install docker-buildx
ln -sfn /opt/homebrew/opt/docker-buildx/bin/docker-buildx  ~/.docker/cli-plugins/docker-buildx
```
