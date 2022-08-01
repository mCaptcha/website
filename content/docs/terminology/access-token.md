---
title: "Access token"
description: "mCaptcha implements leaky bucket algorithm to measure
current traffic levels. Cooldown period specifies the leak or the time
after which a visitor addition is decremented."
lead: ""
date: 2022-07-22
lastmod: 2022-07-22 20:17
draft: false
images: []
menu:
  docs:
    parent: "Terminology"
weight: 521
toc: true
---

When a visitor solves the CAPTCHA and sends their solution to an
mCaptcha instance, the solution will be verified for correctness. If the
solution is correct, mCaptcha will return a single use access token.

This access token should be attached to the visitor's requited to the
protected service and the protected service should validity of the
access token with the mCaptcha instance and only allow access to
protected resource if the access token is valid.

## Validate access token:

```bash
curl --location --request POST 'https://mcaptcha.example.net/api/v1/pow/siteverify' \
  --header 'Content-Type: application/json' \
  --data-raw '{
    "token": "replace this with the access token presented by visitor",
    "key": "replace this with the sitekey associated with the CAPTCHA"
    "secret": "replace this with mCaptcha account secret, available in settings"
  }'
```
