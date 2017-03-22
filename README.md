# PHP for pro-cli

This is the PHP project structure for [pro-cli](https://github.com/chriha/pro-cli) PHP projects.

The virtual host points to `./src/public`.

## Usage

Copy the `.env.example` to `.env`.

```bash
cp .env.example .env
```

## Environment variables

All variables for `docker-compose{.env}.yml` are stored in `.env.example` resp. `.env`.

## docker compose

Each project has its `docker-compose.yml` which should not be touched as it will be overwritten as soon as the project structure gets updated. Instead you should create your own docker-compose file according to the `env` in `pro-cli.json`. For example, if you set the `env` to `local`, **pro-cli** will look for `docker-compose.local.yml`. So you can cherry pick the services you need for your environment.

Example for `docker-compose.local.yml` that only uses the **web** and **db** service for its environment:

```yaml
version: '2'

services:
  web:
    extends:
      file: docker-compose.yml
      service: db
    volumes:
      - ./src/app-name:/var/www
    links:
      - db
      - redis
      - rabbit
      - mailcatcher
    env_file:
      - ./src/app-name/.env
  db:
    extends:
      file: docker-compose.yml
      service: db

networks:
  def_network:
    driver: "bridge"
```

## Used docker images
- [docker-images](https://github.com/chriha/docker-images)
