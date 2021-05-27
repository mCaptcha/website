---
title: "Security"
description: "mCaptcha security policies."
date: 2021-03-10
lastmod: 2021-03-10 20:48
draft: false
identifiers: "security"
layout: "security"
toc: true
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
  restricted to email correspondence with us. Do not post information to
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
