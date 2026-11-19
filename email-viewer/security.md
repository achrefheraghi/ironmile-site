---
layout: default
title: "Security Policy: Email Attachment Viewer for Jira"
---

Last updated: 2026-11-19

This page describes the security practices of "Email Attachment Viewer for Jira" (the "app"), provided by Achref Heraghi, trading as Ironmile. For what data the app handles, see the [privacy policy](https://ironmile.dev/email-viewer/privacy).

## Where data is processed and stored

The app is built on Atlassian Forge and runs on Atlassian's infrastructure ("Runs on Atlassian"). We operate no servers, databases or services for it. Attachments are fetched and read inside the Forge function. The email is cleaned in your browser before it is shown. The manifest declares no external permissions, so no data goes outside Atlassian.

## What is stored and for how long

Nothing. The app has no database, no cache and no Forge storage. Its logs hold one line per call with the function name, status, duration, sizes and counts. They never hold email content, subjects, addresses, file names or account IDs. There is nothing to delete when the app is uninstalled.

## Encryption

Encryption in transit and at rest is provided by Atlassian's platform. The app stores nothing of its own.

## Access and authentication

The app has no accounts and no tokens of its own. The only scope is `read:jira-work`, and the app never writes to Jira. Every Jira call is made as the signed-in user, so Jira permissions apply. A requested attachment must belong to the issue being viewed. The app checks its input before any Jira call. Files over 25 MiB are not opened. Email HTML is cleaned with DOMPurify and shown in a sandboxed frame that does not allow scripts. Remote images are blocked.

## Certifications

Ironmile holds no security certifications. This includes ISO 27001 and SOC 2. We operate no servers and hold no customer data outside Atlassian, so the app relies on Atlassian's Forge platform. Atlassian publishes its own certifications and reports on its trust site: <https://www.atlassian.com/trust>.

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

- [Privacy policy](https://ironmile.dev/email-viewer/privacy)
- [Terms of use (EULA)](https://ironmile.dev/email-viewer/terms)
- [Support](https://ironmile.dev/email-viewer/support)

Provided by Achref Heraghi, trading as Ironmile, Tunisia.
