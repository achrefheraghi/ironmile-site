---
layout: default
title: "Security Policy: Worklog Sync for Harvest"
---

Last updated: 2026-11-19

This page describes the security practices of "Worklog Sync for Harvest" (the "app"), provided by Achref Heraghi, trading as Ironmile. For what data the app handles, see the [privacy policy](https://ironmile.dev/worklog-sync/privacy).

## Where data is processed and stored

The app is built on Atlassian Forge and hosted on Atlassian's infrastructure. We operate no servers, databases or services for it. It is not a "Runs on Atlassian" app, because it calls one outside host: `api.harvestapp.com` (Harvest's API), using each user's own token. It sends the token and account ID, reads that user's projects, tasks and time entries, and creates, updates or stops Harvest time entries made from the issue panel. Data held by Harvest is under Harvest's own terms and privacy policy.

## What is stored and for how long

Stored in the app's Forge storage for your site: each connected user's Harvest token and account ID, user and project records, a record per synced entry, a sync log and site settings. Sync log entries are deleted after 30 days. Tokens and user records stay until the user disconnects or the app is uninstalled. Project maps and link records stay until uninstall. On uninstall the app deletes every token first, then the other records. Anything left (such as log entries, or records on very large sites) stays in Forge storage until Atlassian removes it after the uninstall. The app writes no analytics or telemetry. A weekly job reports stored account IDs through Atlassian's personal data reporting API and erases the data of accounts that Atlassian reports as closed.

## Encryption

Each Harvest token is kept in Forge's encrypted secret store, not in regular storage and not in logs. It is shown masked, with only the last four characters visible. Disconnecting deletes the token. Encryption in transit and at rest is provided by Atlassian's platform.

## Access and authentication

There is no site-wide token: each user connects their own Harvest account. Admin actions need Jira administrator permission, checked on the server. Worklogs are read and written as the connected user. If Jira does not allow that, the app writes as itself, but only after checking that the user has permission on the issue. If the check fails, nothing is written. The scopes requested are `read:jira-work`, `write:jira-work`, `read:jira-user`, `storage:app` and `report:personal-data`. If Harvest rejects a token, the app stops that user's sync and shows it as needing a new connection.

## Certifications

Ironmile holds no security certifications. This includes ISO 27001 and SOC 2. We operate no servers and hold no customer data outside Atlassian, so the app relies on Atlassian's Forge platform. Atlassian publishes its own certifications and reports on its trust site: <https://www.atlassian.com/trust>.

## Access to the app and its code

The app is built and maintained by one person, Achref Heraghi, trading as Ironmile. Two-factor authentication is on for the Atlassian and GitHub accounts used to build and release it. We have no access to the data in your Jira site or its Forge storage.

## Vulnerability management

- Fixes for security vulnerabilities follow Atlassian's Marketplace security bugfix policy: <https://developer.atlassian.com/platform/marketplace/security-bugfix-policy/>
- A fix ships as a new app version through Forge.

## Reporting a vulnerability or incident

Email **support@ironmile.dev** with what you found and how to reproduce it. Please do not include real customer data.

If a security incident affects the app, we report it to Atlassian within 48 hours through Marketplace (Security, Report incident). Because we run no servers, an incident would be a flaw in the shipped app. We would respond with a patch release through Forge and, if a Harvest token may be exposed, ask affected users to revoke it in Harvest and reconnect.

## Related pages

- [Privacy policy](https://ironmile.dev/worklog-sync/privacy)
- [Terms of use (EULA)](https://ironmile.dev/worklog-sync/terms)
- [Support](https://ironmile.dev/worklog-sync/support)

Provided by Achref Heraghi, trading as Ironmile, Tunisia.
