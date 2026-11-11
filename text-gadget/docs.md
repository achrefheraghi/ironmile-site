---
layout: default
title: "Documentation: Text & Announcement Gadget for Jira"
permalink: /text-gadget/docs
---

Text & Announcement Gadget puts Markdown text and announcement banners on Jira Cloud dashboards. It runs on Atlassian (Forge), asks for no permissions and sends no data outside your Jira site.

## What you need

- Jira Cloud. A Jira admin installs the app from the Atlassian Marketplace.
- Permission to edit the dashboard where you add the gadget. Anyone who can see the dashboard can see the gadget.

## Add the gadget to a dashboard

1. Open a dashboard in Jira (**Dashboards**, then pick one or create one).
2. Press **Edit** (top right), then **Add gadget**.
3. Search for **Text & Announcement Gadget** and press **Add**.
4. The new gadget says *Click Configure to add your text*. Open the gadget menu (**…**) and choose **Configure**.
5. Fill in the fields described below and press **Save**.

You can add the gadget more than once. Each copy has its own content, so one dashboard can show a release notice and a sprint goal side by side.

## Fields

| Field | What it does |
|---|---|
| **Title** | Optional. Shown as the banner title when an announcement style is set. Up to 120 characters. |
| **Text (Markdown)** | The content. Up to 20,000 characters. The **Preview** below it shows the result as you type. |
| **Announcement style** | **None**, **Info**, **Warning**, **Success** or **Error**. Any style other than None shows the text in a colored banner. |
| **Preset** | **Plain**, **Card**, or **Accent** in blue, yellow, green or purple. Sets the background and border. |
| **Compact spacing** | Less padding, so more fits on the dashboard. |
| **Open links in a new tab** | On by default. Links open in a new browser tab, not inside the gadget. |
| **Show from (optional)** | First day the text is shown. |
| **Show until (optional)** | Last day the text is shown. |
| **Text shown outside the dates (optional)** | Up to 200 characters shown before the start date and after the end date. Leave it empty to show nothing. |

Nothing is saved until you press **Save**. If a save fails, the edit view shows *Could not save* with the reason, and your text stays in the form.

## Markdown you can use

| You type | You get |
|---|---|
| `# Heading`, `## Heading`, `### Heading` | Headings (three levels) |
| `**bold**`, `*italic*`, `~~struck~~` | Bold, italic, strikethrough |
| `- item` or `1. item` | Bulleted or numbered lists, nested up to two levels |
| `[text](https://example.com)` | Links (`https:`, `http:` and `mailto:` only) |
| `` `code` `` and fenced blocks with three backticks | Inline code and code blocks |
| `> quote` | Block quotes |
| `---` | A horizontal line |
| A table (see the example below) | A table, up to 20 columns and 200 rows |

Example: a release freeze notice with a table.

```
**Code freeze** for release 4.2. Only fixes approved in [the release channel](https://example.com).

| Day | What happens |
|---|---|
| Monday | Freeze starts |
| Wednesday | Release candidate |
| Friday | Release |
```

Raw HTML is shown as plain text and never run. Images are not supported yet; an image line shows a short notice instead. They are planned for a later version.

## Schedule an announcement

Set **Show from** and **Show until** to limit when the text appears. Both days are included, and the day is the viewer's local date. Outside the dates the gadget shows your fallback text, or nothing.

The edit view always shows the full content and a label with the schedule: **Scheduled** (starts later), **Showing now** or **Ended**. You can set only one of the two dates; the other side then has no limit. Save is blocked if the end date is before the start date.

## Dark mode

The gadget uses Jira's own colors, so it follows the theme each viewer chose in Jira (light, dark or match the browser). You do not need to set anything.

## Where your content is stored

The text and settings are saved on the dashboard item in your Jira site, the same place Jira keeps settings for its own gadgets. The app has no servers, no database of its own and no external network access. Deleting the gadget deletes its content. Details: [Privacy policy](https://ironmile.dev/text-gadget/privacy).

## Pricing and licensing

Free for up to 10 users. Above that, $0.30 per user per month, billed by Atlassian. If the subscription lapses, your text stays visible and is not deleted. The gadget shows a banner and becomes read-only until a Jira admin activates the app again under **Manage apps**.

## Limits

- Text: 20,000 characters. Title: 120. Fallback text: 200. The whole configuration must stay under 28 KB; Save tells you if it does not.
- Tables: 20 columns and 200 rows; extra rows and columns are cut and marked *(table truncated)*.
- No images yet, and no WYSIWYG editor: you write Markdown and check the preview.

## Help

- [Support](https://ironmile.dev/text-gadget/support): email **support@ironmile.dev**.
- [Privacy policy](https://ironmile.dev/text-gadget/privacy)
- [Terms of use (EULA)](https://ironmile.dev/text-gadget/terms)

Provided by Achref Heraghi, trading as Ironmile, Tunisia.
