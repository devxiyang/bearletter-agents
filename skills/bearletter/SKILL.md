---
name: bearletter
description: Work on the author's Bearletter blog through the Bearletter MCP server - write and publish articles, edit pages, menus and themes, post to X, manage the podcast, and back up. Use when the user mentions Bearletter or their blog hosted on bearletter.com.
---

# Bearletter

Bearletter hosts the author's blog. A blog is a folder of plain text: Markdown articles in `posts/`, pages in `pages/`, site files with fixed names, a few components (lines starting with `::`), and one `styles.css`. Drafts live in Write and are published to the blog from there.

The format is documented at https://docs.bearletter.com/llms.txt (every page is Markdown). Read the pages you need before writing files, or call `get_blog_guide`.

## Connect

If the `bearletter` MCP tools are not available, add the remote MCP server `https://api.bearletter.com/mcp` (HTTP) to your configuration, the way your agent adds MCP servers. The author approves it in the browser the first time; there is no key. Then call `get_blog` and tell the author their blog's title and address.

## Rules

- The site files have fixed names: `home.md`, `nav.md`, `footer.md`, `post-header.md`, `post-footer.md`, `post-aside.md`, `social.md`, `directories.md`, `redirects.md`, `styles.css`. Never rename them, move them or invent other site files. Only files under `posts/` and `pages/` are yours to name.
- Read before you write, and pass back the `writeSeq` you read. If a save is refused as stale, read again and reapply the change.
- A refused save names the lines to fix. Fix those lines and try again; do not guess around the error.
- Anything public (saving a blog file, publishing, posting to X, changing the theme) goes live at once. Tell the author what will change and wait for a clear yes.
- Articles published from Write are changed in Write (`update_document`, then `publish_document` again), not by editing their blog file.
- Images and audio come from the author's media library. Upload new files with `start_media_upload`, a direct HTTP PUT, then `finish_media_upload`; never send file bytes through other tools.

## Common tasks

**Write and publish an article.** `create_document` (type `article`), show the author the text, `preview_document` for a link they can open, then on their yes `publish_document`. Report the article's address.

**Change the look.** `list_themes`, then `preview_styles` with a theme or a whole new `styles.css` and give the author the link. Only after they agree: `apply_theme` or `save_blog_file` for `styles.css`. Keep the first `:root` block of variables first, and add dark values in `@media (prefers-color-scheme: dark)`.

**Edit the menu or a page.** `read_blog_file` (`nav.md`, `pages/about.md`…), change it, show the diff, then `save_blog_file`.

**Post to X** (Max). Write the post as a Write `post` document (`create_document` with parts, each part one post of a thread). Check `get_x_account` for the allowance, show the author the text, then `post_to_x` now, with `at: "queue"` for the next queue time, or with a time. Posts on X cannot be taken back.

**Back up.** Ask the author for a backup token (Settings › Apps & tokens › Backup) and follow https://docs.bearletter.com/api/backup.md; or use the export in the dashboard.
