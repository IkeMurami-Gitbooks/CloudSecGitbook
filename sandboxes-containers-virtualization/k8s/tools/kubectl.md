# kubectl

## Подключение к кластеру по токену

Секрет и цепочку сертификатов можно найти на ControlPanel ноде (по умолчанию, порт 22623) https://\<Address Node>:22623/config/master или /config/worker

Там будет конфиг `kubeconfig`:

```yaml
clusters:
- cluster:
    certificate-authority-data: LS0t...
  name: someName
contexts:
- context:
    cluster: someName
    user: userSecret
  name: contextName
current-context: contextName
preferences: {}
users:
- name: userSecret
  user:
    token: eyJhbGc...
```

`certificate-authority-data` мы декодируем из base64 (там будет цепочка PEM сертификатов) и записываем в файл `cert.crt`. Далее, настраиваем контекст в `kubectl`:

```
kubectl config set-credentials "userSecret" --token="<JWT>"
kubectl config set-cluster clusterName --server="https://<Address Node>:6443" --certificate-authority="/path/to/chain/cert.crt"  --embed-certs
kubectl config set-context contextName --cluster="clusterName" --user="usereSecret"
kubectl config use-context contextName
kubectl get pods
```

## Примеры использования kubectl

Получаем список пространств\
kubectl get namespaces\
kubectl get ns\
\
Создать пространство:\
kubectl create ns \<name>\
\
Удалить пространство: \
kubectl delete namespaces \<name>

Работа с подами\
Получить информацию о поде: \
kubectl describe pod re-privategallery-backend-978dddf6-d2wgx\
\
Все поды: kubectl get pods

Текущий контекст: kubectl config current-context\
Переключить в контексте на другой namespace: kubectl config set-context \<CONTEXT, ex: minikube> --namespace \<NAMESPACE>

Посмотреть Persistance Volume: kubectl get pv\
Посмотреть Persistance Volume Claim: kubectl get pvc

## Troubleshooting

[https://managedkube.com/kubernetes/k8sbot/troubleshooting/imagepullbackoff/2019/02/23/imagepullbackoff.html](https://managedkube.com/kubernetes/k8sbot/troubleshooting/imagepullbackoff/2019/02/23/imagepullbackoff.html)

## Что еще можем получить

Запуск без проверки сертификата:

```
$ kubectl --insecure-skip-tls-verify <cmd>
```

Доступные ресурсы (= информация о k8s-ноде)

```
kubectl --insecure-skip-tls-verify api-resources
```

Можно получить HTTP запрос, соотв команде kubectl:

```
$ kubectl --insecure-skip-tls-verify auth can-i list pods -v 9
I0112 16:04:38.235938   37941 round_trippers.go:435] curl -k -v -XGET  -H "Accept: application/json, */*" -H "Authorization: Bearer <masked>" -H "User-Agent: kubectl/v1.21.5 (darwin/amd64) kubernetes/aea7bba" 'https://<IP>:6443/api/v1?timeout=32s'
...
I0112 16:04:38.270815   37941 round_trippers.go:435] curl -k -v -XPOST  -H "Accept: application/json, */*" -H "Content-Type: application/json" -H "User-Agent: kubectl/v1.21.5 (darwin/amd64) kubernetes/aea7bba" -H "Authorization: Bearer <masked>" 'https://<IP>:6443/apis/authorization.k8s.io/v1/selfsubjectaccessreviews'
```

## Плагины

У kubectl есть система плагинов. Есть плагин **Krew**, который упрощает установку других плагинов. Как поставить Krew [https://krew.sigs.k8s.io/docs/user-guide/quickstart/](https://krew.sigs.k8s.io/docs/user-guide/quickstart/)

Полезные плагины:

### rakkess / access-matrix

Позволяет посмотреть все полномочия, которые были предоставлены пользователю

```
$ kubectl krew install access-matrix 
$ kubectl access-matrix -n my-project-dev --as jean
```

### kubectl-who-can

[Этот проект](https://github.com/aquasecurity/kubectl-who-can) позволяет нам узнать, какие пользователи могут выполнить определенное действие. Он помогает ответить на вопрос: «Кто может это сделать?».

### rbac-lookup

[Этот проект](https://github.com/reactiveops/rbac-lookup) предоставляет обзор RBAC-правил. Он помогает ответить на вопросы: «В какую роль входят `jean` и `sarah`?», «В какую роль входят все пользователи?», «В какую роль входит вся группа?».&#x20;
