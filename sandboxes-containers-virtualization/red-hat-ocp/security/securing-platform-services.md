# Securing Platform Services

Для взаимодействия с OpenShift Container Pllatform все пользователи должны быть аутентифицированы в кластере. В OpenShift встроен OAuth сервер для авторизации по токенам.

OpenShift API Server — 0.0.0.0:**6443**. API сервер не может быть сконфигурирован на другой порт! Не должен быть доступен извне кластера.

Еще может быть доступна openshift web console (но она как правило за паролем (kubeadmin/somepassword) или вообще отключена (best practise)): [https://console-openshift-console.apps.demo1.example.com](https://console-openshift-console.apps.demo1.openshift4-beta-abcorp.com)
