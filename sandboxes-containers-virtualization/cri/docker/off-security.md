# \[Off] Security

## Container Breakouts

Серия статей, посвященная тому, как происходит выход за пределы контейнера. Об этой угрозе часто можно услышать от маркетологов решений по Container Runtime Security, но время разобраться, как это происходит на самом деле.

[Part 1: Access to root directory of the Host](https://blog.nody.cc/posts/container-breakouts-part1/) \
[Part 2: Privileged Container](https://blog.nody.cc/posts/container-breakouts-part2) \
[Part 3: Docker Socket](https://blog.nody.cc/posts/container-breakouts-part3)

Также автор предлагает познакомиться с [CVE-2019-5736](https://blog.dragonsector.pl/2019/02/cve-2019-5736-escape-from-docker-and.html), [CVE-2019-14271](https://unit42.paloaltonetworks.com/docker-patched-the-most-severe-copy-vulnerability-to-date-with-cve-2019-14271/), а также со статьей ["Abusing Privileged and Unprivileged Linux Containers "](https://www.nccgroup.com/globalassets/our-research/us/whitepapers/2016/june/container\_whitepaper.pdf)

Для того, чтобы предотвратить возможность выхода за пределы контейнера, Clint Gibler написал отдельный [перечень инструментов тестирования](https://tldrsec.com/blog/container-security/).

## Tools

Поиск уязвимостей в docker-контейнерах\
Dockle: [https://github.com/goodwithtech/dockle](https://github.com/goodwithtech/dockle)\
Trivy: [https://github.com/knqyf263/trivy](https://github.com/knqyf263/trivy)

Security Issue / уязвимости в популярных контейнерах с Docker Hub\
[https://containers.goodwith.tech/](https://containers.goodwith.tech/)

## Papers

TODO Reading: Статья про докер контейнеры\
[https://blog.ropnop.com/docker-for-pentesters/](https://blog.ropnop.com/docker-for-pentesters/) \
[https://blog.trailofbits.com/2019/07/19/understanding-docker-container-escapes/](https://blog.trailofbits.com/2019/07/19/understanding-docker-container-escapes/)
