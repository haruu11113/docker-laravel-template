# docker-laravel 🐳

## Introduction

Build a simple laravel development environment with docker-compose.

## Usage

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
