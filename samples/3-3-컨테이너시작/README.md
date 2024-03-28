# 【 ３부: 컨테이너실행 】

## App 컨테이너시작

```
$ docker container run  \
    --name app          \
    --rm                \
    docker-practice:app \
    php -S 0.0.0.0:8000
```

## DB 컨테이너시작

```
$ docker container run                     \
    --name db                              \
    --rm                                   \
    --platform linux/amd64                 \
    --env MYSQL_ROOT_PASSWORD=rootpassword \
    --env MYSQL_USER=test                  \
    --env MYSQL_PASSWORD=password          \
    --env MYSQL_DATABASE=event             \
    docker-practice:db`
```

## Mail 컨테이너시작

```
$ docker container run     \
    --name mail            \
    --rm                   \
    --platform linux/amd64 \
    mailhog/mailhog:v1.0.1
```
