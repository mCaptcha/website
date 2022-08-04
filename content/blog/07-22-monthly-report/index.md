---
title: "July, 2022: Monthly Report"
description: "Codeberg is trying you mCaptcha, Gitea is getting mCaptcha support, mCaptcha supports MariaDB, I've applied for NLnet and Open Tech Fund, documentation is updated: tutorials and glossary is added and glue libraries have new releases."
lead: "We are mCaptcha. We build kickass CAPTCHA systems that give (DDoS) attackers a run for their money. And we do all of this without tracking your users. Oh and did I mention our UX is great?"
date: 2022-08-04
lastmod: 2022-08-04
draft: false
weight: 50
images: ["icon.png"]
contributors: ["Aravinth Manivannan"]
---

Hello and welcome to the July, 2022 monthly report!

## TL;DR

_Codeberg is trying you mCaptcha, Gitea is getting mCaptcha support,
mCaptcha supports MariaDB, I've applied for NLnet and Open Tech Fund,
documentation is updated: tutorials and glossary is added and glue libraries
have new releases._

## Codeberg is deploying mCaptcha

Codeberg is committed to trying out mCaptcha to make their platform more
accessible: they currently use a text-based CAPTCHA, which will be
replaced by mCaptcha. The decision was finalized after I presented
mCaptcha to them at a meeting their organized. Please see
[here](https://batsense.net/talks/codeberg-introducing-mcaptcha/) for
slides.

## Gitea gets mCaptcha support

[@Gusted](https://gusted.xyz) from Codeberg is working on integrating
mCaptcha in Gitea so that Codeberg can deploy it. Please see
[here](https://github.com/go-gitea/gitea/pull/20458) for related the
pull request.

This project is yet to see usage, so we are venturing into uncharted
territory: should you face issues with either deploying or
integrating mCaptcha, please feel free [to reach out](/community).

## mCaptcha supports MariaDB:

Codeberg uses MariaDB. To facilitate Codeberg deployment, I implemented
support for MariaDB. [The work done in
May, 2022](https://mcaptcha.org/blog/may-2022-monthly-report#refactor) made
implementing support easy. Support for MariaDB is first class in
mCaptcha: automatic testing exist to run tests with both Postgres and
MariaDB, so I expect things to be stable.

## Applied for Funding: NLnet and Open Tech Fund

I've applied for NLnet and Open Tech Fund[0], Please find the
applications
[here](https://forum.forgefriends.org/t/mcaptcha-nlnet-grant-application-august-2022/830/3)
and
[here](https://forum.forgefriends.org/t/mcaptcha-nlnet-grant-application-august-2022/830/3)
respectively.

If funding is granted:

1. I'll be able to work full-time for a year at the rate of 2,000 EUR/month
2. We'll have a dedicated build server
3. We'll have funds to run a DDoS test to gauge mCaptcha's effectiveness

## Documentation updates

mCaptcha docs over the months have become inconsistent and incorrect. I
cleaned up some of the mess and added [a
tutorial](/docs/introduction/installing-captcha/) to help folks install
mCaptcha on their website. The docs also gets [a
glossary](/docs/terminology/access-token/), which contain explanations
to mCaptcha jargon.

## New releases: glue libraries

`0.1.0-alpha-2` for
[vanilla](https://www.npmjs.com/package/@mcaptcha/vanilla-glue),
[react](https://www.npmjs.com/package/@mcaptcha/react-glue) and
[svelte](https://www.npmjs.com/package/@mcaptcha/svelte-glue) glue
libraries were released. They now hand over widget sizing to the client
code([associated PR](https://github.com/mCaptcha/glue/pull/12)).

## Footnotes

- [0]: Special thanks to
  [@humantech](https://mastodon.social/@humanetech) for his thoughtful
  reviews and to [@dachary](https://dachary.org) for pointing me towards
  OTF.
