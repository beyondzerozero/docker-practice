# 【 ３부: 이미지빌드 】

## 파일트리

```
$ tree .

.
|-- docker
|   |-- app
|   |   |-- Dockerfile        ← New
|   |   |-- mail.ini          ← New
|   |   `-- mailrc            ← New
|   `-- db
|       |-- Dockerfile        ← New
|       `-- my.cnf            ← New
`-- src
    |-- form.php
    |-- history.php
    |-- index.php
    `-- mail.php
```

## App 이미지 빌드

```
$ docker image build             \
    --tag docker-practice:app    \
    --file docker/app/Dockerfile \
    .
```

## DB 이미지 빌드

```
$ docker image build            \
    --tag docker-practice:db    \
    --file docker/db/Dockerfile \
    .
```
