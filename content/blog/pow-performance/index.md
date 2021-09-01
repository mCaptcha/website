---
title: "PoW performance"
description: "PoW performance of native and WASM implementations. Does
the native implementation have and edge over the WASM library?"
lead: "We are mCaptcha. We build kickass CAPTCHA systems that gives (DDoS) attackers a run for their money. And we do all of this without tracking your users. Oh and did I mention our UX is great?"
date: 2021-05-26
lastmod: 2021-05-26
draft: false
weight: 50
images: ["icon.png"]
contributors: ["Aravinth Manivannan"]
---

mCaptcha uses a
[proof-of-work(PoW)](https://en.wikipedia.org/wiki/Proof_of_work) mechanism
to rate limit users or potential bots. In order for this to be
effective, the PoW should be configured properly. The difficulty
requirement can't be too high, as it could cause accessibility issues on
the client-side while at the same time, it shouldn't be too low, as it
wouldn't offer proper protection against bots.

Malicious bots(the ones that wreak havoc), run native code which is
capable of running in a multi-threaded context. This creates an unfair
advantage for crackers using these bots over legitimate users, who
usually | browsers to access a website. I wanted to see how much of
an advantage a native program would have over our WASM library.

## Benchmark tools

So I wrote these to compare native and WASM performances:

- Browser benchmark: [https://mCaptcha.github.io/benches](https://mCaptcha.github.io/benches)
- Native benchmark: [mCaptcha/cli managed by scripts/bench.sh](https://github.com/mCaptcha/cli/blob/master/scripts/bench.sh)

{{< alert icon="⭐" text="Feel free to reproduce the results!" >}}

## Results

The tests were run on my development machine featuring an Intel Core
i7-9750h.

### Native

| Difficulty | Real     | User     | Sys      |
| ---------- | -------- | -------- | -------- |
| 50000      | 0m0.040s | 0m0.040s | 0m0.000s |
| 300000     | 0m0.122s | 0m0.122s | 0m0.000s |
| 550000     | 0m0.124s | 0m0.119s | 0m0.003s |
| 800000     | 0m0.123s | 0m0.118s | 0m0.003s |
| 1050000    | 0m0.933s | 0m0.932s | 0m0.000s |
| 1300000    | 0m1.227s | -        | 0m0.007s |
| 1550000    | 0m1.260s | 0m1.256s | 0m0.003s |
| 1800000    | 0m1.243s | 0m1.242s | 0m0.000s |
| 2050000    | 0m2.524s | 0m2.510s | 0m0.000s |
| 2300000    | 0m2.545s | 0m2.543s | 0m0.000s |
| 2550000    | 0m2.561s | 0m2.551s | 0m0.004s |
| 2800000    | 0m2.555s | 0m2.540s | 0m0.006s |
| 3050000    | 0m2.513s | 0m2.508s | 0m0.000s |
| 3300000    | 0m2.484s | 0m2.481s | 0m0.000s |
| 3550000    | 0m2.643s | 0m2.642s | 0m0.000s |
| 3800000    | 0m2.663s | 0m2.661s | 0m0.000s |
| 4050000    | 0m2.663s | 0m2.660s | 0m0.000s |
| 4300000    | 0m2.689s | 0m2.683s | 0m0.004s |
| 4550000    | 0m2.688s | 0m2.686s | 0m0.000s |
| 4800000    | 0m2.517s | 0m2.509s | 0m0.003s |

### Browser

I ran the tests on both Firefox and Chromium to compare results

### Firefox

- **User Agent:** `Mozilla/5.0 (X11; Linux x86_64; rv:91.0) Gecko/20100101 Firefox/91.0`
- **Hardware concurrency:** 12

| Difficulty | Duration(in ms) |
| ---------- | --------------- |
| 500000     | 401             |
| 1000000    | 413             |
| 1500000    | 398             |
| 2000000    | 394             |
| 2500000    | 1495            |
| 3000000    | 1556            |
| 3500000    | 3971            |
| 4000000    | 4235            |
| 4500000    | 4116            |

> To be fair, my Firefox installation is loaded with a gazillion
> extensions while the Chromium instance is clean, as I don't use it
> much

#### Chromium

- **User Agent:** `Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/92.0.4515.159 Safari/537.36`
- **Hardware concurrency:** 12

| Difficulty | Duration(in ms)    |
| ---------- | ------------------ |
| 500000     | 399.40000000037253 |
| 1000000    | 354.6000000014901  |
| 1500000    | 351.19999999925494 |
| 2000000    | 353.80000000074506 |
| 2500000    | 1337.800000000745  |
| 3000000    | 1311.199999999255  |
| 3500000    | 3417.5999999996275 |
| 4000000    | 3488.800000000745  |
| 4500000    | 3458.2999999988824 |

## Conclusion

At the highest difficulty factor, the native implementation was a almost second
faster than the WASM library. But the fact that both of them were able
to run to completion in under 5 seconds is impressive.

So, in my opinion, native implementation is only slightly faster than
the WASM library and for all intents and purposes, this shouldn't matter
much.
