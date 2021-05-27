---
title: "Security"
description: "mCaptcha security policies."
date: 2021-03-10
lastmod: 2021-03-10 20:48
draft: false
identifiers: "security"
layout: "security"
toc: true
lastEdited: true
---

Security is at the heart of mCaptcha. If you find any discrepancies in
our software(see listing on our [GitHub](https://github.com/mCaptcha),
[services available](#scope))

## Rules:

### Before you start

- Check the list of domains that are in scope for security research
  and the list of targets for useful information for getting started.

- Check the list of bugs that have been classified as ineligible.

- Check our changelog(in our GitHub repositories) for recently launched
  features.

- Never attempt non-technical attacks such as social engineering,
  phishing, or physical attacks against our employees, users, or
  infrastructure.

When in doubt, contact
me([@realaravinth](/contributors/aravinth-manivannan/)) at
[realaravinth@batense.net](mailto:realaravinth@batsense.net).

### Performing your research

- Do not impact other users with your testing, this includes testing
  vulnerabilities with CAPTCHA credentials and account credentials
  of accounts you do not own. If you are attempting to find an
  authorization bypass, you must use accounts you own.

- The following are never allowed for research. We may
  suspend your mCaptcha account for:

  - Performing distributed denial of service (DDoS) or other volumetric
    attacks. Sure, we are a DDoS protection organisation, but with sufficient
    resources and motivation, it is possible to take us down. For this
    reason, we request you to not hurt us.

  - Spamming content Large-scale vulnerability scanners, scrapers, or
    automated tools which produce excessive amounts of traffic.

    Note: We do allow the use of automated tools so long as they do
    not produce excessive amounts of traffic. For example, running
    one nmap scan against one host is allowed, but sending 65,000
    requests in two minutes using Burp Suite Intruder is excessive.

- Researching denial-of-service attacks is allowed only if you follow
  these rules:

  - There are no limits for researching denial of service
    vulnerabilities against your own instance of mCaptcha server. **We
    strongly recommend/prefer this method for researching denial of
    service issues.**

  - If you choose to test on mCaptcha proper (i.e.
    [https://mcaptcha.org](https://mcaptcha.org) or [https://mcaptcha.io](https://mcaptcha.io)):
    - Research must be performed using credentials you own.
    - Stop immediately if you believe you have affected the
      availability of our services. Don’t worry about demonstrating
      the full impact of your vulnerability, our team
      will be able to determine the impact.

### Handling personally identifiable information (PII)

- Personally identifying information (PII) includes:

  - legal and/or full names
  - names or usernames combined with other identifiers like phone numbers or email addresses
  - health or financial information (including insurance information, social security numbers, etc.)
  - information about political or religious affiliations
  - information about race, ethnicity, sexual orientation, gender, or other identifying information that could be used for discriminatory purposes

- Do not intentionally access others’ PII. If you suspect a service
  provides access to PII, limit queries to your own personal
  information.

- Report the vulnerability immediately and do not attempt to access any
  other data. We will assess the scope and impact of the PII exposure.

- Limit the amount of data returned from services. For SQL injection,
  for example, limit the number of rows returned

- You must delete all your local, stored, or cached copies of data
  containing PII as soon as possible. We may ask you to sign a
  certificate of deletion and confidentiality agreement regarding the
  exact information you accessed. We may ask you for the usernames and
  IP addresses used during your testing to assess the impact of the
  vulnerability.

### Reporting your vulnerability

- Reports must include written instructions for reproducing the
  vulnerability.

- When reporting vulnerabilities you must keep all information on
  restricted to email correspondence with us([see below for
  contact](#contact)). If you believe the bug to be critical, please use
  encryption.

- Do not post information to
  video-sharing or pastebin sites.

- For vulnerabilities involving personally identifiable information,
  please explain the kind of PII you believe is exposed and limit the
  amount of PII data included in your bug report. For textual
  information and screenshots, please only include redacted data in your
  bug report.

- During the course of an investigation, it may take time to resolve
  the issue you have reported. We ask that you refrain from publicly
  disclosing details regarding an issue you’ve reported until the fix has
  been publicly made available.

### Legal safe harbor:

We currently don't have any legal policies in place but rest assured
that as long as your research adheres to the above rules, your security
research and vulnerability disclosure activities are considered as
"authorized".

A detailed policy based on this sentiment is in the works.

## Scope:

mCaptcha runs a number of services. Only domains listed below are are
eligible for security research. Any mCaptcha-owned domains not listed
below are _not_ in scope and are _not_ covered by our [legal safe
harbor](./#legal-safe-harbor)

### mcaptcha.org

- mcaptcha.org
- demo.mcaptcha.org
- demo2.mcaptcha.org

### mcaptcha.io

- mcaptcha.io

## Contact

### Email
[realaravinth@batense.net](mailto:realaravinth@batsense.net).

### GPG Key

[Click here to download key](/aravinth.asc)

```GPG
-----BEGIN PGP PUBLIC KEY BLOCK-----

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
=gpUQ
-----END PGP PUBLIC KEY BLOCK-----
```
