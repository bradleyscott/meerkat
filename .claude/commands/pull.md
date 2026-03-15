---
description: Pull content from wiki (Confluence or Notion) to local markdown files (project)
argument-hint: <file-path(s) or glob pattern(s)>
allowed-tools: Read, Edit, Glob, Bash, AskUserQuestion, mcp__mcp-atlassian__confluence_get_page, mcp__notion__notion-fetch
---

# Pull from Wiki

Pull content from wiki pages (Confluence or Notion) to the corresponding local markdown files.

## Instructions

### Resolve file list

`$ARGUMENTS` may contain one or more file paths and/or glob patterns, separated by spaces or commas. If not provided, ask the user for the file path(s).

1. Split `$ARGUMENTS` into individual tokens (space or comma separated).
2. For each token, use the Glob tool to expand it. If a token contains no glob characters (`*`, `?`, `[`), treat it as a literal file path.
3. Collect all resolved `.md` files into a deduplicated list. If the list is empty, tell the user no matching files were found and ask them to check the path.
4. Process each file in the list by following the steps below. When processing multiple files, report progress (e.g. "Pulling 2/5: path/to/file.md").

### Per-file processing

For each file:

1. Read the file.

2. Parse the YAML frontmatter (between the opening and closing `---` lines) to extract:
   - `wiki_url`: (required) The URL of the wiki page to pull from
   - If `wiki_url` is not present, abort with an error message: "No wiki_url found in frontmatter. Push the file first with /push to create the wiki page."

3. **Detect the wiki platform** from the `wiki_url` domain:
   - `atlassian.net` → **Confluence**
   - `notion.so` → **Notion**
   - If the domain doesn't match either, ask the user which platform this URL belongs to

4. Read the platform-specific skill file and follow its instructions:
   - Confluence → read `skills/wiki-sync/pull-confluence.md`
   - Notion → read `skills/wiki-sync/pull-notion.md`

   Follow the steps in that file, passing along the file path and parsed frontmatter.
