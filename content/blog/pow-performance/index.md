---
title: "PoW performance"
description: "PoW performance of native and WASM implementations. Does
the native implementation have and edge over the WASM library?"
lead: "We are mCaptcha. We build kickass CAPTCHA systems that give (DDoS) attackers a run for their money. And we do all of this without tracking your users. Oh and did I mention our UX is great?"
date: 2021-09-01
lastmod: 2021-09-01
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
usually use browsers to access a website.

I wanted to see how much of an advantage a native program would have
over our WASM library.

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
| 500000     | 0m0.220s | 0m0.197s | 0m0.006s |
| 1000000    | 0m0.203s | 0m0.203s | 0m0.000s |
| 1500000    | 0m0.198s | 0m0.198s | 0m0.000s |
| 2000000    | 0m0.203s | 0m0.203s | 0m0.000s |
| 2500000    | 0m0.758s | 0m0.752s | 0m0.003s |
| 3000000    | 0m0.776s | 0m0.769s | 0m0.003s |
| 3500000    | 0m2.010s | 0m1.998s | 0m0.000s |
| 4000000    | 0m2.038s | 0m2.033s | 0m0.003s |
| 4500000    | 0m2.014s | 0m2.013s | 0m0.000s |

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
to run to completion in under 5 seconds is impressive!

So, in my opinion, native implementation is only slightly faster than
the WASM library and for all intents and purposes, this shouldn't matter
much.

---

P.S Work is underway to benchmark multiple platforms. A detailed report
will be published when that data is available.

For this post, I asked some of my friends to run the tests on their
computers. The results slightly varied but even the slowest case
generated proof for 4500000 difficulty(the highest in this test), in under
15 seconds!
