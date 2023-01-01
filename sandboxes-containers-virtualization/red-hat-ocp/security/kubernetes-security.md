# Kubernetes Security

Есть понятие нод, а есть понятие контейнеров. Контейнеры крутятся на нодах openshift (считай на нодах куба).

## Cluster Monitoring

Сервисы Cluster Monitoring устанавливаются на все ноды. Базируется все на [Prometheus](https://prometheus.io/). Сюда входит и [Grafana](https://grafana.com/) Dashboard.

## Cluster Logging

Когда оператор логирования установлен, то он устанавливается на все ноды. «The cluster logging services are based upon [Elasticsearch](https://www.elastic.co/products/elasticsearch), [Fluentd](https://www.fluentd.org/architecture), and [Kibana](https://www.elastic.co/guide/en/kibana/current/introduction.html) (EFK).» Fluentd устанавливается на каждую ноду и собирает логи со всех контейнеров и нод и отправляет в эластик. Потом пользователи и админы через Kibana могут анализировать логи.

## Audit

Аудит событий и хоста установлен на все ноды.
