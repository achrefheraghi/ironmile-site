---
layout: default
title: "Privacy Policy: Harvest Sync for Jira"
---

Last updated: 2026-10-20

This policy covers the Jira Cloud app "Harvest Sync for Jira" (the "app"), provided by Achref Heraghi, trading as Ironmile ("we", "us"). Contact: support@ironmile.dev.

The app is not affiliated with, endorsed by or sponsored by Harvest or Atlassian. "Harvest" is used only to name the service the app connects to.

## What the app does with data

The app syncs time entries from a user's Harvest account into Jira worklogs. It is built on Atlassian Forge and hosted on Atlassian's infrastructure. It is **not** a "Runs on Atlassian" app, because it sends data to an outside service (Harvest, described below). We do not operate any servers, databases or services for it.

## What is stored

In the app's Forge storage, per Jira site:

- Each connected user's Harvest personal access token and Harvest account ID, in Forge's encrypted secret storage. The token is masked after entry (only the last four characters are shown).
- Per connected user: Jira account ID, Harvest user ID, name and email as reported by Harvest, time zone, connection status, last sync time, last error, and sync bookmarks.
- Project mappings: Jira project ID and key, Harvest project ID and name, default task.
- A link record per synced entry: Harvest entry ID, Jira worklog ID, issue ID and key, a hash of the entry's fields, timestamps and state.
- A sync log: time, user account ID, level, a code and a short message, sometimes with an entry or worklog ID. Log entries are deleted automatically after 30 days.
- Site settings (default start time, backfill days, sync on or off) and short-lived processing locks.

Worklogs themselves live in Jira, in your site. Harvest entries live in Harvest.

## What we collect

Nothing is sent to us. We do not receive, log or read your tokens, time entries, issue data or users' names or email addresses. The app contains no analytics, tracking, advertising or cookies of its own. We use no subprocessors.

## What leaves your site

The app calls one outside host, `api.harvestapp.com` (Harvest's API), using each user's own token. It sends the token and account ID, reads that user's projects, tasks and time entries, and (for timers and entries added from the issue panel) creates, updates or stops Harvest time entries. Those entries can include notes, issue keys, issue URLs and project names. Data processed by Harvest is governed by Harvest's own terms and privacy policy, which are between you and Harvest.

## How the app uses Jira data

With the scopes `read:jira-work`, `write:jira-work`, `read:jira-user` and `storage:app`, the app reads issues, projects, users' time zones and worklogs, and creates, updates and deletes the worklogs it created. The "Hours by epic" project page reads issues and worklogs as the viewing user, only when that user opens it; the totals are shown on screen and are neither stored nor sent outside Atlassian. It writes worklogs as the connected user where Jira allows; otherwise it writes as the app, and only after checking that user's permission on the issue.

## Personal data

The personal data handled is: Jira account IDs, names and emails reported by Harvest, time zones, and the text of time entry notes. It is used only to run the sync. It is held in Forge storage under your Atlassian agreement and handled by Atlassian as described in Atlassian's privacy policy, and by Harvest for the calls above.

## Data location and retention

Forge storage follows Atlassian's Forge hosting. Tokens and user records are kept until the user disconnects or the app is uninstalled. Disconnecting deletes the user's token and pauses their sync. Sync log entries expire after 30 days. Project maps and link records stay until the app is uninstalled. On uninstall, the app deletes every stored Harvest token first, then user records, links, project maps and settings, before Atlassian completes the uninstall. Any data left after that step (for example sync log entries, or records on very large sites) stays in the app's Forge storage for the site, which Atlassian deletes after the uninstall under its Forge data practices. Reinstalling the app does not restore it.

## Licensing

Atlassian handles billing and licence status. We see what Marketplace shows a vendor about sales and licences (such as the site name, licence type and tier), under the Atlassian Marketplace Partner Agreement. We use it for support and accounting only.

## Support requests

If you contact us, we receive your email address and whatever you send. We use it to reply and delete it on request. Please do not send tokens.

## Your rights

For data stored in Jira or Forge storage, contact your Jira site administrator or Atlassian. Each user can disconnect at any time from "My Harvest connection". For data from support requests, write to support@ironmile.dev to ask for access or deletion. To remove Harvest-side data, use Harvest.

## Changes

If the app ever changes what it stores or sends, we will update this policy before the release and describe the change in the release notes. A new external host would also require new admin consent in Jira.

## Contact

Achref Heraghi, trading as Ironmile, support@ironmile.dev, https://ironmile.dev/worklog-sync/support
