# helm

Инициализация репозитория (при условии, что есть коннект до куба). Включает установку tiller на куб (в тч minikube):

```
helm init
```

Составные части:

* Deployment — как запускать контейнеры
* Service — как подключаться к контейнеру
* Netpol — политики взаимодействия между контейнерами (ака Firewall)
* Configmap
* Ingress — настройка контроллера

Добавление дефолтоного репозитория:

```
helm add repo <name> 
kubernetes-charts.storage.googleapis.com/

helm update repo 
helm search <chart>
helm install <name chart local> <name-repo>/<name-chart>
```

Установить чарт (локальный) на кубер:&#x20;

```
helm install <name-chart-on-kube> <helm path ./> --namespace <namespace>
```

Дефолтные helm-charts для кучи всего: [https://github.com/helm/charts/tree/master/stable](https://github.com/helm/charts/tree/master/stable)
