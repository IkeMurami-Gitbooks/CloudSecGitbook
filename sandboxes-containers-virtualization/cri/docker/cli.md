# CLI

## Практические примеры использования docker

Link: [https://blog.ropnop.com/docker-for-pentesters/](https://blog.ropnop.com/docker-for-pentesters/)

### Запуск контейнера

Общий вид

```
docker run -d --name имя_контейнера имя_образа
    -d - запуск в автономном режиме
    --name - имя контейнера
    в конце - имя_образа
```

Примеры

```
docker run --rm -i -t --entrypoint=/bin/bash

docker run --name имя_контейнера -d -p 80:80 имя_образа
    Запуск нового контейнера с проброшенным портом (слева - порт сервиса, справа - через какой порт будут уходить сообщения)

```

Отправка команды терминалу в контейнер:

```
docker exec -it <container_id> <Команда>

-i - Оставить STDIN открытым, даже если контейнер запущен в неприкрепленном режиме
-t, -tty - Запустить псевдотерминал
```

### Работа с контейнерами

Запущенные контейнеры:

```
docker ps
```

Удалить контейнер:

```
docker rm -f имя_контейнера
```

Работа с файлами внутри контейнера: чтобы заменить какой-нибудь файл в контейнере, используется команда `docker cp`. Она копирует файл из локальной файловой системы в контейнер:

```
docker cp qa_nginx:/etc/nginx/nginx.conf /tmp/nginx.conf
```

Где `qa_nginx` и `/etc/nginx/nginx.conf` — имя контейнера и путь к скачиваемому файлу из контейнера, соответственно, а `/tmp/nginx.conf` путь до нового файла в текущей операционной системе.

Остановить контейнер

```
docker stop qa_nginx
```

Удалить все контейнеры, которые остановлены

```
docker container prune
```

### Сохранение изменений в контейнере

Если мы удалим наш контейнер и вновь его запустим, то все наши изменения, сделанные через консоль, исчезнут. Чтобы сохранить изменения используется команда `docker commit`:

```
docker commit 2404abeecf66 nginx_mc

    Данная команда создаст новый образ nginx_mc, 
    в котором будет уже установленный редактор mc. 
    Здесь 2404abeecf66 - id контейнера, который можно узнать выполнив команду docker ps.
```

### Работа с образами

Список установленных образов:

```
docker image ls
```

Установить образ из репозитория:

```
docker pull <repo>
```

Можно установить образ из tar-архива (gz/gzip/tgz..):

```
docker load -i <some_image>.tar[.gz]
```

Удалить образ:

```
docker image rm <image_id>
```

## Volumes

Подключение разделов в процессе запуска контейнера (например, если надо передать какие-то файлы на обработку):

```
docker run --rm -it -v /path/to/dir/on/home:/path/to/dir/on/container ...
```

Можно устанавливать права сразу:

```
... -v /path1:/path2:ro ...
```

## Работа с логами

```
Посмотреть логи
docker logs <container_name> 
    --timestamps - писать время
    --since ГГГГ-ММ-ДД
    --since ГГГГ-ММ-ДДТЧЧ (ex: 2018-01-30Т11:00)
    --tail N - последние n строк
    -f, --follow - непрерывный вывод

Узнать, где лежат:
docker inspect --format='{{.LogPath}}' <container_name>
    

```

## Информация о занимаемом объеме памяти

```
docker system df  - disk usage
docker system info
```

## Ограничение сети

```
docker run --rm -it --network none myimage ...
```

Другие сетевые адаптеры (можно делать свои):

* bridge — сеть между контейнерами на одном хосте (default)
* overlay — сеть между контейнерами на разных хостах
* macvlan —&#x20;
* ...
* none

## Перенос директории с образами в новую папку

link: [https://linuxconfig.org/how-to-move-docker-s-default-var-lib-docker-to-another-directory-on-ubuntu-debian-linux](https://linuxconfig.org/how-to-move-docker-s-default-var-lib-docker-to-another-directory-on-ubuntu-debian-linux)

## Ограничение общих ресурсов

Есть такая проблема. Пусть есть несколько контейнеров, запущенных на одной машине. В случае, если один контейнер выедает все ресурсы (например озу), то от этого падают все контейнеры. Такое поведение не приемлемо, если есть контейнеры критичные и которые by design не могут выжирать столько ресурсов.&#x20;

Решение — разделять важные и о не очень контейнеры на cgroups

У докера есть опция `—cgroup-parent` — ты можешь сделать цгруппу где ограничить общую память до 14 ГБ, а потом внутри запускать безлимитные контейнеры, например (или выставить дополнительные лимиты для контейнеров внутри).

или сделать то же самое через `systemd`

[https://stackoverflow.com/questions/46408673/docker-17-06-ce-default-container-memory-limit-on-shared-host-resources/46557336#46557336](https://stackoverflow.com/questions/46408673/docker-17-06-ce-default-container-memory-limit-on-shared-host-resources/46557336#46557336) Например вот ответ где объясняется как.

## Papers and notes

Подробная документация: [https://docs.docker.com/engine/reference/](https://docs.docker.com/engine/reference/)\
Работа с Docker: [https://community.vscale.io/hc/ru/community/posts/211783625-Основы-работы-с-Docker](https://community.vscale.io/hc/ru/community/posts/211783625-%D0%9E%D1%81%D0%BD%D0%BE%D0%B2%D1%8B-%D1%80%D0%B0%D0%B1%D0%BE%D1%82%D1%8B-%D1%81-Docker)
