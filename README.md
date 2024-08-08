# Kubernates - bare minimum

В качестве образов для двух контейнеров можно (но не обязательно) использовать уже созданные нами в модулях по Docker образы.

Единственное отличие от приведённого примера — наши образы не представлены в публичном репозитории, поэтому их нужно вручную загрузить внутрь кластера:

```bash
minikube cache add <название локального образа>
```

Кроме того, файл index.php нужно чуть переписать, т. к. у нас адрес до БД и логин/пароль прописаны статически в самом файле. А должны браться из переменных окружения.

Если используете публичные образы, проследите, чтобы образ веб-приложения брал данные для подключения к БД из переменных окружения.

Использовать уже приведённые образы запрещено.

Помимо этого, необходимо сделать таблицу (например, в формате Excel) с инвентаризацией вашего кластера. В кратком виде указать установленное ПО на нодах, количество нод, ОС на нодах, адреса.

## Условия реализации

В качестве ответа предоставьте:

- [ ] все конфигурационные файлы,
- [ ] скриншот из браузера с работающим веб-приложением,
- [ ] вывод команды kubectl get all -o wide,
- [ ] табличку с инвентаризацией.

Результаты работы загрузите на свой GitHub. В качестве ответа приложите ссылку на репозиторий.

## Таблица инвентарищации кластера

| Сущность кубера | Софт | Назначение | Комментарий |
|-----------------+------+------------+-------------|
|                 |      |            |             |

# Commands to run

```bash
# delete if exists
minikube delete -p petr-polyakov-kuber-sf

# create
minikube config set driver virtualbox
minikube kubectl -- get po -A
minikube start --nodes 3 -p petr-polyakov-kuber-sf --driver=virtualbox

# deploynment
minikube config set profile petr-polyakov-kuber-sf
alias kubectl="minikube kubectl --"
kubectl apply -f 1_configmap.yaml,2_mongo-secret.yaml,3_database.yaml,4_webapp.yaml

# addons for dashboard
minikube -p petr-polyakov-kuber-sf addons enable metrics-server

# dashboard
minikube dashboard -p petr-polyakov-kuber-sf &!

# exposing service
minikube service webapp-service
```
