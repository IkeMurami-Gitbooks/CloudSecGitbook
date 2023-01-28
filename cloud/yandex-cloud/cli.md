# YC CLI

Install & Usage: [https://cloud.yandex.ru/docs/cli/quickstart#install](https://cloud.yandex.ru/docs/cli/quickstart#install)

```
// Init YC
yc init

// Show current config
yc config list
```

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

