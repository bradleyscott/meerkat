---
description: Pull content from external source (Confluence, Notion, etc.) to local markdown files (project)
argument-hint: <file-path(s) or glob pattern(s)> [source-url]
allowed-tools: Read, Edit, Glob, Bash, AskUserQuestion, mcp__mcp-atlassian__confluence_get_page, mcp__notion__notion-fetch, mcp__claude_ai_Google_Drive__download_file_content, mcp__claude_ai_Google_Drive__get_file_metadata
---

# Pull from Source

Pull content from source pages (Confluence, Notion, etc.) to the corresponding local markdown files.

## Instructions

### Resolve file list

`$ARGUMENTS` may contain one or more file paths and/or glob patterns, plus an optional URL, separated by spaces or commas. If not provided, ask the user for the file path(s).

1. Split `$ARGUMENTS` into individual tokens (space or comma separated).
2. Separate URL tokens (starting with `http`) from file/glob tokens.
3. For each file/glob token, use the Glob tool to expand it. If a token contains no glob characters (`*`, `?`, `[`), treat it as a literal file path.
4. Collect all resolved `.md` files into a deduplicated list. If the list is empty, tell the user no matching files were found and ask them to check the path.
5. Process each file in the list by following the steps below. When processing multiple files, report progress (e.g. "Pulling 2/5: path/to/file.md").

### Per-file processing

For each file:

1. Read the file.

2. Parse the YAML frontmatter (between the opening and closing `---` lines) to extract:
   - `source_url`: (optional) The URL of the source page to pull from

3. **Resolve the source URL** using this priority order:
   a. Use `source_url` from frontmatter if present
   b. Use a URL token found in `$ARGUMENTS` if present
   c. If still no URL, ask: "No source URL found for {filename}. Paste the URL to pull from (Notion, Confluence, etc.):"
   - After resolving via (b) or (c), write the URL back to the file's frontmatter as `source_url` using the Edit tool before proceeding

4. **Detect the source platform** from the `source_url` domain:
   - `atlassian.net` → **Confluence**
   - `notion.so` → **Notion**
   - `docs.google.com` or `drive.google.com` → **Google Docs**
   - If the domain doesn't match a known platform, ask the user which platform this URL belongs to

5. Read the platform-specific skill file and follow its instructions:
   - Confluence → read `references/pull-confluence.md`
   - Notion → read `references/pull-notion.md`
   - Google Docs → read `references/pull-gdocs.md`

   Follow the steps in that file, passing along the file path and parsed frontmatter.
