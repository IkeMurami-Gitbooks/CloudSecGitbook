# AWS Lambda

## AWS Lambda Abuse

Описание того, как минимизировать ущерб от DDoS-атак на AWS Lambdas.

Тезисно:

* Убедиться, что код не зависает на неправильных данных (ReDoS или длинные пейлоады)
* Оповещать о превышении биллинга
* Сoncurrency level для каждой функции
* Использовать SQS в качестве брокера для функции Lambda для обработки нескольких событий одновременно
* Использовать CDN (например, CloudFront) или AWS WAF
* Требовать API ключ для доступа к API Gateway
* Присмотреться к «Token Bucket» моделям

[https://luminousmen.com/post/aws-lambda-abuse](https://luminousmen.com/post/aws-lambda-abuse)

## AWS Lambda&#x20;

Есть история, что если RCE в Lambda, то изнутри увидешь все другие s3-бакеты и сервера, сможешь их енумить, напрямую обращаться
