---
layout: default
title: "Security Policy: Text & Announcement Gadget for Jira"
---

Last updated: 2026-11-19

This page describes the security practices of "Text & Announcement Gadget for Jira" (the "app"), provided by Achref Heraghi, trading as Ironmile. For what data the app handles, see the [privacy policy](https://ironmile.dev/text-gadget/privacy).

## Where data is processed and stored

The app is built on Atlassian Forge and runs on Atlassian's infrastructure ("Runs on Atlassian"). We operate no servers, databases or services for it. It has no backend functions and makes no calls outside Atlassian. Its manifest declares no external permissions and requests no Jira or product API scopes.

## What is stored and for how long

Only the gadget's configuration: the announcement text (Markdown), style, preset, optional start and end dates, and display toggles. Jira stores it as a property of the dashboard item, so it follows your Jira site's data residency. It stays until the gadget is removed from the dashboard. We hold no copy. The app stores no user IDs or email addresses and writes no logs or analytics.

## Encryption

Encryption in transit and at rest is provided by Atlassian's platform. The app adds no storage of its own.

## Access and authentication

The app has no accounts and no tokens of its own. Who can view or edit a dashboard is decided by Jira's own permissions. Markdown is shown as UI Kit components only. Raw HTML in the text is shown as plain text and is never run.

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

- [Privacy policy](https://ironmile.dev/text-gadget/privacy)
- [Terms of use (EULA)](https://ironmile.dev/text-gadget/terms)
- [Support](https://ironmile.dev/text-gadget/support)

Provided by Achref Heraghi, trading as Ironmile, Tunisia.
