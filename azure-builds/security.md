---
layout: default
title: "Security Policy: Pipeline Builds & Deployments via Webhook for Jira"
---

Last updated: 2026-11-19

This page describes the security practices of "Pipeline Builds & Deployments via Webhook for Jira" (the "app"), provided by Achref Heraghi, trading as Ironmile. For what data the app handles, see the [privacy policy](https://ironmile.dev/azure-builds/privacy).

## Where data is processed and stored

The app is built on Atlassian Forge and hosted on Atlassian's infrastructure. We operate no servers, databases or services for it. Its manifest declares no external permissions. Azure DevOps sends events in to a web address that belongs to your Jira site. The app never calls Azure DevOps. Its only outbound calls are to your own Jira site.

## What is stored and for how long

In Forge storage for your site: a shared secret, settings, small caches that link commits, pull requests and builds to Jira issue keys, and a short event log. Commit, pull request and build caches expire after 90 days. Held stage results expire after 7 days. Event log entries expire after 7 days. The secret and settings stay until replaced or until the app is uninstalled. The app drops names and email addresses of people from events before it stores anything. When commits, branches and pull requests are sent to Jira (an admin toggle, on by default), the commit author and the pull request creator and reviewers, with their names and emails, are passed straight on to Jira in the same request. If Jira is unavailable, a failed delivery waits in the Forge queue for up to about 40 minutes and is then dropped. Jira holds the build and deployment records the app sends, and removes them when the app is uninstalled. The app writes no analytics or telemetry.

## Encryption

The shared secret is stored as a Forge secret. Encryption in transit and at rest is provided by Atlassian's platform. Azure DevOps requires HTTPS for webhooks that use Basic authentication.

## Access and authentication

The webhook address is public, as Forge requires, and cannot be guessed. The app accepts a request only when it carries the shared secret: a 256-bit random value, sent as the Basic auth password or in the `X-Webhook-Secret` header. The secret is never accepted in the address and never logged. A wrong or missing secret gets a 401 reply and nothing is stored. Requests over 1 MiB are rejected. A Jira admin can rotate the secret, with the old one valid for 24 hours, or revoke all old secrets at once. The admin page can only be used by Jira administrators. The scopes requested are `write:build-info:jira`, `write:deployment-info:jira`, `write:dev-info:jira`, `delete:dev-info:jira`, `read:jira-work` and `storage:app`.

## Certifications

Ironmile holds no security certifications. This includes ISO 27001 and SOC 2. We operate no servers and hold no customer data outside Atlassian, so the app relies on Atlassian's Forge platform. Atlassian publishes its own certifications and reports on its trust site: <https://www.atlassian.com/trust>.

## Access to the app and its code

The app is built and maintained by one person, Achref Heraghi, trading as Ironmile. Two-factor authentication is on for the Atlassian and GitHub accounts used to build and release it. We have no access to the data in your Jira site or its Forge storage.

## Vulnerability management

- Fixes for security vulnerabilities follow Atlassian's Marketplace security bugfix policy: <https://developer.atlassian.com/platform/marketplace/security-bugfix-policy/>
- A fix ships as a new app version through Forge.

## Reporting a vulnerability or incident

Email **support@ironmile.dev** with what you found and how to reproduce it. Please do not include real customer data.

If a security incident affects the app, we report it to Atlassian within 48 hours through Marketplace (Security, Report incident). Because we run no servers, an incident would be a flaw in the shipped app. We would respond with a patch release through Forge and, if the shared secret may be exposed, ask admins to rotate it and revoke old secrets on the app's admin page.

## Related pages

- [Privacy policy](https://ironmile.dev/azure-builds/privacy)
- [Terms of use (EULA)](https://ironmile.dev/azure-builds/terms)
- [Support](https://ironmile.dev/azure-builds/support)

Provided by Achref Heraghi, trading as Ironmile, Tunisia.
