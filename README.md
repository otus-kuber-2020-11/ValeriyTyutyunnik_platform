# ValeriyTyutyunnik_platform

## ДЗ №1.

1. Знакомство с кубером на примере локального развертывания minikube
2. Проверено востановление кластера после удаления контейнеров из ВМ

```
minikube ssh
docker ps
docker rm -f $(docker ps -a -q)
```

и при удаление подов

```
kubectl get pods -n kube-system
kubectl delete pod --all -n kube-system
```

Кластер полностью востановился в течении нескольких секунд.

Востановление компонентов apiserver, etcd, controller, scheduler выполняется агентом на ноде kubelet.
Kubelet проверяет состояние компонентов и восстанавливает компоненты при сбое автоматически.

Другие компоненты управляются контроллером в зависимости от шаблона.

Pod core-dns управляется шаблоном контроллера ReplicaSet
Pod kube-proxy управляется шаблоном контроллера DaemonSet

3. Создан контейнер с запуском веб сервиса allien/web:0.1, контейнер добавлен в под
