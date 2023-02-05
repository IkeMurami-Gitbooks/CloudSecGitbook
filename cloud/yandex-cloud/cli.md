# YC CLI

Install & Usage: [https://cloud.yandex.ru/docs/cli/quickstart#install](https://cloud.yandex.ru/docs/cli/quickstart#install)

```
// Init YC
yc init

// Show current config
yc config list

// Show profiles (congig groups)
yc config profile list
```

Команды CLI разделены на группы, каждая из которых соответствует сервису или компоненту Yandex Cloud. Например:

* `yc resource-manager …` — управление облаками и каталогами;
* `yc compute …` — управление ВМ;
* `yc load-balancer …` — управление балансировщиками нагрузки.

Управление кластерами баз данных:

* `yc managed-mysql …` — MySQL;
* `yc managed-postgresql …` — PostgreSQL;
* `yc managed-clickhouse …` — ClickHouse.

Есть ещё небольшая группа служебных команд:

* `yc init` — первоначальная настройка CLI;
* `yc version` — показывает версию CLI;
* `yc help` — выводит описание всех команд или справку о команде.

## VM

### List VMs

```
yc compute instance list
```

### Create VM

Создаем startup.sh, который поднимет nginx

```bash
#!/bin/bash
apt-get update
apt-get install -y nginx
service nginx start
sed -i -- "s/nginx/Yandex Cloud - ${HOSTNAME}/" /var/www/html/index.nginx-debian.html
EOF
```

Создаем VM из загрузочного диска ubuntu-2004-lts в конкретной зоне с сетевым интерфейсом и адресом из IPv4:

```
yc compute instance create \
> --name vm-cli \
> --metadata-from-file user-data=startup.sh \
> --create-boot-disk image-folder-id=standard-images,image-family=ubuntu-2004-lts \
> --zone ru-central1-a \
> --network-interface subnet-name=default-ru-central1-a,nat-ip-version=ipv4
```

