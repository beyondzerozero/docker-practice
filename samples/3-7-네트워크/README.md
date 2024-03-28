# 【 ３부: 네트워크】

## 네트워크 만들기

```
$ docker network create \
    docker-practice-network
```

## App 컨테이너를 네트워크에 연결

```
$ docker container run                        \
    --name app                                \
    --rm                                      \
    --detach                                  \
    --mount type=bind,src=$(pwd)/src,dst=/src \
    --publish 18000:8000                      \
    --network docker-practice-network         \
    docker-practice:app                       \
    php -S 0.0.0.0:8000 -t /src
```

## DB 컨테이너를 네트워크에 연결하여 별칭 설정

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
    --network docker-practice-network                                                        \
    --network-alias db                                                                       \
    docker-practice:db
```

## Mail 컨테이너를 네트워크에 연결하여 별칭 설정

```
$ docker container run                \
    --name mail                       \
    --rm                              \
    --detach                          \
    --platform linux/amd64            \
    --publish 18025:8025              \
    --network docker-practice-network \
    --network-alias mail              \
    mailhog/mailhog:v1.0.1
```

## App 컨테이너에서 DB컨테이너로의 연결 설정

변경 파일

- [src/history.php](src/history.php#L7-L10)
- [src/mail.php](src/mail.php#L41-L47)

```php
$host = 'db';
$port = '3306';
$database = 'event';
$dsn = sprintf('mysql:host=%s; port=%s; dbname=%s;', $host, $port, $database);

$username = 'test';
$password = 'password';
```

반영 명령

없음

## App 컨테이너에서 Mail컨테이너로의 연결 설정

변경 파일

- [docker/app/mailrc](docker/app/mailrc#L2-L3)

```txt
account default
host mail
port 1025
from "service@d-prac.test"
```

반영 명령

```
$ docker image build             \
    --tag docker-practice:app    \
    --file docker/app/Dockerfile \
    .
```
