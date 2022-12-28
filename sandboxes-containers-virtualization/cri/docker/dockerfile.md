# Dockerfile

## Build image from Dockerfile

Собираем из локального файла:

```
docker build .
docker build -f MyDockerfile -t ikemurami/myimage:v1.0 /path/to/dir/context
```

## Цепочка FROM в Dockerfile

В dockerfile допустимо делать цепочки из образов. То есть билдим один образ (golang AS builder) для билда, а для запуска используем другой (alpine) и перекидываем бинарь из первого командой COPY.

```
FROM golang:1.14-stretch AS builder

ENV CGO_ENABLED=0
ENV GOOS=linux
ENV GO111MODULE=on

RUN mkdir -p /go/src/example.com/test/project
ADD . /go/src/example.com/test/project

WORKDIR /go/src/example.com/test/project/

# RUN go test -mod vendor  -v ./...
RUN go build -mod vendor -a -o /bin/project /go/src/example.com/test/project/cmd/main.go



FROM alpine:3.10

RUN apk --no-cache add ca-certificates

WORKDIR /bin
COPY --from=builder /bin/project  /bin/project

EXPOSE 8080

ENTRYPOINT ["/bin/project"]
```

## ENTRYPOINT & CMD

ENTRYPOINT определяет программу, которая будет запускать при старте контейнера (по умолчанию, `/bin/sh -c`).

CMD — определяет аргументы для ENTRYPOINT.&#x20;

Соотв, если мы хотим сделать контейнер, посвященный одной программе, то переопределяем ENTRYPOINT.

## Статьи

По командам докера (Dockerfile):\
[https://habr.com/ru/company/ruvds/blog/439980/](https://habr.com/ru/company/ruvds/blog/439980/)\
[https://infoboxcloud.ru/community/blog/infoboxcloud/200.html](https://infoboxcloud.ru/community/blog/infoboxcloud/200.html)
