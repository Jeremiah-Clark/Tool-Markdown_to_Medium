# Markdown → Medium

A single-file tool for drafting articles in Markdown and pasting them into Medium with formatting intact.

## Setup

1. Open `md-to-medium.html` in any modern browser. No install needed — everything runs locally.
2. First load needs internet to fetch two scripts (marked and DOMPurify) from jsDelivr. After that, your browser caches them.
3. On first open you'll see sample markdown demonstrating the supported syntax. Select all and delete to start fresh.

## The interface

Two panes:

- **Left:** Markdown editor. Type or paste your draft.
- **Right:** Live preview. Updates ~200ms after you stop typing.

Across the top:

- **Split / Editor / Preview** — toggle the view mode.
- **Copy for Medium** — copies the rendered output as rich text, ready to paste into Medium.

Across the bottom:

- **Warning chips** flag anything Medium won't handle cleanly (see below).
- **Word count** is derived from the rendered preview, so markdown syntax doesn't inflate the number.

## Workflow

1. Write or paste your markdown.
2. Glance at the warning chips — anything there flags compatibility issues.
3. Click **Copy for Medium** (or press **Cmd/Ctrl+Shift+C**).
4. In Medium's editor, paste. Formatting carries over.

## What translates cleanly

- Headings: H1, H2, H3
- Bold and italic
- Links
- Inline code and fenced code blocks
- Blockquotes
- Bulleted and numbered lists, including nested
- Images — but only when hosted at a public URL
- Horizontal rules

## What doesn't translate, and what to do about it

The bottom-bar chips warn you when these appear in your draft:

- **H4–H6 headings** get auto-collapsed to H3 in the copy. Medium doesn't support deeper levels.
- **Tables** are replaced with a placeholder line. Medium strips table formatting entirely. Rewrite as a list, or capture the table as an image.
- **Nested lists** get flattened to a single level by Medium on paste. This is a Medium platform limitation, not something the tool can fix. If you need a visual hierarchy, the common workaround is to use `Shift+Enter` and an em dash inside Medium's editor after pasting.
- **Empty line after blockquotes** — Medium's editor inserts an empty quote line immediately after every blockquote on paste. This is a Medium platform behavior, not something the tool can prevent. After pasting, click into the empty line and press Backspace once to remove it.
- **Local image paths** like `![alt](image.png)` won't display. Upload the image somewhere public first, then link to the URL.
- **Raw HTML tags** in your markdown are stripped during sanitization. Medium would ignore them anyway.

## If the copy button fails

Some browsers block clipboard writes on `file://` pages. If that happens, a popup will appear in the middle of the screen with two buttons:

- **Open rendered HTML in new tab** *(recommended)* — click this. A new browser tab opens with your article rendered cleanly. Press Cmd/Ctrl+A to select all, Cmd/Ctrl+C to copy, then switch to Medium and paste as normal.
- **Show raw HTML** — for debugging only. Pasting raw HTML source into Medium gives you plain text, not rich content.

## A few things worth knowing

- **Synced scrolling** works in both directions. It's proportional rather than line-perfect, so very long documents may drift slightly between panes.
- **The preview matches the copy.** What you see, including the H4-collapse warnings and table replacements, is exactly what gets copied to your clipboard.
- **Your content stays local.** The tool itself doesn't transmit your markdown anywhere. The only network calls are the two script fetches on first load.
- **Sanitization is automatic.** Embedded scripts, event handlers, and `javascript:` URLs are stripped before they touch the preview, so pasting markdown from an untrusted source is safe.
