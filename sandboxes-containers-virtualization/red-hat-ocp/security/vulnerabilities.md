# Vulnerabilities

## Хранение секретов в ConfigMap, а не в Secret.

## Machine Config Server: конфиги подов публично доступны

MachineConfigServer поднят на порту 22623 по умолчанию

По адресу /config/worker и /config/master можно получить конфиги подов, которые будут подключаться к кластеру. А там могут быть токены, пароли и многое другое

Подробнее: [https://github.com/openshift/machine-config-operator/blob/master/docs/MachineConfigServer.md](https://github.com/openshift/machine-config-operator/blob/master/docs/MachineConfigServer.md)
