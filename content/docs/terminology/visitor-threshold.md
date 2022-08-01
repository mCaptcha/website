---
title: "Visitor Threshold"
description: "Visitor threshold is used to split traffic into levels. If
the traffic level supersceedes the configured threshold, then mCaptcha will
increase difficulty factor based on the configuration provided."
lead: ""
date: 2022-07-22
lastmod: 2022-07-22 20:17
draft: false
images: []
menu:
  docs:
    parent: "Terminology"
weight: 525
toc: true
---

mCaptcha's variable difficulty factor mechanism requires a website's traffic
statistics be split into levels, so that it can deploy the right
difficulty factor for each level.

Visitor threshold is used to traffic into levels and mCaptcha accepts a
difficulty configuration for each of these levels. When current traffic
exceeds a difficulty factor, mCaptcha will increase the difficulty
factor to the next configured level.

For instance, consider the configuration given below:

- Cool down period: 30 seconds

| Level | Difficulty Factor | Visitor Threshold |
| ----- | ----------------- | ----------------- |
| 1     | 5,000             | 2,000             |
| 2     | 50,000            | 5,000             |
| 3     | 500,000           | 10,000            |
| 4     | 5,000,000         | 15,000            |

If the website sees 2,000 requests in a 30 second window, level 1
difficulty factor(5,000) will be deployed. If the traffic increases to
5,000 requests in a 30 second window, then difficulty factor will be
upgraded to level 2(50,000). Likewise 10,000 and 15,000 requests over 30
seconds will result in difficulty factor being upgraded to 500,000 and
5,000,000 respectively.

Visitor threshold is how mCaptcha determines which difficulty factor
level to deploy. mCaptcha uses leaky bucket algorithm to keep the
visitor threshold constantly updated within the configured cool down
period. So, at any given moment the, the current visitor level will be
the amount of traffic that was served in the cool down period specified.
