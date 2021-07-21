---
title: "Deploy bare metal"
description: "Bare metal deployment is tedious, most of this will be automated with a script in the future."
lead: "Bare metal deployment is tedious, most of this will be automated with a script in the future."
date: 2021-07-21 14:49
lastmod: 2021-07-21 14:49
draft: false
images: []
menu:
  docs:
    parent: "self-hosted"
weight: 120
toc: true
---

### 2. Configure

mcaptcha is highly configurable.

Configuration is applied/merged in the following order:

1. path to configuration file passed in via `MCAPTCHA_CONFIG`
2. `./config/default.toml`
3. `/etc/mcaptcha/config.toml`
4. environment variables.



### 1. Install postgres if you don't have it already.
For Debian based distributions:
```bash
sudo apt install postgres
```

### 2. Create new user for running `mcaptcha`

```bash
$ sudo useradd -b /srv -m -s /usr/bin/zsh mcaptcha
```

### 3. Create new user in Postgres

```bash
$ sudo -iu postgres # switch to `postgres` user
$ psql
postgres=#  CREATE USER mcaptcha WITH PASSWORD 'my super long password and yes you need single quote`;
$  createdb -O mcaptcha mcaptcha # create db 'mcaptcha' with 'mcaptcha' as owner
```

### 4. Install and load [`mCaptcha/cache`](https://github.com/mCaptcha/cache) module:

See [`mCaptcha/cache`](https://github.com/mCaptcha/cache) for more
details.

### 4. Build `mcaptcha`

To build `mcaptcha`, you need the following dependencies:

1. rust
2. node(`v14.16.0`)
3. yarn(JavaScript package manager)
4. make

## How to build

1. Install Cargo using [rustup](https://rustup.rs/) with:

```bash
$ curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

2. Install node(`v14.16.0`)

3. Install yarn(JavaScript package manager)

4. Build with make:

```bash
$ make dev-env && \
	make release
```

### 5. Install package:

```bash
$ sudo cp ./target/release/mcaptcha /usr/bin/ && \
	mkdir sudo /etc/mcaptcha && \
	sudo cp config/default.toml /etc/mcaptcha/config.toml
```

### 6. Systemd service configuration:

1. Copy the following to `/etc/systemd/system/mcaptcha.service`:

```systemd
[Unit]
Description=mCaptcha: a CAPTCHA system that gives attackers a run for their money

[Service]
Type=simple
User=mcaptcha
ExecStart=/usr/bin/mcaptcha
Restart=on-failure
RestartSec=1
SuccessExitStatus=3 4
RestartForceExitStatus=3 4
SystemCallArchitectures=native
MemoryDenyWriteExecute=true
NoNewPrivileges=true
Environment="RUST_LOG=info"

[Unit]
After=sound.target
Wants=network-online.target
Wants=network-online.target
Requires=postgresql.service
After=syslog.target

[Install]
WantedBy=multi-user.target
```

2. Enable service:

```bash
$ sudo systemctl daemon-reload && \
	sudo systemctl enable mcaptcha && \ # Auto startup during boot
	sudo systemctl start mcaptcha
``
```
