---
layout: default
title: "Privacy Policy: Builds & Deployments from Azure Pipelines for Jira"
---

Last updated: 2026-10-20

This policy covers the Jira Cloud app "Builds & Deployments from Azure Pipelines for Jira" (the "app"), provided by Achref Heraghi, trading as Ironmile ("we", "us"). Contact: support@ironmile.dev. The app is not affiliated with, endorsed by or sponsored by Microsoft. "Azure DevOps" and "Azure Pipelines" are Microsoft trademarks, used only to say what the app works with.

## What the app does with data

The app is built on Atlassian Forge and hosted on Atlassian's infrastructure (we are still confirming its "Runs on Atlassian" eligibility; it declares no external permissions). We do not operate any servers, databases or services for it. Azure DevOps sends events (builds, stage results, releases, code pushes, pull requests) to a private web address that belongs to your Jira site. The app reads them and sends build and deployment records to Jira.

## What is stored

In the app's Forge storage, inside your Jira site's installation:

- A shared secret, created by the app, stored as a Forge secret. It is shown once to a Jira admin.
- Settings: environment mapping rows, Jira project keys, three on/off options.
- Small caches that link commits, pull requests, builds and stage results to Jira issue keys: issue keys, commit hashes, branch names, stage names, links to Azure DevOps pages, and timestamps. They expire after 90 days (commit, pull request and build caches) or 7 days (held stage results).
- An event log entry per logged event: time, event type, outcome, up to 4 issue keys, and a short detail (up to 80 characters). Entries expire after 7 days. Routine events are logged one in ten.
- After a rotation, up to 3 previous secrets, each for 24 hours (as a Forge secret), unless an admin revokes them.
- A licence status copy and a "log cleared" timestamp.

The dashboard gadget stores nothing in the app: its settings (a project key and a filter) are saved by Jira with the dashboard, and it searches issues as the person viewing it.

Jira holds the build, deployment and development records the app sends: build and pipeline names, numbers, states, links, branch names, commit hashes, issue keys, environment names and timestamps. Jira deletes them when the app is uninstalled.

When commits, branches and pull requests are sent to Jira (an admin toggle, on by default), the app passes the commit author name and email, the pull request creator's and reviewers' names and emails, and the commit messages and titles from the Azure DevOps event straight on to Jira in the same request. Nothing of this is stored by the app beyond the delivery itself: if Jira is unavailable, the failed delivery waits in the Forge queue for up to about 40 minutes (five retries) and is then dropped. The app drops identity objects (names and email addresses of people who requested, pushed or authored) from events before it stores anything. We have no access to this data.

## Permissions

Scopes requested in the manifest: `write:build-info:jira`, `write:deployment-info:jira`, `write:dev-info:jira`, `delete:dev-info:jira`, `read:jira-work` and `storage:app`. No external permissions are declared.

## What we collect

Nothing. We do not receive, log or read your events, records, users' names or email addresses. The app contains no analytics, tracking, advertising or cookies of its own.

## What leaves your site

Nothing. The app makes no calls to servers outside Atlassian and sends no data to us or to third parties. Its only outbound calls are to your own Jira site. We use no subprocessors. The data path is one way: Azure DevOps to the app, and the app to Jira. The app never calls Azure DevOps and holds no Microsoft credentials.

## Who can send data to the webhook

The webhook address is public on the internet, as Forge requires, and is unguessable. The app accepts a request only when it carries the shared secret. A request with a wrong or missing secret is rejected; the app writes one line to its Forge logs (outcome only, never the request body) and stores nothing.

## Personal data

Branch names, commit messages read for issue keys, and pull request titles may contain text people chose to write. The app keeps only issue keys and identifiers from them, not the message text. Anything personal in Jira records is held by Jira under your Atlassian agreement and handled by Atlassian as described in Atlassian's privacy policy. The app does not store user account IDs, names or email addresses.

## Data location and retention

Data stays where your Jira site's data resides (Jira) and in Atlassian's Forge hosting (app storage). Retention is as stated above. Uninstalling the app removes the records it sent to Jira immediately; Atlassian's deletion practices apply to app storage. Reinstalling creates a new secret and a new address.

## Licensing

Atlassian handles billing and licence status. The app reads the licence state from Atlassian to know whether a subscription is active. We see what Marketplace shows a vendor about sales and licences (such as the site name, licence type and tier), under the Atlassian Marketplace Partner Agreement. We use it for support and accounting only.

## Support requests

If you contact us, we receive your email address and whatever you send. We use it to reply and delete it on request. Please do not send secrets, webhook URLs or build content you consider sensitive.

## Your rights

For data stored in Jira, contact your Jira site administrator or Atlassian. For data from support requests, write to support@ironmile.dev to ask for access or deletion.

## Changes

If the app ever changes what it stores or sends, we will update this policy before the release and describe the change in the release notes. Adding an external connection, or a new permission, would also require new admin consent in Jira.

## Contact

Achref Heraghi, trading as Ironmile, support@ironmile.dev, https://ironmile.dev/azure-builds/support
