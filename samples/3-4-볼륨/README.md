# 【 ３부: 볼륨 】

## 볼륨 만들기

```
$ docker volume create \
    --name docker-practice-db-volume
```

## DB 콘테이너에 볼륨 마운트

```
$ docker container run                                                   \
    --name db                                                            \
    --rm                                                                 \
    --detach                                                             \
    --platform linux/amd64                                               \
    --env MYSQL_ROOT_PASSWORD=rootpassword                               \
    --env MYSQL_USER=test                                                \
    --env MYSQL_PASSWORD=password                                        \
    --env MYSQL_DATABASE=event                                           \
    --mount type=volume,src=docker-practice-db-volume,dst=/var/lib/mysql \
    docker-practice:db
```
