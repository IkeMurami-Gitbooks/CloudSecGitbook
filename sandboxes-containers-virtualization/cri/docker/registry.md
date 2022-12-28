# Registry

Enum: [https://github.com/nccgroup/go-pillage-registries](https://github.com/nccgroup/go-pillage-registries)

Подключение к регистри по логину паролю:

```
docker login -u="someuser+namespace" -p="password" quay.io
```

Пример auth-конфига для регистри

```json
{
     "auths": {
          "quay.io": {
               "auth": "base64(someuser+namespace:password)",
               "email": "someuser@gmail.com"
          }
     }
}
```
