---
title: "Database and cache"
description: "mCaptcha server requires dependencies like a Postgres
database and a Redis cache"
lead: "mCaptcha server requires dependencies like a Postgres
database and a Redis cache"
date: 2021-07-21 14:49
lastmod: 2021-07-21 14:49
draft: false
images: []
menu:
  docs:
    parent: "Self-Hosted"
weight: 534
toc: true
---

## Notes

### Database

- Database migrations are baked into the server binary so don't worry
about them.

- When compiling from source, unset database configuration(comment out
database configuration/ `unset` relevant environment variables).
`mCaptcha` uses [`sqlx`](https://crates.io/crates/sqlx) database client
library which checks SQL queries at compile time. So if you are starting
with a fresh database without migrations applied, compilation will fail.

### Redis

- Redis is an optional dependency. Currently, the non-Redis configuration
doesn't persist CAPTCHA heat. So if there's a systems failure, CAPTCHA
heat will be reset and visitor count will start from 0. For small
installations, this should post a problem as heat is short lived and is
reset anyways at cool down period.

- mCaptcha uses a custom Redis module called
[cache](https://github.com/mCaptcha/cache) to overcome some of Redis'
limitations.


## Instructions

Once again, there are two ways to go about this:

1. Docker
2. Bare metal

### Docker

### Database

Download and run Postgres

```bash
docker create --name mcaptcha-postgres \
  -e POSTGRES_PASSWORD=<database-password> \
  -p 5432:5432 \
  postgres && docker start mcaptcha-postgres
```

### Redis

```bash
docker create --name mcaptcha-cache \
  -p 6379:6379 \
  mcaptcha/cache && docker start mcaptcha-cache
```

See [mCaptcha/cache](https://github.com/mCaptcha/cache) for more
details.

### 1. Install Postgres if you don't have it already.

For Debian based distributions:

```bash
sudo apt install postgres
```

### 2. Create new user for running `mCaptcha`

```bash
$ sudo useradd -b /srv -m -s /usr/bin/bash mcaptcha
```

### 3. Create new user in Postgres

```bash
$ sudo -iu postgres # switch to `postgres` user
$ psql
postgres=#  CREATE USER mcaptcha WITH PASSWORD 'my super long password and yes you need single quote';
$  createdb -O mcaptcha mcaptcha # create db 'mcaptcha' with 'mcaptcha' as owner
```

### 4. Install [`mCaptcha/cache`](https://github.com/mCaptcha/cache)

See [`mCaptcha/cache`](https://github.com/mCaptcha/cache) for more
details.
