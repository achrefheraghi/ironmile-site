---
layout: default
title: "Documentation: Code Block+ for Confluence"
permalink: /code-block-plus/docs
---

Code Block+ adds a code macro to the Confluence Cloud editor. It shows syntax-highlighted code with an optional title, line numbers, highlighted lines, line wrapping and a collapse button. The code is saved inside the macro on your page and is included when you export the page. The app runs on Atlassian (Forge) and sends no data outside your Confluence site.

## What you need

- Confluence Cloud. A Confluence admin installs the app from the Atlassian Marketplace.
- Permission to edit the page where you add the macro. Anyone who can view the page can see the code.
- For the migration scan only: Confluence administrator rights. See [Scan a space for Better Code Macro blocks](#scan-a-space-for-better-code-macro-blocks).

## Add a code block to a page

1. Open a page in the editor.
2. Type `/` and search for **Code Block+**, then select it. (You can also pick it from the editor's insert menu.)
3. The editor dialog opens at once. Fill in the fields described below.
4. Press **Save**. The code appears on the page.
5. Publish or update the page.

To change a block later, select it on the page, choose **Edit**, change the fields and press **Save** again.

An empty block shows *Edit this macro to add code*.

## Fields

| Field | What it does |
|---|---|
| **Title (optional)** | Shown above the code. Up to 120 characters. A counter shows how many you have used. |
| **Language** | One of 84 languages, or **Plain text**. The default is Plain text. |
| **Code** | The code. Required. Up to 200 KiB. A counter shows the size against 65,536 bytes (64 KiB). |
| **Highlight lines (for example 1-5,7)** | Lines to mark, as numbers and ranges separated by commas. Optional. |
| **Show line numbers** | On by default. |
| **Wrap long lines** | Off by default. Long lines wrap instead of scrolling sideways. |
| **Collapsed by default** | Off by default. The block is hidden behind a button until a reader opens it. |

A **Preview** under the form shows the block as you type. It updates a moment after you stop typing.

Nothing is saved until you press **Save**. Save stays disabled while a field has an error. If a save fails, the dialog shows *Could not save* with the reason, and your code stays in the form.

### Highlight lines

Write line numbers (1 is the first line) and ranges, with no spaces needed: `1-5,7` marks lines 1 to 5 and line 7. The field takes up to 64 characters. Lines past the end of the code are ignored. If the text is not in this form, the dialog shows *Use ranges like 1-5,7* and blocks Save.

### Languages

The list covers common languages and formats, among them JavaScript, TypeScript, Python, Java, C, C++, CSharp, Go, Rust, PHP, Ruby, Kotlin, Swift, SQL, Shell, PowerShell, Dockerfile, YAML, JSON, XML, HTML, CSS, Markdown, GraphQL, HCL, NGINX, TOML and Diff. Open the **Language** menu for the full list. If a block uses a language the app does not know, it shows as plain text.

## Collapse a long block

With **Collapsed by default** on, readers see the title and a button that says, for example, *Show 40 lines*. One click opens the block, and the button then says *Hide*. The reader's choice is not saved: the block starts collapsed again on the next page load.

## Large code blocks

- Above 64 KiB the dialog warns that large blocks slow the page, and the preview is off until you press **Show preview (large code block)**.
- 200 KiB (204,800 bytes) is the hard limit. Save is blocked above it. If a block already on the page is larger (for example, a page edited through the API), the page shows only the first 200 KiB with a note. When you open that block in the editor, you must tick **Save only the first 200 KiB** before Save works, because saving removes the rest.

## Export to PDF and Word

PDF and Word export include your code and its title. The export carries the title in bold followed by a code block in the language you chose. Page history shows the same.

- **PDF:** in our tests the PDF showed syntax colours and line numbers. Lines longer than 100 characters are split into pieces, and each piece gets its own line number in the PDF.
- **Word:** the code appears as plain monospace text, without colours or line numbers.
- **Not exported:** highlighted lines. A collapsed block is exported in full.
- If the app cannot find the block while exporting, the export shows a short placeholder line instead of failing.

## If your subscription lapses

Your code stays visible. Blocks become read-only: the page shows *Subscription inactive. Code Block+ is read-only until a Confluence admin activates it under Manage apps.*, and the editor dialog opens for viewing and previewing but cannot save. A Confluence admin can activate the app again under **Manage apps**. The admin importer also stops until then.

## Scan a space for Better Code Macro blocks

If your site uses Better Code Macro, a Confluence admin can scan a space to see how many of its blocks Code Block+ recognises. The scan is read-only. Converting blocks is not available yet. Steps and details are on the [migration page](https://ironmile.dev/code-block-plus/migrating).

In short:

1. Open **Confluence settings**, then **Code Block+ import** under Apps.
2. Choose a space and press **Dry run**.
3. Read the report: pages scanned, blocks that can be converted, blocks that would be skipped with the reason, and a list of pages with their counts.

Good to know:

- Only Confluence administrators can use the page. If anyone else opens the page, the scan refuses with a message that only Confluence administrators can import.
- The scan runs with your own permissions, so pages you cannot see are not counted.
- Reasons for skipping include an empty block, a block over the size limit, a block used inline in text, a block with unsupported content and a block that was already converted.
- Very large spaces may stop at a page limit. The report says it stopped at the page limit.
- The space menu shows up to 1,000 spaces.

## Where your content is stored

The code, title and settings are saved in the macro on your Confluence page. They follow the page: they appear in page history and come back with restore points, and deleting the macro or the page deletes them. The app has no servers, no database of its own and no external network access.

The only data the app stores is the importer's scan record: page IDs and the admin's account ID, with no page text, deleted after 30 minutes. Details: [Privacy policy](https://ironmile.dev/code-block-plus/privacy).

### Permissions

The app asks Atlassian for these scopes when an admin installs it.

| Scope | Used for |
|---|---|
| Read pages and blog posts | The migration scan, and finding a block when you export a page. |
| Write pages | Reserved for the converter. Version 1.0 does not change any page. |
| Read spaces | Listing spaces for the scan. |
| Read Confluence users | Checking that the person opening the import page is an admin. |
| App storage | The 30-minute scan record described above. |

## Pricing and licensing

Free for sites with 1 to 10 users, with no time limit. Above 10 users the price is $0.20 per user per month, billed by Atlassian. Annual billing is ten times the monthly price. For example, 25 users cost $5 per month or $50 per year; 50 users cost $10 per month or $100 per year; 100 users cost $20 per month or $200 per year. Atlassian shows the exact tiers on the Marketplace pricing tab.

## Limits and what is not included

- No copy button in version 1.0. Readers select the code and copy it as usual.
- No themes, no custom first line number and no folding at brackets.
- No Gist or Bitbucket snippet embeds. They need outside servers, and this app makes no external calls.
- Highlighted lines are not part of PDF or Word export.
- Title: 120 characters. Highlight field: 64 characters. Code: 200 KiB.
- The importer scans only. It does not convert blocks yet.
- Code text is not promised to appear in Confluence site search.

## Help

- [Support](https://ironmile.dev/code-block-plus/support): email **support@ironmile.dev**.
- [Migrating from Better Code Macro](https://ironmile.dev/code-block-plus/migrating)
- [Privacy policy](https://ironmile.dev/code-block-plus/privacy)
- [Terms of use (EULA)](https://ironmile.dev/code-block-plus/terms)
- [All apps](https://ironmile.dev/)

Provided by Achref Heraghi, trading as Ironmile, Tunisia.
