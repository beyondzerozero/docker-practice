# 【 ３부: Docker Compose 】

## Docker Compose 서비스 시작

```
$ docker compose up \
    --detach        \
    --build
```

## Docker Compose 서비스 중단

```
$ docker compose down
```

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
|       |-- init.sql
|       `-- my.cnf
|-- docker-compose.yaml
`-- src
    |-- form.php
    |-- history.php
    |-- index.php
    `-- mail.php
```
