# Push to Notion

Platform-specific push instructions for Notion. Called by the `/push` router command, which has already:
- Read the file and parsed frontmatter (`wiki_url`, `wiki_title`)
- Determined the page title
- Extracted markdown content after frontmatter
- Removed the leading H1 heading (if applicable)

Continue from here with the prepared content.

## Steps

1. **Replace links with Notion URLs**:

   **Relative markdown links** — scan for `[text](./path/to/file.md)` or `[text](../path/to/file.md)` or `[text](path/to/file.md)`:
   - For each relative link found:
     a. Resolve the full path relative to the current file's directory
     b. Read that target file's YAML frontmatter
     c. Extract the `wiki_url` value from the target file's frontmatter
     d. If a `wiki_url` exists, replace the relative link with the Notion URL
     e. If no `wiki_url` exists in the target file, leave the link unchanged and note a warning

   **Obsidian wikilinks** — scan for `[[Page Name]]`, `[[Page Name|Display Text]]`, and `[[@Person Name]]`:
   - For each wikilink found:
     a. Extract the target page name (before `|` if present) and optional display text (after `|`)
     b. Use Glob to find a matching `.md` file in the vault (match on filename, stripping any `@` prefix for people links)
     c. Read that target file's YAML frontmatter
     d. If a `wiki_url` exists in the frontmatter, replace the wikilink with `[display text](wiki_url)` (use display text if provided, otherwise the page name)
     e. If no matching file is found or no `wiki_url` exists, replace the wikilink with plain text (the display text or page name) so it renders cleanly in Notion rather than showing raw `[[brackets]]`

   - This ensures links remain navigable when the markdown is pushed to Notion

2. **Image references**: Notion MCP does not support file uploads. If the content contains image references (`![alt](path)`), leave them unchanged and output a warning:
   ```
   Note: This document contains local image references that won't display in Notion.
   Upload images to Notion manually or host them externally, then update the links.
   ```

3. **Diff and confirm** (only when `wiki_url` EXISTS — i.e. updating an existing page):
   - Use `notion-fetch` to retrieve the current Notion page content using the `wiki_url`
   - Compare the fetched Notion content against the new markdown content (from steps 1–2)
   - Display the differences to the user in a unified-diff style format:
     - Lines removed from the current Notion page: prefix with `- `
     - Lines added in the new local version: prefix with `+ `
     - Unchanged lines shown for context (2–3 surrounding lines), prefixed with a space
     - Group changes into hunks with `@@ ... @@` headers, like a git diff
   - Before diffing, normalize both texts to reduce noise:
     - Trim trailing whitespace from each line
     - Collapse runs of 3+ blank lines into 2
     - Ignore differences that are only whitespace or blank-line count changes
   - If there are **no meaningful differences**, report "No changes to push — Notion page is already up to date." and stop
   - If there **are** differences, display the diff and ask the user:
     ```
     The above changes will be pushed to Notion. Proceed? (yes/no)
     ```
   - If the user answers **no**, stop without making changes
   - If the user answers **yes**, continue to step 4

4. If `wiki_url` EXISTS in the frontmatter:
   - Use the diff from step 3 to build a list of `update_content` search-and-replace operations. For each changed hunk in the diff:
     - Use the **old text** (removed lines) as the `old_str`
     - Use the **new text** (added lines) as the `new_str`
     - Include enough surrounding unchanged context in both `old_str` and `new_str` to ensure a unique match
   - Update the page title if it has changed:
     - Use `notion-update-page` with `command: "update_properties"` and `properties: { "title": "<title>" }`
   - Apply content changes:
     - Use `notion-update-page` with `command: "update_content"` and `content_updates` set to the search-and-replace operations built above
   - This approach preserves Notion block IDs and any comments attached to unchanged blocks, rather than replacing the entire page content

5. If `wiki_url` does NOT exist in the frontmatter:
   - **Load Notion configuration:** Read `config.json` from the meerkat project root to get `notion.parent_page_id`. If the file does not exist or the field is empty, ask the user for:
     - The parent page ID or URL under which new pages should be created
     - Save the value to the `notion` object in `config.json` for future use
   - Use `notion-create-pages` to create a new page with:
     - `parent`: The parent page ID from `config.json`
     - `title`: The determined page title
     - `content`: The markdown content
   - After successful creation, update the original markdown file's frontmatter:
     - Extract the page URL from the API response
     - Use the Edit tool to add `wiki_url: <new-page-url>` to the YAML frontmatter

6. Report success or any errors encountered.
