# docker-laravel 🐳
こちらの記事を参考に、させていただいています。
[qiita : 最強のLaravel開発環境をDockerを使って構築する【新編集版】](https://qiita.com/ucan-lab/items/5fc1281cd8076c8ac9f4#a-laravel%E3%83%97%E3%83%AD%E3%82%B8%E3%82%A7%E3%82%AF%E3%83%88%E3%82%92%E3%83%90%E3%83%BC%E3%82%B8%E3%83%A7%E3%83%B3%E6%8C%87%E5%AE%9A%E3%81%97%E3%81%A6%E6%96%B0%E8%A6%8F%E4%BD%9C%E6%88%90)

## Introduction

Build a simple laravel development environment with docker-compose.

## Usage
### start with docker
```bash
$ git clone git@github.com:haruu11113/docker-laravel-template.git
$ cd docker-laravel-template
$ cp .env.example .env
-> edit .env
$ make init
```

### start new project
```bash
$ git clone git@github.com:haruu11113/docker-laravel-template.git
$ cd docker-laravel-template
$ make create-project # Install the latest Laravel project
$ make install-recommend-packages # Not required
```

http://localhost

### start clone project

```bash
$ git clone git@github.com:haruu11113/docker-laravel-template.git
$ git cloen <project url: git@github.com:???????????????.git> docker-laravel-template/backend
$ cd docker-laravel-template
$ make init
```

http://localhost

## Tips


## Container structure

```bash
├── app
├── web
└── db
```

### app container

- Base image
  - [php](https://hub.docker.com/_/php):7.4-fpm-buster
  - [composer](https://hub.docker.com/_/composer):2.0

### web container

- Base image
  - [nginx](https://hub.docker.com/_/nginx):1.18-alpine
  - [node](https://hub.docker.com/_/node):14.2-alpine

### db container

- Base image
  - [mysql](https://hub.docker.com/_/mysql):8.0

#### Persistent MySQL Storage

By default, the [named volume](https://docs.docker.com/compose/compose-file/#volumes) is mounted, so MySQL data remains even if the container is destroyed.
If you want to delete MySQL data intentionally, execute the following command.

```bash
$ docker-compose down -v && docker-compose up
```

## License
copyright (c) 2021 haruu11113/docker-laravel-template
https://github.com/haruu11113/docker-laravel-template/blob/main/LICENSE

copyright (c) 2020 ucan-lab/docker-laravel
https://github.com/ucan-lab/docker-laravel/blob/main/LICENSE
