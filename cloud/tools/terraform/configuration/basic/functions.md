# Functions

В Terraform есть встроенные функции, например:

* `file("ssh.pub")` — прочитать файл `ssh.pub`
* `lookup(var.my_map, var.my_key)` — получить одно значение из map по ключу
* `templatefile` — вызвать скрипт. [Пример](https://developer.hashicorp.com/terraform/tutorials/configuration-language/functions#use-templatefile-to-dynamically-generate-a-script)

Можно строить свои выражения при работе с ресурсами: [https://developer.hashicorp.com/terraform/tutorials/configuration-language/expressions#expressions](https://developer.hashicorp.com/terraform/tutorials/configuration-language/expressions#expressions)

