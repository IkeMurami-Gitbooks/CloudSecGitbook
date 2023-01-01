# S3 Bucket

S3 - Simple Storage Service

## Intro

buckets служат для хранения файлов

Пример ссылок на такие хранилища:\
kaizo-s3-public.s3-ap-southeast-1.amazonaws.com  -> s3://kaizo-s3-public

Они могут быть где угодно - Android, iOS, Web ... Если доступно чтение/запись без аутентификации -> сообщаем, что bucket открыт -> bounty.\


## Upload

```
# aws s3 cp test.txt s3://rzimageupload
upload: ./test.txt to s3://rzimageupload/test.txt
```

## Delete

```
# aws s3 rm s3://rzimageupload/test.txt
delete: s3://rzimageupload/test.txt
```

## Поиск открытых s3 buckets

FestIN - [https://github.com/cr0hn/festin](https://github.com/cr0hn/festin)

Smogcloud - анализ AWS assets. Кроме поиска теневых IP и неправильных настроек, Smogcloud умеет находить торчящие в Интернет FQDN и IP. - [https://github.com/BishopFox/smogcloud](https://github.com/BishopFox/smogcloud)

И, наконец, [репозиторий](https://github.com/SummitRoute/aws\_exposable\_resources), который поможет разобраться, какие ресурсы должны быть открыты для публичного доступа, а какие нет.
