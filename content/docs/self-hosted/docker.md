---
title: "Docker"
description: "Deploy mCaptcha with docker"
lead: "Deploy mCaptcha with docker"
date: 2021-07-21 15:14
lastmod: 2021-07-21 15:14
draft: false
images: []
menu:
  docs:
    parent: "Self-Hosted"
weight: 110
toc: true
---

## Docker

### 1. Configure

mcaptcha is highly configurable.

Configuration is applied/merged in the following order:

1. path to configuration file passed in via `MCAPTCHA_CONFIG`
2. `./config/default.toml`
3. `/etc/mcaptcha/config.toml`
4. environment variables.

See
[CONFIGURATION.md](https://github.com/mCaptcha/mCaptcha/tree/master/docs/CONFIGURATION.md)
for configurable options.

### 2. Run image

If you have already have a Postgres instance running, then:

```bash
docker run -p <host-machine-port>:<port-in-configuration-file> \
	--add-host=database:<database-ip-addrss> \
	-e RUST_LOG=debug \
	-e DATABASE_URL="postgres://<db-user>:<db-password>@database:<db-port>/<db-name>" \
	mcaptcha/mcaptcha:latest
```

If you don't have a Postgres instance running, you can either install
one using a package manager or launch one with docker. A [docker-compose
configuration]('../docker-compose.yml) is available that will launch both
a database instance mcaptcha instance.

## With docker-compose

1. Follow steps above to build docker image.

2. Set database password [docker-compose configuration]('../docker-compose.yml).

3. Launch network

```bash
docker-compose up -d
```
