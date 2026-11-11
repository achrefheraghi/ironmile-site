---
layout: default
title: "Documentation: Email Attachment Viewer for Jira"
permalink: /email-viewer/docs
---

Email Attachment Viewer adds a panel to the Jira Cloud issue view. It lists the `.msg` and `.eml` files attached to the issue and opens the one you pick as a readable email: sender, recipients, date, subject, body, inline images and attachments. You do not have to download the file or start a mail client. The app runs on Atlassian (Forge), asks for one read-only permission and sends no data outside Atlassian.

## What you need

- Jira Cloud (Jira or Jira Service Management). A Jira admin installs the app from the Atlassian Marketplace.
- Permission to view the issue and its attachments. The app reads attachments as you, so you can only open files you could already see in Jira.

## Open an email attachment

1. Open an issue that has a `.msg` or `.eml` file attached.
2. Find the **Email attachments** panel in the issue view. It shows *Loading attachments…* and then lists every `.msg` and `.eml` file on the issue, with its size.
3. Press **Open** next to the file. The panel shows *Opening* and the file name, then the email.
4. Press **Refresh** at the top of the list after someone adds or removes an attachment.

If the issue has no such files, the panel says *No .msg or .eml attachments on this issue.*

Files are found by the `.eml` or `.msg` ending, or by the mail file type Jira records for them. When you open a file, the app checks what the file really contains, not just its name. A file that is not a mail message gets the notice *This file is not a .msg or .eml message.*

## What the panel shows

Above the message:

- **Breadcrumb.** The first link is **Attachments** and takes you back to the list. After it comes the file name, and for an email opened inside an email, the subject of each one.
- **Headers.** **From**, **To**, **Cc**, **Date** and **Subject**. A line is left out when the email has no value for it. The date is shown in your browser's local format. Bcc and Reply-To are not shown.
- **Notes**, when they apply: the number of remote images blocked, inline images that were too large to show, and warnings about text encoding or rich-text formatting (see below).
- **Attachments.** Files inside the email, with their sizes. Pictures that are only part of the formatted body are not listed.

Below that is the **body**. An HTML body is shown formatted, with inline images. A plain-text body is shown as plain text. A body written only in Outlook rich text (RTF) is converted to basic formatting: paragraphs, line breaks, bold, italic, underline and links. If the email has no body, the panel says *(This message has no body.)* The panel grows to fit the email, so you scroll the Jira page, not the message.

### Attachments inside an email

- **Download** saves the file to your computer.
- **Open** appears for attachments that are themselves emails. The nested email opens in the same panel. Use the breadcrumb to step back up. You can go 5 levels deep.

### Links in an email

Web, mail and phone links open from the panel. Jira opens web links in a new tab and may ask you to confirm before it leaves Atlassian.

## Supported files

| Type | Notes |
|---|---|
| `.eml` | Standard internet email (RFC 822). Plain text and HTML bodies. Common non-UTF-8 character sets, for example ISO-2022-JP, KOI8-R and Windows-1252, are read correctly. |
| `.msg` | Outlook message files. HTML, plain text and RTF-only bodies. Non-English text and older Windows code pages are handled, for example Japanese. |

Not supported yet: TNEF `winmail.dat` attachments, signed or encrypted (S/MIME) messages and calendar invites. Heavy marketing newsletters from Outlook may lose some styling. If the app had to guess a text encoding, a note says that some characters may be wrong.

## Security: what is not shown

Email can contain hostile content, so the app removes it before display.

- **Scripts never run.** The HTML is cleaned and shown in a sandboxed frame that does not allow scripts. Forms, embedded pages, objects and similar elements are removed.
- **Remote images are blocked.** Images that would load from another website are not fetched, so tracking pixels cannot fire. The panel says, for example, *2 remote images blocked (not loaded, for privacy)*. There is no setting to turn loading on.
- **Remote styling is removed.** Style rules that would load files from outside, such as `url()` and `@import`, are stripped.
- **Only images inside the email are shown.** Pictures embedded in the message display. Anything else is replaced by a blank placeholder.

## Permissions and data

- The app has one permission: read Jira work (`read:jira-work`). It never writes to Jira.
- When you open a file, the app checks that the file belongs to the issue you are viewing. If it does not, it refuses.
- The app has no servers of its own, no database and no outside network access. It stores no email content and keeps no cache. Each time you open an email, the file is read from Jira again and the result is discarded after display.
- App logs hold the attachment ID, sizes, time taken and status. They never hold email content.

More: [Privacy policy](https://ironmile.dev/email-viewer/privacy).

## Pricing and licensing

Free for up to 10 users. Above that, $0.30 per user per month, billed by Atlassian. If the subscription lapses, the list of file names still appears, but **Open** is disabled and the panel says *Subscription inactive. A Jira admin can reactivate Email Attachment Viewer under Manage apps.* Nothing is deleted. Opening works again once a Jira admin reactivates the app.

## Limits

- **25 MB per attachment.** Larger files show *over 25 MB, download it from Jira* in the list, and **Open** is disabled. Jira's own download still works.
- **Inline images:** up to 4 MB in total per email. Larger ones are left out and the panel tells you how many.
- **Very large emails:** if the processed email is over about 5 MB, it is not shown and the panel asks you to download it from Jira.
- **Downloads from the panel:** attachments inside an email up to 3.5 MB. For larger ones, download the parent file from Jira and open it in your mail client.
- **Nested emails:** up to 5 levels.
- **Time:** an email that takes more than 20 seconds to open stops with *This email took too long to open*. Download it from Jira instead.
- If an error appears, press **Try again**, or **Back to attachments** to return to the list.

## Help

- [Support](https://ironmile.dev/email-viewer/support): email **support@ironmile.dev**.
- [Privacy policy](https://ironmile.dev/email-viewer/privacy)
- [Terms of use (EULA)](https://ironmile.dev/email-viewer/terms)

Provided by Achref Heraghi, trading as Ironmile, Tunisia.
