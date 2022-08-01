---
title: "Troubleshooting"
description: "Solutions to common problems."
lead: "Solutions to common problems."
date: 2021-07-21 15:48
lastmod: 2021-07-21 15:48
draft: false
images: []
menu:
  docs:
    parent: "Help"
weight: 541
toc: true
---

## Q: I just setup an instance but I am unable to login

mCaptcha by default is configured to server at `localhost` hostname. If
the instance is deployed at another hostname, please try setting
`MCAPTCHA_SERVER_DOMAIN` environment variable to the hostname at which
your instance is deployed or setting the equivalent in config.toml:

```toml
[server]
domain=mydomain
```
