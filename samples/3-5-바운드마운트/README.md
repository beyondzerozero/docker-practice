# 【 ３부: 바인드 마운트 】

## 파일트리

```
$ tree .

.
|-- docker
|   |-- app
|   |   |-- Dockerfile
|   |   |-- mail.ini
|   |   `-- mailrc
|   `-- db
|       |-- Dockerfile
|       |-- init.sql          ← New
|       `-- my.cnf
`-- src
    |-- form.php
    |-- history.php
    |-- index.php
    `-- mail.php
```

## App 컨테이너에 바인드 마운트

```
$ docker container run                        \
    --name app                                \
    --rm                                      \
    --detach                                  \
    --interactive                             \
    --tty                                     \
    --mount type=bind,src=$(pwd)/src,dst=/src \
    docker-practice:app                       \
    php -S 0.0.0.0:8000 -t /src
```

## 볼륨 삭제 및 재작성

```
$ docker volume rm \
    docker-practice-db-volume

$ docker volume create \
    --name docker-practice-db-volume
```

## DB 컨테이너에 바인드 마운트

```
$ docker container run                                                                       \
    --name db                                                                                \
    --rm                                                                                     \
    --detach                                                                                 \
    --platform linux/amd64                                                                   \
    --env MYSQL_ROOT_PASSWORD=rootpassword                                                   \
    --env MYSQL_USER=test                                                                    \
    --env MYSQL_PASSWORD=password                                                            \
    --env MYSQL_DATABASE=event                                                               \
    --mount type=volume,src=docker-practice-db-volume,dst=/var/lib/mysql                     \
    --mount type=bind,src=$(pwd)/docker/db/init.sql,dst=/docker-entrypoint-initdb.d/init.sql \
    docker-practice:db
```
