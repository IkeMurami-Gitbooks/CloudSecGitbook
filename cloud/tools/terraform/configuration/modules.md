# Modules

Базовая структура модуля:

```
main.tf
README.md
variables.tf
outputs.tf
```

Модуль может быть локальный или из репозитория публичного

Перед применением конфигурации модули нужно загрузить:

```
terraform get -update=true
```
