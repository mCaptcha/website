---
title: "Browser libraries"
description: "API documenttion for mCaptcha WASM library"
lead: ""
date: 2021-03-11
lastmod: 2021-03-11 10:27
draft: false
images: []
menu:
  docs:
    parent: "API"
weight: 110
toc: true
---

The browser part of mCaptcha is divided into three components.

- Glue code
- Widget program
- Proof-of-Work libraries(WebAssembly and JavaScript polyfill)

## Glue code

This is the code that links mCaptcha with your website's frontend code.
It creates an `iframe` containing the mCaptcha widget and injects the
received verification proof token into a hidden input field.

Support is available for various frameworks, see
[`mCaptcha/glue`](https://github.com/mCaptcha/glue) for the full list.

For frameworks without official support, a low-level library,
[`@mcaptcha/core-glue`](https://www.npmjs.com/package/@mcaptcha/core-glue),
can be used to implement support.

## Widget Program

This part is served by the mCaptcha backend. It fetches PoW config from
the backend, generates proof and submits it for verification. If
verification is successful, it sends a message containing the
verification proof token to the parent window, assuming it's loaded as
an `iframe`.

- Source code:
  [`mCaptcha/mCaptcha/templates/widget`](https://github.com/mCaptcha/mCaptcha/tree/master/templates/widget)

WebAssembly library which generates Proofs of Work for mCaptcha systems.

## Proof-of-Work(PoW) library

WebAssembly bindings([`mCaptcha/pow_wasm`](https://github.com/mCaptcha/pow_wasm)) are available for the main rust library([`mCaptcha/pow_sha256`](https://github.com/mCaptcha/pow_sha256)).

For browsers without support WebAssembly, a
polyfill([`pow_sha256-polyfill`](https://github.com/mCaptcha/pow_sha256-polyfill))
is available.
