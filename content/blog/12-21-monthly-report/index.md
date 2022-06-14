---
title: "December, 2021: Monthly Report"
description: "New features, improved accessibility and software
integrations"
lead: "We are mCaptcha. We build kickass CAPTCHA systems that give (DDoS) attackers a run for their money. And we do all of this without tracking your users. Oh and did I mention our UX is great?"
date: 2021-12-23
lastmod: 2021-12-23
draft: false
weight: 50
images: ["icon.png"]
contributors: ["Aravinth Manivannan"]
---

Hello and welcome to the first edition of the monthly report!

I believe free software like mCaptcha is critical to a healthy internet
but being a one-person show, there's hardly any accountability in the
way software is built. I hope, through monthly reports, I can explain
the logic and intentions behind decisions taken in the development
process.

This month, the following things were accomplished:

## 1. Full LibreJS Compliance

The CAPTCHA widget and the admin dashboard are 100% LibreJS compliant!

{{%
    img src="librejs-dashboard.jpg"
    alt="Screenshot of mCaptcha admin dashboard with GNU LibreJS extension's report in frame.LibreJS reports that all scripts in this webpage are accepted(and hence free software) and are licensed under the AGPL license."
    caption="LibreJS report of the dashboard webpage"
%}}

{{%
    img src="librejs-widget.jpg"
    alt="Screenshot of mCaptcha client-side widget(I'm-not-a-robot widget) with GNU LibreJS extension's report in frame. LibreJS reports that all scripts in this webpage are accepted(and hence free software) and are licensed under the X11(aka MIT license). It should also detect the Apache licensing but I probably botched it up."
    caption="LibreJS report of the CAPTCHA widget webpage"
%}}

## 2. JavaScript PolyFill

mCaptcha relied on a WebAssembly(WASM) port of the proof-of-work
algorithm used in mCaptcha. This meanth browsers without WASM support
couldn't process CAPTCHAs. This month, [a pure JavaScript(TypeScript,
technically) implementation
](https://github.com/mCaptcha/pow_sha256-polyfill) was released to
overcome this limitation.

## 3. Integration libraries for Vanilla JS, React and Svelte:

To make migration from existing CAPTCHA deployments to mCaptha,
integration libraries for [Vanilla
JS](https://www.npmjs.com/package/@mcaptcha/vanilla-glue), [React
Js](https://www.npmjs.com/package/@mcaptcha/react-glue) and
[Svelte](https://www.npmjs.com/package/@mcaptcha/svelte-glue) with
similar APIs very similar to that of Google's reCAPTCHA and Cloudflare's
hCaptcha.

- Source code: [mCaptcha/glue](https://github.com/mCaptcha/glue)

# 4. Beginner friendly CAPTCHA configuration options.

The original configuration panel offers a comprehensive but daunting
task for folks that are justgetting started with mCaptcha.
{{%
    img src="captcha-advanced-config.jpg"
    alt="Screenshot of mCaptcha admin dashboard CAPTCHA creation form with advance configuration options"
    caption="CAPTCHA creation with advance configuration options"
%}}


A new CAPTCHA creation format is rolled out which generates a
configuration from familiar metrics like average, peak and traffic that
took the user's website down.

{{%
    img src="easy-config.jpg"
    alt="Screenshot of mCaptcha admin dashboard CAPTCHA creation form with easy configuration options"
    caption="CAPTCHA creation with easy configuration options"
%}}

Of course, the advance option is available and can always be swished to
at any moment!
