---
title: "pow_sha256"
description: "API documenttion for PoW Library used in mCaptcha"
lead: ""
date: 2021-03-11
lastmod: 2021-04-01 22:57
draft: false
images: []
menu:
  docs:
    parent: "API"
weight: 553
toc: true
---

Rust crate which generates SHA256 Proofs of Work on serializable datatypes.

This is a fork of the [`pow` library](https://github.com/bddap/pow) by
[@robkorn](https://github.com/robkorn/pow_sha256)) with some new
additions. Primary of these being:

- PoW datatype now offers a constructor
- Salt is no longer hard coded into the library, users can provide
  unique salts.

Other small changes have also been included of various importance but
mostly just stylistic/ease of use improvements.

## Versions

- [master-branch](https://mcaptcha.github.io/pow_sha256/pow_sha256/index.html)
- [0.2.1](/api-docs/pow_sha256/0.2.1/pow_sha256/index.html)
- [0.2.0](/api-docs/pow_sha256/0.2.0/pow_sha256/index.html)
- [0.1.0](/api-docs/pow_sha256/0.1.0/pow_sha256/index.html)

## Changelog

Changelog is available at the project's
[repository](https://github.com/mCaptcha/pow_sha256/blob/master/CHANGELOG.md)
