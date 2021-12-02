---
title: "Say hello to mCaptcha"
description: "Introducing mCaptcha, a kickass CAPTCHA systems that gives (DDoS) attackers a run for their money. Oh and UX is great too!"
lead: "We are mCaptcha. We build kickass CAPTCHA systems that give (DDoS) attackers a run for their money. And we do all of this without tracking your users. Oh and did I mention our UX is great?"
date: 2021-05-26
lastmod: 2021-05-26
draft: false
weight: 50
images: ["icon.png"]
contributors: ["Aravinth Manivannan"]
---

At mCaptcha, we believe in digital freedom and privacy and so we built a
[proof-of-work](https://en.wikipedia.org/wiki/Proof_of_work) based
CAPTCHA system that doesn't track. Seriously, no tracking. But that
isn't the killer feature, our system doesn't require the user to
pick cars or ID sidewalks --- our system does it's thing(usually
at the click of a button) and gets out of the way.

## How does it work?
mCaptcha uses SHA256 based proof-of-work(PoW) to rate limit users.

When a user wants to do something on an mCaptcha-protected website,

1. they will have to generate proof-of-work(a bunch of math that will
   takes time to compute) and submit it to mCaptcha.

2. We'll validate the proof:
  - if validation is unsuccessful, they will be prevented from accessing
  the destination website
  - if validation is successful, read on,

3. They will be issued a token that should be submit along with the
   request/form to the destination website.

4. The destination website validates the submitted token with
   mCaptcha before processing the request.

The whole process is automated from the user's point of view. All they
have to do is click on a button to initiate the process.

## Okay, but what about bad actors?

mCaptcha makes interacting with websites (computationally)expensive for
the user. A well-behaving user will experience a slight delay(no delay
when under moderate load to 2-3 seconds when under attack; PoW difficulty is
variable) but if someone wants to hammer your site, they will have to do
more work to send requests than your server you will have to do to respond
to their request.


## Why use mCaptcha?

- **Free software, privacy focused**
- **Seamless** UX --- No more annoying CAPTCHAs!
- **IP address independent:** your users are behind a NAT? We got you covered!
- **Automatic bot throttling**
- **Resistant to replay attacks:** proof-of-work configurations have short lifetimes(30s) and can be used only once. If a user submits a PoW to an already used configuration or an expired one, their proof will be rejected.

## How to migrate?
Our client libraries are mostly compatible with reCAPTCHA and hCaptcha.
A detailed guide will be published soon.

## Our Philosophy
Man has has come so far only because our ancestors chose to
share their knowledge with others. If everything was labeled
intellectual property, we might still be stuck in Stone Age. The idea of
intellectual property is alien to us. For this reason, all of our source
code is freely available(both as in freedom and beers) at [our
GitHub](https://github.com/mCaptcha/).


## Resources

- [guard](https://github.com/mCaptcha/guard) - mCaptcha backend `AGPL`
- [frontend library](https://github.com/mCaptcha/browser) - mCaptcha frontend library. `MIT/APACHE`
