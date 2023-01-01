# Container Security

## Отдельные рекомендации

* Не рекомендуется использовать Persistent Volumes (PV) и другие решения, требующие хранения данных на стороне OpenShift
* Не запускать контейнеры с привилегиями (securityContext.privileged)
* Не запускать контейнеры под root (uid=0)
* не использовать никаких security context constraints, кроме restricted
* для хранения конф информации использовать secrets (доступ через volumeMount или secretKeyRef)
* &#x20;настраивать TLS (zero trust)
* Ingress/Egress прокси (nginx, envoy, mq-gateway, kafka-gateway, db-gateway) внутри проекта. Должны быть реализованы механизмы аутентификации и авторизации
* не использовать HostNetwork
* не использовать node ports
* Использовать COPY, а не ADD

## Отдельные заметки

Container Engine — предлагает набор инструментов для таких задач как создание и запуск контейнеров.

CRI — Container Runtime Interface

CRI-O — Container Engine of OpenShift. Как реализация Kubernetes CRI, CRI-O позволяет использовать среды выполнения, совместимые с OCI (Open Container Initiative).

OCI — Open Container Initiative — проект Linux Foundation, по разработке открытых стандартов для виртуализации на уровне операционной системы, в первую очередь контейнеров Linux. В настоящее время разрабатываются и используются две спецификации: спецификация среды выполнения (runtime-spec) и спецификация изображения (image-spec).

CRI-O — контейнерный движок по умолчанию для OpenShift 4, заменяющий Docker, который был по умолчанию в OpenShift 3.11.

## CRI-O

Для запуска контейнеров вне OpenShift, используется **podman** (on RHEL host).

В архитектуре OpenShift не приветствутся обращение напрямую к CRI-O, однако это можно сделать с помощью команды **crictl** с любой ноды openshift и посмотреть например логи на другом контейнере:

```
# crictl ps

49f7832d3c4b9 quay.io/openshift-release-dev/ocp-v4.0-art-dev@sha256…      
    5 hours ago   Running   openvswitch    0b989143485eb

# crictl logs 49f7832d3c4b9

```

Почитать про возможности crictl: [https://github.com/kubernetes-sigs/cri-tools/blob/master/docs/crictl.md](https://github.com/kubernetes-sigs/cri-tools/blob/master/docs/crictl.md)\
Про разницу podman и crictl: [https://www.openshift.com/blog/crictl-vs-podman](https://www.openshift.com/blog/crictl-vs-podman)
