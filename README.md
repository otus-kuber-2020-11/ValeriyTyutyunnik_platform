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

4. Создан контейнер allien/fronend:0.0.1 приложения Hipster Shop

5. Сгенерирован манифест с помощью kubectr
```
kubectl run frontend --image allien/frontend:0.0.1 --restart=Never --dry-run -o yaml > frontend-pod.yaml
```

6. Добавлен манифест frontend-pod-healthy.yaml, в котором контейнер запускается в статусе RUNNING. Проблема - не хватало переменных окружения для старта контейнера. Добавлены полуфейковые переменные в манифест

## kubernetes-security ДЗ-3
- Создание и выдача ролей.
### task-01
- Выдача роли admin в рамках кластера сервис-аккаунту bob
- Сервис аккаунт dave без доступа к кластеру
### task-2
- Создан namespace prometheus, и сервис аккаунт carol в ns prometheus
- Всем service account в ns prometheus выданы права на get/list/watch в отношении Pods кластера
### task-03
Создан namespace dev, в рамках которого:
- Создан Service account jane c ролью admin в рамках dev
- Создан Service account ken с ролью view в рамках dev
