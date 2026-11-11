---
layout: default
title: "Documentation: Worklog Sync for Harvest"
permalink: /worklog-sync/docs
---

Worklog Sync for Harvest copies your Harvest time entries into Jira Cloud as worklogs, so nobody types hours twice. You can also start a Harvest timer or add a past entry from a Jira issue. The app runs on Atlassian (Forge). It has no servers of its own and talks to one outside host, Harvest's API.

Sync goes one way, from Harvest to Jira. Worklogs you create in Jira are not sent to Harvest.

## What you need

- **Jira Cloud.** A Jira administrator installs the app from the Atlassian Marketplace and accepts its permissions.
- **A Harvest account** for every person whose time should sync. Harvest is billed separately by Harvest.
- **A Harvest personal access token and Account ID** for each of those people. Section "Connect your Harvest account" shows where to find them.
- **Jira administrator rights** for one person, to map Jira projects to Harvest projects and change settings. That person also needs a connected Harvest account, because the Harvest project list comes from it.
- **Time tracking turned on** in each Jira project you sync. Without it, Jira refuses to create worklogs.
- **Permission to work on issues** in the project. Jira checks this before the app writes a worklog for you.

## Install

1. Sign in to Jira as a site administrator.
2. Go to **Apps**, then **Explore more apps**, and search for **Worklog Sync for Harvest**.
3. Select **Get app**, then start the free trial.
4. Read the permissions on the consent screen and accept.

The app asks for four Jira scopes.

| Scope | Why |
|---|---|
| `read:jira-work` | Reads issues, projects and worklogs to match entries and avoid duplicates. |
| `write:jira-work` | Creates, updates and deletes the worklogs the app created. |
| `read:jira-user` | Reads a user's name and time zone. |
| `storage:app` | Keeps tokens, project maps and the sync log in Forge storage. |

The consent screen also lists one outside host, `api.harvestapp.com`. Nothing is sent anywhere else.

## Connect your Harvest account

Every person whose time should sync does this once.

