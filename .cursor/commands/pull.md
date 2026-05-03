# Pull from Source

Pull content from source pages (Confluence, Notion, etc.) to the corresponding local markdown files.

## Instructions

### Resolve file list

The input may contain one or more file paths and/or glob patterns, plus an optional URL, separated by spaces or commas. If you can see file path(s) in the conversation context or the user's selection, use those. Otherwise, ask the user for the file path(s).

1. Split the input into individual tokens (space or comma separated).
2. Separate URL tokens (starting with `http`) from file/glob tokens.
3. For each file/glob token, expand any glob patterns. If a token contains no glob characters (`*`, `?`, `[`), treat it as a literal file path.
4. Collect all resolved `.md` files into a deduplicated list. If the list is empty, tell the user no matching files were found and ask them to check the path.
5. Process each file in the list by following the steps below. When processing multiple files, report progress (e.g. "Pulling 2/5: path/to/file.md").

### Per-file processing

For each file:

1. Read the file.

2. Parse the YAML frontmatter (between the opening and closing `---` lines) to extract:
   - `source_url`: (optional) The URL of the source page to pull from

3. **Resolve the source URL** using this priority order:
   a. Use `source_url` from frontmatter if present
   b. Use a URL token found in the input if present
   c. If still no URL, ask: "No source URL found for {filename}. Paste the URL to pull from (Notion, Confluence, etc.):"
   - After resolving via (b) or (c), write the URL back to the file's frontmatter as `source_url` using the Edit tool before proceeding

4. **Detect the source platform** from the `source_url` domain:
   - `atlassian.net` → **Confluence**
   - `notion.so` → **Notion**
   - If the domain doesn't match either, ask the user which platform this URL belongs to

5. Read the platform-specific skill file and follow its instructions:
   - Confluence → read `skills/source-sync/pull-confluence.md`
   - Notion → read `skills/source-sync/pull-notion.md`

   Follow the steps in that file, passing along the file path and parsed frontmatter.
