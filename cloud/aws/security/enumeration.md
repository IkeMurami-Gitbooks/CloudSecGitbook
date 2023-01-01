# Enumeration

## Brute Force / Enumerate IAM Permissions

## Get Accout ID from AWS Access Keys

Нужен для некоторых API и атак

```
user@host:~$ aws sts get-access-key-info --access-key-id=ASIA1234567890123456
{
    "Account": "123456789012"
}
```

Или вот так ошибкой палит:

```
aws sts get-access-key-info --access-key-id=AKIAUT5AMCC2VINIQAMK

An error occurred (AccessDenied) when calling the GetAccessKeyInfo operation: User: arn:aws:iam::317627044021:user/zfr_test is not authorized to perform: sts:GetAccessKeyInfo
```

Это означает, что Account ID — 317627044021, имя пользователя — zfr\_test

## Tools

Есть разные инструменты перебора разрешений (Brute Force / Enumerate IAM Permissions):

### enumerate-iam

enumerate-iam (py) — шумная, могут и заблочить [https://github.com/andresriancho/enumerate-iam](https://github.com/andresriancho/enumerate-iam)

Пример использования

```
# Обновить правила
cd enumerate_iam/
git clone https://github.com/aws/aws-sdk-js.git
python generate_bruteforce_tests.py

# Запускаем скан
./enumerate-iam.py --access-key $AWS_ACCESS_KEY_ID --secret-key $AWS_SECRET_ACCESS_KEY --session-token $AWS_SESSION_TOKEN
```

Замечание:

Следует отметить, что этот инструмент очень шумный и генерирует тонны журналов CloudTrail. Это позволяет защитнику очень легко обнаружить эту активность и заблокировать вас от этой роли или пользователя. Сначала попробуйте другие методы перечисления разрешений (иначе прискуете потерять доступ к ключам).

По состоянию на 20.12.2020 в API AWS есть ошибка, которая позволяет перечислять разрешения без входа в CloudTrail (см следующий пункт).

### aws\_stealth\_perm\_enum

Enumerate Permissions without Logging to CloudTrail

src: [https://github.com/Frichetten/aws\_stealth\_perm\_enum](https://github.com/Frichetten/aws\_stealth\_perm\_enum)

research: [https://frichetten.com/blog/aws-api-enum-vuln/](https://frichetten.com/blog/aws-api-enum-vuln/)\
кратко: [https://hackingthe.cloud/aws/enumeration/stealth\_perm\_enum/](https://hackingthe.cloud/aws/enumeration/stealth\_perm\_enum/)

Пример:

![](<../../../.gitbook/assets/изображение (2).png>)
