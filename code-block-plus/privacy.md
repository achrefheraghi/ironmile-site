---
layout: default
title: "Privacy Policy: Code Block+ for Confluence"
---

Last updated: 2026-10-20

This policy covers the Confluence Cloud app "Code Block+ for Confluence" (the "app"), provided by Achref Heraghi, trading as Ironmile ("we", "us"). Contact: support@ironmile.dev.

## What the app does with data

The app is a Confluence macro built on Atlassian Forge and hosted on Atlassian's infrastructure ("Runs on Atlassian"). We do not operate any servers, databases or services for it.

## What is stored

The code you type into a macro, its title, language and display settings (line numbers, highlighted lines, wrap, collapse). They are saved inside the macro on your Confluence page, as part of the page content in your own Confluence site. We have no copy of them and no access to them. Anyone who can edit the page can read and change these values.

The app's own storage (Forge storage) holds one kind of record: a temporary token created when a Confluence admin runs the import dry run. It lists the IDs of the pages found in the scanned space and is keyed by the space ID and the admin's Atlassian account ID. It contains no page text and no code. It expires after 30 minutes.

## Permissions

Scopes requested in the manifest: `read:page:confluence`, `write:page:confluence`, `read:space:confluence`, `read:confluence-user` and `storage:app`. They are used only by the admin import scan and the export fallback; displaying a macro makes no API call.

## What we collect

Nothing. We do not receive, log or read your code, page text, users' names or email addresses. The app contains no analytics, tracking, advertising or cookies of its own.

## What leaves your site

Nothing. The app makes no calls to servers outside Atlassian and sends no data to us or to third parties. We use no subprocessors.

## How the app reads your pages

Displaying a macro makes no API call. Two features read pages through Confluence's own APIs, inside Atlassian's infrastructure:

- Export: when a page is exported to PDF or Word, the app produces the code block for the export. If Confluence does not hand the macro its settings, the app reads the page being exported to find them.
- Import scan: a Confluence admin can scan a space. The scan reads pages with that admin's own permissions and reports counts and page titles on screen. It writes nothing in 1.0.

## Personal data

Any personal data in code or titles is text your users chose to write. It is held by Confluence under your Atlassian agreement and handled by Atlassian as described in Atlassian's privacy policy. We do not process it. The only personal identifier the app handles is an admin's Atlassian account ID, inside the temporary scan token described above.

## Data location and retention

Data stays where your Confluence site's data resides. Code is kept as long as the page and its versions exist. Removing the macro from a page removes it from the current version; older page versions keep what they held. Scan tokens expire after 30 minutes. Uninstalling the app removes the app's access; Atlassian's deletion practices apply to app storage.

## Licensing

Atlassian handles billing and licence status. We see what Marketplace shows a vendor about sales and licences (such as the site name, licence type and tier), under the Atlassian Marketplace Partner Agreement. We use it for support and accounting only.

## Support requests

If you contact us, we receive your email address and whatever you send. We use it to reply and delete it on request. Please do not send code or page content you consider sensitive.

## Your rights

For data stored in Confluence, contact your Confluence site administrator or Atlassian. For data from support requests, write to support@ironmile.dev to ask for access or deletion.

## Changes

If the app ever changes what it stores or sends, we will update this policy before the release and describe the change in the release notes. Adding an external connection would also require new admin consent in Confluence.

## Contact

Achref Heraghi, trading as Ironmile, support@ironmile.dev, https://ironmile.dev/code-block-plus/support
