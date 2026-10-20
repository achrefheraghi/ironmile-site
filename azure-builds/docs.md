---
layout: default
title: "Documentation: Builds & Deployments from Azure Pipelines for Jira"
permalink: /azure-builds/docs
---

Azure DevOps pushes events to a private webhook URL on your Jira site. The app shows them on Jira issues: builds in the Development panel, deployments in the Deployments view and Releases. No Azure token, PAT or OAuth app is ever shared with Jira, and the app never calls Azure DevOps.

This app is not affiliated with, endorsed by or sponsored by Microsoft. "Azure DevOps" and "Azure Pipelines" are Microsoft trademarks, used here only to say which product the app works with.

## What you need

- Jira Cloud, and a Jira admin to install the app and open its admin page.
- An Azure DevOps project where you have the **Edit subscriptions** permission (Project Administrators or Project Collection Administrators).

That is all. You do not need to link an Azure subscription, buy a paid Azure DevOps tier or create an app registration. Service hooks cost nothing in Azure DevOps. Repeat steps 2 to 4 for each Azure DevOps project. The service hook must use HTTPS; the webhook URL from Jira already does.

## Set up in 7 steps

1. **Copy the webhook URL and secret.** In Jira open **Apps > Builds from Azure Pipelines** (the admin page; it needs Jira admin). Copy the *Webhook URL*.
   - **The secret is shown once.** The first time an admin opens the page, the app creates the secret and shows it in a green box: "New secret. Copy it now, it is shown only once." Copy it, then press **I have copied it**. After that the page shows it masked.
   - Missed it? Press **Regenerate secret** and choose **Revoke old secrets now** (no hooks use it yet), then copy the new value. To change a secret that hooks already use, see *Rotate the secret* below.
2. **Open service hooks.** In Azure DevOps open your project, then **Project settings** (bottom left) **> General > Service hooks > Create subscription** (green plus). Choose **Web Hooks > Next**.
3. **Builds: "Build completed".** Trigger on this type of event = **Build completed**; leave Build pipeline = *[Any]* and Build status = *[Any]*. **Next**. Action settings:
   - *URL* = the webhook URL.
   - *Basic authentication username* = `jira`.
   - *Basic authentication password* = the secret.
   - *Resource details to send* = **All**; *Messages to send* = **None**; *Detailed messages to send* = **None**.
   
   Press **Test** (expect a success response), then **Finish**.
4. **Deployments and code events.** Create more subscriptions with the same Action settings, for these triggers:
   - **Run stage state changed** (YAML pipeline deployments).
   - **Release deployment completed** (classic release pipelines only).
   - **Code pushed**, **Pull request created**, **Pull request updated** and **Pull request merged or updated** (commits, branches and pull requests in the Development panel, and better issue key matching for builds; pick a repository or leave *[Any]*). Create all four, with *Resource details to send* = **All**. Pull request status (Open, Merged, Declined) follows the *updated* and *merged* events, so skip neither.

   The Web Hooks consumer has no signature option, which is why the app uses Basic auth over HTTPS. Commits (issue key in the message), branches (key in the name) and pull requests (key in the title or source branch) without a key are not sent. A deleted branch is removed from Jira. Azure DevOps includes at most 20 commits per push. To stop sending them, switch off *Send commits, branches and pull requests* on the admin page (default on); the code events then only help find issue keys.
5. **Put the Jira issue key** (for example `ABC-123`) in branch names, commit messages or pull request titles. Builds and deployments with no key are not sent to Jira; they appear as `no-keys` in the event log.
6. **Check the settings** on the admin page and press **Save settings** if you change anything.
7. **Watch the event log.** *Recent events* on the same page lists the last 25 events with a status label. Builds then appear in the issue's Development panel, and deployments in the Deployments view and Releases.


## How issue keys are found

Jira does not guess which issue a build belongs to. The app reads the Jira key (for example `ABC-123`) from the branch name, the commit messages and the pull request title that Azure DevOps sends. Builds and deployments with no key are not sent; the event log says `no-keys`. Commits (key in the message), branches (key in the name) and pull requests (key in the title or source branch) that carry a key are sent to the Development panel, with the pull request status Open, Merged or Declined; turn this off with the admin page toggle. Builds and deployments are sent separately. Restricting the app to your Jira project keys in the admin page avoids false matches such as `UTF-8`.


## When Jira is unavailable

If Jira answers with a rate limit (429) or a server error (5xx), or the call times out, the app does not lose the event. It retries on its own, waiting 30 seconds, 2 minutes, 8 minutes, then 15 minutes twice: five retries over about 40 minutes. You do not need to do anything. If all five fail, the event log shows one `error` entry that is never sampled away, and you can re-run the pipeline. A rejected request (Jira answered 400) is not retried, because the same request would fail again; it shows as `rejected` with the reason.

The app always answers Azure DevOps with success once the secret is right, even when Jira refused the data. This stops Azure DevOps from disabling your subscription. Real problems show in the event log, not in Azure DevOps.


## Rotate the secret

Press **Regenerate secret** on the admin page and pick one:

- **Rotate (old secret works 24 h)**: for planned changes. The new secret works at once and the previous one keeps working for 24 hours, so events keep arriving while you update each Azure DevOps service hook (edit the subscription, paste the new password, **Test**, **Finish**). The page shows until when the previous secret is accepted. Events that still use it appear in the event log with `old-secret;` in front of the detail, which tells you a hook is not updated yet.
- **Revoke old secrets now**: if a secret leaked. Every previous secret stops working immediately; hooks get 401 until you update them.

Each rotation keeps its own 24 hours: rotating again before you finish does not cut off hooks that still use an older secret (up to 3 previous secrets are kept). The page shows when the first one expires.

## Dashboard gadget

Add **Azure Pipelines builds** to a Jira dashboard (**Add gadget**, search "Azure"). In its settings pick a Jira project key (or leave it empty for all projects) and **Failing builds**, **Passing builds** or **Any builds**. The gadget lists up to 20 matching issues, newest update first, with their status. It searches as the person viewing the dashboard, so everyone sees only issues they can browse, and the app stores nothing for it.

## Uninstall

Uninstall the app from **Apps > Manage apps** in Jira. Jira deletes all the builds and deployments the app sent, immediately. The app's stored settings and caches are removed under Atlassian's app-data deletion practices.

The webhook URL stops working. Then delete the service hooks in each Azure DevOps project (**Project settings > Service hooks**), or Azure DevOps will keep trying to deliver events. If you reinstall, the app creates a new URL and secret: update your hooks.


## Support

Email support@ironmile.dev or see the [support page](https://ironmile.dev/azure-builds/support). Privacy policy: [privacy](https://ironmile.dev/azure-builds/privacy). Please do not send secrets; if you posted one by mistake, regenerate it with **Revoke old secrets now**.
