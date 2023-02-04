# Tools

checkov - тестировавние конфигурации облачных контейнеров [https://github.com/bridgecrewio/checkov/](https://github.com/bridgecrewio/checkov/)

SadCloud - [https://github.com/nccgroup/sadcloud](https://github.com/nccgroup/sadcloud)

ScoutSuite — [https://github.com/nccgroup/ScoutSuite](https://github.com/nccgroup/ScoutSuite)

k8s,k3s,prometheus,thanos,helm

cloudquery – позволяет настраивать asset management вашей облачной инфраструктуры [https://www.cloudquery.io/](https://www.cloudquery.io/)

Service Mesh — дает хорошую observability

Cilium — инструмент, для управления политиками сети в Service Mesh архитиктуре

No internet Policy

Golden Images (предустановленные и зааппрувленные образы)

Zero Trust Proxy для доступа к инфраструктуре: [https://github.com/gravitational/teleport](https://github.com/gravitational/teleport) (на базе его можно построить PAM)

kyverno — Kubernetes Native Policy Management — [https://kyverno.io/](https://kyverno.io/)

методологии — SLSA, SAAM, ASVS

[Packer](https://developer.hashicorp.com/packer) — инструмент от HashiCorp для создания образов ВМ для облачных платформ (поддерживает большое количество, в том числе и Yandex Cloud). Указываем спецификацию, токен, запускаем — получаем образ в нашем облаке. Позволяет описывать образы как код (IaaC подход)

[Terraform](https://www.terraform.io/) —  управление сетевыми сервисами и еще чем-то на основе конфигов (разработано hashicorp). Off & Def Terraform: [https://www.youtube.com/watch?v=yt-3ndhMMn8](https://www.youtube.com/watch?v=yt-3ndhMMn8)
