---
title: "May, 2022: Monthly Report"
description: "Python bindings to mCaptcha PoW, DDoS effectiveness measurement, major refactoring to prepare for support for other databases, We also tried to test its DoS defence effectiveness, and some exciting news regarding managed hosting!"
lead: "We are mCaptcha. We build kickass CAPTCHA systems that give (DDoS) attackers a run for their money. And we do all of this without tracking your users. Oh and did I mention our UX is great?"
date: 2022-06-10
lastmod: 2022-06-10
draft: false
weight: 50
images: ["icon.png"]
contributors: ["Aravinth Manivannan"]
---

Hello and welcome to the May 2022 edition of the monthly report!

mCaptcha, for a while was showing all the signs of a dead project:
no commits on the repositories and no monthly updates. But the project
is far from dead!

## Python bindings to [mCaptcha PoW](https://github.com/mCaptcha/pow_sha256/)

[pow_py](https://github.com/mCaptcha/pow_py) contains bindings to
[pow_sha256](https://github.com/mCaptcha/pow_sha256), the
[proof-of-work](https://en.wikipedia.org/wiki/Proof_of_work) library
that mCaptcha uses. For the uninitiated, the bindings allow for python
programs to automatically solve mCaptcha.

So if you are writing a script to do some chore on your favourite
website that is protected by mCaptcha, you can now solve the mCaptcha
automatically from within the program.

Here's an example:

```python
import os

import mcaptcha_pow_py
import requests

# get the sitekey that is used in the mCaptcha protected form
SITEKEY = os.getenv("MCAPTCHA_CAPTCHA_SITEKEY")
# the hostname of the mCaptcha instance that the form is using
MCAPTCHA_HOST = os.getenv("MCAPTCHA_CAPTCHA_HOST")


GET_CONFIG_ROUTE = f"{MCAPTCHA_HOST}/api/v1/pow/config"
VERIFY_POW_ROUTE = f"{MCAPTCHA_HOST}/api/v1/pow/verify"

def solve_captcha():

    # get challenge configuration
    key = {"key": sitekey}
    challenge_config = requests.post(GET_CONFIG_ROUTE, json=key)
    challenge_config = challenge_config.json()

    # extract configuration data
    config = mcaptcha_pow_py.PoWConfig(challenge_config["salt"])
    pow_string = challenge_config["string"]
    pow_difficulty_factor = challenge_config["difficulty_factor"]

    # generate work
    work = config.work(pow_string, pow_difficulty_factor)

    # verify PoW
    proof = {
        "key": SITEKEY,
        "nonce": work.nonce,
        "result": work.result,
        "string": challenge_config["string"],
    }
    resp = requests.post(VERIFY_POW_ROUTE, json=proof)
    resp = resp.json()

    # extract verification token
    token = resp["token"]

    return token


token = solve_captcha()
data = {
    "username": "me",
    "password": "superlongpassword",
    "confirm_password": "superlongpassword",
    "mcaptcha__token": token,
}
response = requests.post("/mCaptcha-protected-form", data=data)
```

This could be missed for building DDoS bots(more on that
[here](#measuring-ddos-protection-effectiveness)) but this could also be
used to make CAPTCHA solving automated within screen readers and other
accessibility devices!

## Measuring DDoS protection effectiveness

Proof-of-work has historically been a good method to achieve rate
limiting but how much attack can it, specifically mCaptcha's
implementation, withstand when compared to an unprotected endpoint? To
find out, we used the recently created Python bindings to the mCaptcha
PoW library, the excellent load testing tool,
[locust](https://locust.io) and wrote
[mCaptcha/dos](https://github.com/mCaptcha/dos)!

[VIT AP](https://vitap.ac.in) kindly permitted me, @realaravinth, to use their network
security lab for setting up a isolated, contained testing environment to
mount a DDoS attack on a [test
server](https://github.com/mCaptcha/dos/tree/master/rust-server/demo-server)
instance.

The initial topology consisted of one mCaptcha instance, one DDoS demo
server, one locust node running in leader configuration and six locust
nodes running in follower configuration. I was authorised to use the
netsec lab for three days, which unfortunately wasn't enough to go
finish running the experiment. [Dr. Sibi Chakkaravarthy
Sethuraman](https://sibichakkaravarthy.github.io/) has kindly offered to
arrange authorisation to use the netsec lab once again in July 2022,
during which I hope to finish running the experiment

Special thanks to [ackr-8](http://ackr8.com/) and
[alan2000alex](https://github.com/alan2000alex) for help with setting up
infrastructure of the experiment.

## Refactor

mCaptcha underwent a major refactor during the month of May: We re-wrote
and cleaned up all database-related stuff for higher flexibility
and generally good architecture. This refactor lays the foundation 
for implementing support for alternate database software
programs(we currently support PostgreSQL only).

## mCaptcha is now on the Fediverse

We recently joined the Fediverse on a
[GoToSocial](https://docs.gotosocial.org/) instance run by
@realaravinth. We'll soon be deleting our Twitter account in favour of
the Fediverse account.

**Fediverse account:**
[@mCaptcha@batsense.net](https://gts.batsense.net/@mcaptcha)

## Generic hosting

I, @realaravinth, have been busy with [ForgeFlux](https://forgeflux.org)
and [Hostea](https://hostea.org) --- both of which are [software
forge](<https://en.wikipedia.org/wiki/Forge_(software)>) related and so
when usable, will mostly improve the Free Software ecosystem. Hostea is
a project that aims to create a libre software development ecosystem and
provide managed hosting for the same. The project is [built by a
horizontal community](https://forum.hostea.org/t/a-guide-to-hostea-governance/57), which allows for multiple service providers who
adhere to the Hostea policies to operate
under the Hostea umbrella --- essentially allowing for the creation of
smaller, highly localised cooperatives.

Cooperatives are interesting, and we believe that mCaptcha, too, can
benefit from such an architecture as it will prevent any one party from
single-handedly sabotaging the project. The experience gained from
Hostea will be reused in providing managed hosting for mCaptcha.

By the end of this year, mCaptcha will reorganise into a horizontal
community and adopt [radical transparency](https://en.wikipedia.org/wiki/Radical_transparency#Radical_corporate_transparency) to improve trust and
reliability of the project

> P.S: I, realaravinth, would do it sooner but I'm a little busy right
> now, so if someone is interested to help out do reach out and so that
> we could do it sooner!

In context of mCaptcha, radical transparency will include all decisions
publicly made, funding and expenses publicly documented, and all
collaborations, too, publicly documented. This of course doesn't imply
that private, personally identifiable information(addresses and phone
numbers, for instance) will be publicly disclosed. Such information will
be redacted and published.
