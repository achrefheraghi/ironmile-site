---
layout: default
title: "Security Policy: Code Block Plus for Confluence"
---

Last updated: 2026-11-19

This page describes the security practices of "Code Block Plus for Confluence" (the "app"), provided by Achref Heraghi, trading as Ironmile. For what data the app handles, see the [privacy policy](https://ironmile.dev/code-block-plus/privacy).

## Where data is processed and stored

The app is built on Atlassian Forge and runs on Atlassian's infrastructure. We operate no servers, databases or services for it. Its manifest declares no external permissions, so it sends no data outside Atlassian.

## What is stored and for how long

Your code and the block settings (title, language, line numbers, highlighted lines, wrapping, collapse) are saved inside the macro on your Confluence page. They follow the page, its versions and your site's data residency. We hold no copy. The only data in the app's own Forge storage is a temporary scan token for the import page: page IDs found by a dry run, under a key that includes the admin's account ID. It expires after 30 minutes and holds at most 5000 page IDs. The app writes no analytics or telemetry.

## Encryption

Encryption in transit and at rest is provided by Atlassian's platform. The app adds no storage of its own beyond Forge storage.

## Access and authentication

The app has no accounts and no tokens of its own. The import page requires a Confluence administrator and an active licence. Pages are read as the signed-in user, so page restrictions apply. Saved block settings are treated as untrusted. The app checks their size and values before it shows or exports them. Code is shown as text and never as HTML. The scopes requested are `read:page:confluence`, `read:blogpost:confluence`, `write:page:confluence`, `read:space:confluence`, `read:confluence-user` and `storage:app`.

## Certifications

Ironmile holds no security certifications. This includes ISO 27001 and SOC 2. We do not operate servers or hold customer data, so the app relies on Atlassian's Forge platform. Atlassian publishes its own certifications and reports on its trust site: <https://www.atlassian.com/trust>.

## Access to the app and its code

The app is built and maintained by one person, Achref Heraghi, trading as Ironmile. Two-factor authentication is on for the Atlassian and GitHub accounts used to build and release it. We have no access to the data in your Jira site or its Forge storage.

## Vulnerability management

- We run `npm audit --omit=dev` on the runtime dependencies before a release and leave no Critical or High finding open.
- Fixes for security vulnerabilities follow Atlassian's Marketplace security bugfix policy: <https://developer.atlassian.com/platform/marketplace/security-bugfix-policy/>
- A fix ships as a new app version through Forge.

## Reporting a vulnerability or incident

Email **support@ironmile.dev** with what you found and how to reproduce it. Please do not include real customer data.

If a security incident affects the app, we report it to Atlassian within 48 hours through Marketplace (Security, Report incident). Because we run no servers, an incident would be a flaw in the shipped app. We would respond with a patch release through Forge.

## Related pages

- [Privacy policy](https://ironmile.dev/code-block-plus/privacy)
- [Terms of use (EULA)](https://ironmile.dev/code-block-plus/terms)
- [Support](https://ironmile.dev/code-block-plus/support)

Provided by Achref Heraghi, trading as Ironmile, Tunisia.
