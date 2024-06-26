# Terraform Block

`terraform` — содержит настройки Terraform, в частности информацию о провайдерах. Провайдеры по умолчанию устанавливаются из [Terraform Registry](https://registry.terraform.io/). Так же, рекомендуется фиксировать версию провайдера.

## cloud block

Для развертывания ресурсов и подключения к облаку вам понадобятся секреты, токены и тп. Все это будет сохранено в State. Пока разворачивается тестовую инфру, допустимо хранить локально все. Однако для разворачивания production среды встает вопрос о безопасном хранении секретов конфигурации.

Можно использовать [Terraform Cloud](https://app.terraform.io) для хранения состояния и секретов и управлять раскаткой оттуда. Для этого используем блок `cloud` в `terraform` блоке:

```hcl
terraform {
  cloud {
    organization = "organization-name"
    workspaces {
      name = "learn-tfc-aws"
    }
  }
}
```

Далее аутентифицируемся в консоли:

```
terraform login
```

Теперь при каждой раскатке State будет синхронизироваться с cloud'ом. По окончании работы не забываем удалять state:

```
rm terraform.tfstate
```
