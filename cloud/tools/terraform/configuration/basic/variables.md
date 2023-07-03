# Variables

Чтобы сделать конфигурацию гибче, можем определить переменные через файл `variables.tf`.

```hcl
variable "instance_name" {
  description = "Value of the Name tag for the EC2 instance"
  type        = string
  default     = "ExampleAppServerInstance"
}
```

И далее использовать:

```hcl
some = var.instance_name
```