1. In Harvest, open **Harvest ID**, then **Developers**, then **Create new personal access token**. Name it "Jira" and copy the token. Harvest explains this in [its authentication guide](https://help.getharvest.com/api-v2/authentication-api/authentication/authentication/).
2. Copy your **Account ID** from the same Developers page. It is a number, not your email.
3. In Jira, open **Apps**, then **My Harvest connection**.
4. Paste the token into **Personal access token** and the number into **Harvest Account ID**.
5. Select **Test**. A green message says *Connected as* followed by your Harvest name and email.
6. Select **Save**.

After you save, the page shows who you are connected as, the masked token (only the last four characters), your time zone and the time of your last sync. The full token is never shown again.

The first sync reads your Harvest entries from the last 30 days. A Jira administrator can change that window (see Settings below). If you later connect a different Harvest account, the app reads the window again.

## Map Jira projects to Harvest projects (administrators)

Only Jira administrators can open the admin page. Connect your own Harvest account first, so the app can list your Harvest projects.

1. Open **Apps**, then **Worklog Sync**.
2. Open the **Project mapping** tab.
3. Under **Add or update a mapping**, pick the **Jira project**, the **Harvest project** and a **Default task**.
4. Leave **Enabled** on and select **Save mapping**.

Use **Remove** on a row to delete a mapping. A new or newly enabled mapping makes the app look again through each connected person's backfill window, so entries that were waiting for it are picked up on the next run.

The default task is used when someone starts a timer or adds an entry from an issue. The app remembers the last task a person used in each project.

### Admin page tabs

| Tab | What it shows |
|---|---|
| **Overview** | How many people are connected, how many need to reconnect, errors in the last 24 hours, and a table of users with status and last sync. |
| **Project mapping** | The mappings and the form above. |
| **Settings** | **Default start time (HH:mm)**, **Backfill days (1 to 365)** and **Sync enabled**. Select **Save settings**. |
| **Sync log** | Recent log lines and the **Divergent links** list. You can filter by Atlassian account ID and by level (all, info, warn, error). |

Settings defaults: start time 09:00, backfill 30 days, sync on. Harvest entries usually have no start time, so each worklog starts at the default start time in the person's Jira time zone. Turn **Sync enabled** off to pause sync for the whole site.

## Log time from a Jira issue

Open an issue and find the **Harvest timer** panel. It needs a connected account and a mapped project. If you are not connected, the panel says so. If the project is not mapped, it asks you to contact a Jira administrator.

- **Start** starts a Harvest timer on this issue, using the project and task from the mapping. The panel then shows *Timer running since* a time, and a **Stop** button.
- **Stop** stops the timer. The entry is saved in Harvest and queued for Jira.
- **Add a past entry** takes a **Date**, **Hours** and **Notes**. Hours must be more than 0 and at most 24 (decimals such as 1.5 work). The date cannot be in the future, so you can back-date but not forward-date. If you leave Notes empty, the issue key is used.
- **Log to Jira now** queues a sync for you right away.
- **Today on this issue** lists your entries for today with their state: *synced to Jira*, *waiting to sync* or *needs attention*.

Each of these actions writes to Harvest first. The worklog then reaches Jira through the normal sync, usually within seconds to a minute. The panel shows *Queued, syncing in a few seconds*.

## How entries become Jira worklogs

The app checks each connected person's Harvest entries every hour. Nobody needs to start it. If a person has had no Harvest changes for 7 days, the app checks every 4 hours instead, and returns to hourly after the next change or after that person uses the issue panel.

| In Harvest | In Jira |
|---|---|
| A new entry in a mapped project that names an issue | A worklog on that issue, in the person's name where Jira allows. The date is the entry's date in the person's Jira time zone. |
| An edited entry (hours, date, notes or issue) | The worklog is updated. If the entry now names a different mapped issue, the worklog moves there. |
| A deleted entry | The worklog is deleted, but only if the app created it. |
| A running timer | Nothing until you stop it. |

Hours are rounded to whole minutes. Running the sync twice never creates a second worklog for the same entry.

### How an entry finds its issue

1. The issue reference on the entry. Timers and entries made from the issue panel carry it.
2. The entry's existing link, if the entry names no issue.
3. An issue key in the notes, such as `WEB-42`. This works only if that key's Jira project is mapped to the entry's Harvest project.

If none of these match, the entry is listed in the sync log as unmatched. The app never guesses.

### Who owns the worklog

The app writes the worklog as the connected person where Jira allows. If Jira refuses, it writes as the app, after checking that the person has permission on that issue. If that check fails, nothing is written and the entry shows up under **Divergent links**.

### Delete safety

- Only worklogs the app created are ever deleted.
- Harvest does not report deleted entries. Once a day (once a week for a person with no Harvest change for 7 days), the app compares the backfill window with its records and treats missing entries as deleted. It confirms each one with a single lookup and deletes only a small share per run. If it hits the cap, it logs `delete-sweep-capped` and finishes on later days.
- Entries that are locked, billed or approved in Harvest are never changed from Jira.

## The sync log

Administrators see the log under **Apps**, **Worklog Sync**, **Sync log**. Lines are kept for 30 days, and the page shows the most recent ones, newest first.

- An *unmatched* line names the Harvest entry, with its date and an excerpt of its notes. No worklog was created for it.
- **Divergent links** lists entries where the worklog and the entry no longer correspond. The app touched neither. The table gives the Harvest entry, the Jira issue and the reason: for example, the entry now names an issue in an unmapped project, the worklog was not created by this app, the entry is locked or billed, or the person lacks permission on the issue. Fix the cause or edit the worklog or entry by hand. The app deletes nothing for you.

## Hours by epic report

Every Jira project has an **Hours by epic** page in its sidebar. Pick a **From** and **To** date and select **Run**. The default range is the first day of the current month to today.

The table lists each epic with its summary, hours and number of issues. Time logged on stories and sub-tasks counts toward their epic. Issues with no epic go to a *No epic* row. A total line shows the hours across all issues.

The report is read-only and runs as you, so Jira's own permissions decide what it counts. It reads at most 300 issues and has a time limit of about 20 seconds. If it hits either one, it shows *Results truncated*. The totals are then incomplete, so narrow the date range.

It counts all Jira worklogs on those issues, not only the ones this app created.

## Disconnect

Go to **Apps**, then **My Harvest connection**, and select **Disconnect**. This deletes your stored token and pauses your sync. Worklogs already in Jira stay. To connect again, paste a token and Account ID and save.

To cut access from the Harvest side, delete the token in Harvest ID under Developers.

## If a subscription lapses

The admin page and issue panel show a notice that the app is read-only or that sync is paused. Hourly sync stops, and Start, Stop, Add entry, Log to Jira now, Save mapping and Save settings are disabled. Nothing is deleted and nothing is undone. A Jira administrator reactivates the subscription under **Apps**, **Manage apps**. The next hourly run catches up.

## Uninstall

In **Apps**, **Manage apps**, choose Worklog Sync for Harvest and select **Uninstall**. Sync stops. Worklogs already in Jira remain, because they are ordinary Jira worklogs. Entries in Harvest are not touched.

On uninstall, the app first deletes every person's Harvest token, then its user records, links, project mappings and settings. This cleanup is time-limited, so on a very large site some records may remain in the app's Forge storage, which Atlassian deletes after the uninstall. Reinstalling does not bring the data back.

## Where your data is stored

Everything is stored in Atlassian Forge storage for your Jira site. We run no servers or databases and receive no data from the app.

- **Harvest token:** in Forge's encrypted secret store, one per person. It is never shown again after saving, only its last four characters. It is deleted on Disconnect and on uninstall.
- **Records:** project mappings, settings, a link between each synced Harvest entry and its Jira worklog, and a sync log kept 30 days.
- **Outside host:** `api.harvestapp.com`, called with each person's own token. The app has no analytics or telemetry.

Details are in the [Privacy policy](https://ironmile.dev/worklog-sync/privacy).

## Pricing and licensing

$0.50 per user per month, from the first user. There is no free tier. Paid plans include a 30-day free trial. Atlassian bills by your Jira site's user tier, and you can see the current price in the Marketplace pricing tab. You also need a Harvest plan, which Harvest bills separately.

## Limits

- Harvest to Jira only. Worklogs created in Jira are not sent to Harvest.
- Sync is hourly, not instant (every 4 hours for a person with no Harvest change for 7 days). Panel actions are faster.
- Running timers do not sync until you stop them.
- Entries that name no issue and match no rule are not synced.
- One task per project from the mapping, or the task the person last used there. There is no choice by issue type.
- The backfill window is 1 to 365 days. Entries older than that are not read.
- Back-dated entries from the panel: hours above 0 up to 24, no future dates. Notes up to 2,000 characters.
- Hours by epic reads up to 300 issues.
- The app does not use OAuth or "Sign in with Harvest". It uses a personal access token.

## Troubleshooting

| Symptom | What to do |
|---|---|
| **Test** says the token or Account ID is wrong | Copy both again from Harvest ID, Developers. The Account ID is a number, not your email. |
| The panel or Overview says you need to reconnect | Harvest rejected the token, probably because it was revoked. Create a new token and save it again. |
| An entry is missing in Jira | Look for it in the Sync log. Usually the Harvest project is not mapped, or the notes have no issue key, or the key's project is mapped to a different Harvest project. Add the key to the notes, for example `WEB-42 fix redirect`, and save the entry in Harvest, or fix the mapping. |
| The panel says the project is not mapped | Ask a Jira administrator to add a mapping for it. |
| A divergent link appears | See the sync log section above for the reasons, then fix the cause or edit by hand. |
| Jira says time tracking is off | Turn on time tracking for the project. |
| A panel action did not show up in Jira | Wait a minute, then select **Log to Jira now**. The hourly run will catch up in any case. |
| The log shows `delete-sweep-capped` | The app refused to delete more than its safety cap in one run. Check that entries were not deleted in Harvest by mistake. The rest is handled on later days. |
| The worklog date is off by a day | The date uses your Jira profile time zone. Fix it in your Atlassian profile. The app refreshes it daily. |
| The admin page or panel says the app is read-only | The subscription is inactive. A Jira administrator can activate it under **Manage apps**. |

If the problem continues, email the log line's code and the issue key. Do not send your token.

## Help

- [Support](https://ironmile.dev/worklog-sync/support): email **support@ironmile.dev**. We reply by email.
- [Privacy policy](https://ironmile.dev/worklog-sync/privacy)
- [Terms of use (EULA)](https://ironmile.dev/worklog-sync/terms)

Worklog Sync for Harvest is not affiliated with or endorsed by Harvest (Forecast). "Harvest" is used only to name the service the app connects to.

Provided by Achref Heraghi, trading as Ironmile, Tunisia.
