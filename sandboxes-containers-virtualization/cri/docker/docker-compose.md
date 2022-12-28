# docker compose

## Примеры конфигов&#x20;

Пишутся в формате yaml. По дефолту должны быть названы docker-compose.yml, но можно и по-другому (тогда использовать ключ -f)

github: [https://github.com/docker/awesome-compose](https://github.com/docker/awesome-compose)

## Управление

```
Собрать:
docker-compose build

Остановить:
docker-compose down 
ключ --rmi - удалит все, что было связано с билдом

Запустить:
docker-compose up - поднять инфру
docker-compose -f some_config.yml up -d 

Или одной командой удалить страрые контейнеры, пересобрать и сбилдить новые:
$ docker compose rm -f && docker compose build && docker compose up 
```

Можно указать несколько конфигов, например:

```
$ ls -al
docker-compose.prod.yml
docker-compose.mocks.yml
docker-compose.yml
$ docker compose -f docker-compose.yml -f docker-compose.mocks.yml up
```

При этом, в docker-compose.yml — базовые настройки, а в docker-compose.mocks.yml — настройки, связанные с Mock-окружением.

Например:

```yaml
# docker-compose.yml
version: '3'

networks:
    default:
        driver: bridge
        enable_ipv6: true
        
# docker-compose.mocks.yml
version: '3'

services:
    my-service:
        image: ...
```

## Синтаксис конфига

man: [https://docs.docker.com/compose/compose-file/](https://docs.docker.com/compose/compose-file/)

port mapping (format - "HOST:CONTAINER")

```
ports:
  - "8080:80"
```

tty — добавляем в services, чтоб контейнер не падал, если у нас нет CMD (нечего запустить если, например образ системы только есть). Пример:

```yaml
version: '3'

services:

  ruby_rails_irb:
    build:
      context: .
      dockerfile: Dockerfile
    container_name: rails-irb
    restart: always
    depends_on:
     - db
    tty: true
```

Настройка сетки

```yaml
version: '3'

services:
  myservice:
    ...
    networks:
    - my-spring-app-network

networks:
  my-spring-app-network:
```

Настройка логирования

```yaml
version: '3'

services:
  myservice:
    ...
    logging:
      driver: "local"
      options:
        max-size: "10m"
        max-file: "3"
```

