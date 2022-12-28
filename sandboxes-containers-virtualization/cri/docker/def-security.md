# \[Def] Security

## Docker capabilities

У докер контейнеров есть возможность ограничивать или предоставлять доступ к какой-то функциональности (например, доступ к сетевым интерфейсам хоста, или дать возможность контейнеру работать с группами, менять их и тп).

В целях безопасности:

Обязательны для блокировки:

* SYS\_CHROOT
* SYS\_PTRACE
* NET\_RAW
* NET\_ADMIN
* SYS\_ADMIN

Опциональны для блокировки (рекомендуется для собственных сервисов, дополнение к обязательным):

* FSETID
* SETUID
* SETGID
* CHOWN
* NET\_BIND\_SERVICE

Не надо использовать директиву privileged.&#x20;

Во всех образах должны быть созданы отдельные пользователи, т.е. запрещено использование пользователя root (uid=0)

Часть капабилити будут выключены в принудительном порядке, поэтому сервис надо разрабатывать с учетом этого. Вы обязательно должны дропнуть (`cap_drop`) следующие капабилити: FSETID, SETUID, SETGID, SYS\_CHROOT, SYS\_PTRACE, CHOWN, NET\_RAW, NET\_ADMIN, SYS\_ADMIN, NET\_BIND\_SERVICE, подробнее: [https://docs.docker.com/compose/compose-file/compose-file-v3/#cap\_add-cap\_drop](https://docs.docker.com/compose/compose-file/compose-file-v3/#cap\_add-cap\_drop)

## Безопасность Docker-контейнеров

Хороший материал об обеспечении безопасности Docker'а. Начиная от правильной конфигурации самого демона, и заканчивая настройкой seccomp (позволяет ограничить список системных вызовов, доступных конкретному приложению) и Docker secrets.

[https://0x00sec.org/t/securing-docker-containers/16913](https://0x00sec.org/t/securing-docker-containers/16913)
