# Push to Source

Push one or more markdown files to their corresponding source pages (Confluence, Notion, etc.).

## Instructions

### Resolve file list

The input may contain one or more file paths and/or glob patterns, plus an optional URL, separated by spaces or commas. If you can see file path(s) in the conversation context or the user's selection, use those. Otherwise, ask the user for the file path(s).

1. Split the input into individual tokens (space or comma separated).
2. Separate URL tokens (starting with `http`) from file/glob tokens.
3. For each file/glob token, expand any glob patterns. If a token contains no glob characters (`*`, `?`, `[`), treat it as a literal file path.
4. Collect all resolved `.md` files into a deduplicated list. If the list is empty, tell the user no matching files were found and ask them to check the path.
5. Process each file in the list by following the steps below. When processing multiple files, report progress (e.g. "Pushing 2/5: path/to/file.md").

### Per-file processing

For each file:

1. Read the file.

2. Parse the YAML frontmatter (between the opening and closing `---` lines) to extract:
   - `source_url`: (optional) The URL of the source page to update
   - `source_title`: (optional) The title to set for the page

3. **Resolve the source URL** using this priority order:
   a. Use `source_url` from frontmatter if present
   b. Use a URL token found in the input if present
   c. If still no URL, ask: "No source URL found for {filename}. Paste the URL of the page to update, or the parent page URL to create a new page under:"
   - After resolving via (b) or (c), write the URL back to the file's frontmatter as `source_url` using the Edit tool before proceeding

4. Determine the page title:
   - If `source_title` exists in the frontmatter, use that value
   - Otherwise, find the first H1 heading (line starting with `#`) in the markdown content and use its text as the title

5. Extract the markdown content that appears AFTER the closing `---` of the frontmatter. Do NOT include the frontmatter in the source content.

6. **Remove leading H1 heading from content**:
   - Check if the first non-empty line of the content is an H1 heading (line starts with `#` followed by a space)
   - Count the total number of H1 headings in the document
   - If the first content is an H1 AND there is only one H1 in the entire document:
     - Remove that H1 line from the content (the source page title will serve as this heading)
     - Also remove any blank lines immediately following the removed heading
   - Otherwise, leave the content unchanged

7. **Detect the source platform** from the `source_url` domain:
   - `atlassian.net` → **Confluence**
   - `notion.so` → **Notion**
   - If the domain doesn't match a known platform, ask the user which platform this URL belongs to

8. Read the platform-specific skill file and follow its instructions:
   - Confluence → read `skills/source-sync/push-confluence.md`
   - Notion → read `skills/source-sync/push-notion.md`

   Follow the steps in that file, passing along the file path, determined title, and prepared content.
