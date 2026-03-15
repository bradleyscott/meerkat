---
description: Push markdown files to wiki (Confluence or Notion) (project)
argument-hint: <file-path(s) or glob pattern(s)>
allowed-tools: Read, Edit, Glob, Bash, AskUserQuestion, mcp__mcp-atlassian__confluence_get_page, mcp__mcp-atlassian__confluence_update_page, mcp__mcp-atlassian__confluence_create_page, mcp__notion__notion-fetch, mcp__notion__notion-create-pages, mcp__notion__notion-update-page
---

# Push to Wiki

Push one or more markdown files to their corresponding wiki pages (Confluence or Notion).

## Instructions

### Resolve file list

`$ARGUMENTS` may contain one or more file paths and/or glob patterns, separated by spaces or commas. If not provided, ask the user for the file path(s).

1. Split `$ARGUMENTS` into individual tokens (space or comma separated).
2. For each token, use the Glob tool to expand it. If a token contains no glob characters (`*`, `?`, `[`), treat it as a literal file path.
3. Collect all resolved `.md` files into a deduplicated list. If the list is empty, tell the user no matching files were found and ask them to check the path.
4. Process each file in the list by following the steps below. When processing multiple files, report progress (e.g. "Pushing 2/5: path/to/file.md").

### Per-file processing

For each file:

1. Read the file.

2. Parse the YAML frontmatter (between the opening and closing `---` lines) to extract:
   - `wiki_url`: (optional) The URL of the wiki page to update
   - `wiki_title`: (optional) The title to set for the page

3. Determine the page title:
   - If `wiki_title` exists in the frontmatter, use that value
   - Otherwise, find the first H1 heading (line starting with `#`) in the markdown content and use its text as the title

4. Extract the markdown content that appears AFTER the closing `---` of the frontmatter. Do NOT include the frontmatter in the wiki content.

5. **Remove leading H1 heading from content**:
   - Check if the first non-empty line of the content is an H1 heading (line starts with `#` followed by a space)
   - Count the total number of H1 headings in the document
   - If the first content is an H1 AND there is only one H1 in the entire document:
     - Remove that H1 line from the content (the wiki page title will serve as this heading)
     - Also remove any blank lines immediately following the removed heading (to avoid extra whitespace at the top)
   - Otherwise, leave the content unchanged

6. **Detect the wiki platform** using this priority order:
   a. If `wiki_url` exists in the frontmatter, infer from the URL domain:
      - `atlassian.net` → **Confluence**
      - `notion.so` → **Notion**
   b. Read `config.json` from the project root. If `wiki.default_platform` is set, use that value.
   c. Check which platform has configuration populated in `config.json`:
      - `confluence.space_key` or `confluence.parent_id` non-empty → **Confluence**
      - `notion.parent_page_id` non-empty → **Notion**
      - Both populated → ambiguous, fall through to (d)
   d. Use `AskUserQuestion` to ask: "Which wiki platform? (Confluence / Notion)"
      - Save the answer to `config.json` under `wiki.default_platform` for future use

7. Read the platform-specific skill file and follow its instructions:
   - Confluence → read `skills/wiki-sync/push-confluence.md`
   - Notion → read `skills/wiki-sync/push-notion.md`

   Follow the steps in that file, passing along the file path, determined title, and prepared content.
