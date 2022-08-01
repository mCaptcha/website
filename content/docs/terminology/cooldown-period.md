---
title: "Cooldown Period"
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
weight: 522
toc: true
---

mCaptcha implements leaky bucket algorithm to measure
current traffic levels. Cooldown period specifies the leak or the time
after which a visitor addition is decremented.

For instance, if initial traffic level is 0 and a user visits one
second later, the traffic level will be incremented to 1. Now, if the
cooldown period is set to 30 seconds, the traffic level will be
decremented after 30 seconds. So after 30 seconds, the traffic level will
go from 1 to 0.

## Easy Mode: Default cooldown

When configuring mCaptcha in [easy Mode](/docs/introduction/configuring-difficulty-factor/#easy-option), the default cooldown period is set to 30 seconds.
