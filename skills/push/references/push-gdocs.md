# Push to Google Docs

Platform-specific push instructions for Google Docs. Called by the `/push` router command, which has already:
- Read the file and parsed frontmatter (`source_url`, `source_title`)
- Determined the page title
- Extracted markdown content after frontmatter
- Removed the leading H1 heading (if applicable)

Continue from here with the prepared content.

> **Limitation:** The Google Drive MCP does not support updating the content of an existing Google Doc. If the file already has a `source_url`, a new Google Doc will be created and the frontmatter updated to point to it. The old document is not modified or deleted.

## Steps

1. **Convert markdown to Google Docs-compatible format**:

   The Google Drive MCP accepts plain text or markdown when creating files. Prepare the content:
   - Keep headings as markdown (`#`, `##`, etc.) — Google Docs will render these as heading styles if the MCP accepts markdown
   - Keep bold (`**text**`), italic (`*text*`), and links (`[text](url)`) in markdown syntax
   - For tables, keep markdown table syntax — note that Google Docs may not render markdown tables natively; they will appear as plain text

2. **Replace relative links with Google Docs URLs**:
   - Scan the markdown content for relative links matching the pattern `[text](./path/to/file.md)` or `[text](../path/to/file.md)` or `[text](path/to/file.md)`
   - For each relative link found:
     a. Resolve the full path relative to the current file's directory
     b. Read that target file's YAML frontmatter
     c. Extract the `source_url` value from the target file's frontmatter
     d. If a `source_url` exists, replace the relative link with the Google Docs URL
     e. If no `source_url` exists in the target file, leave the link unchanged and note a warning

3. **Image references**: The Google Drive MCP does not support file uploads. If the content contains image references (`![alt](path)`), leave them unchanged and output a warning:
   ```
   Note: This document contains local image references that won't display in Google Docs.
   Upload images manually or host them externally, then update the links.
   ```

4. If `source_url` EXISTS in the frontmatter:
   - Warn the user:
     ```
     Note: Google Docs does not support in-place content updates via MCP.
     A new Google Doc will be created. The old document at {source_url} will not be modified.
     ```
   - Ask: "Create a new Google Doc? (yes/no)"
   - If no, stop without making changes

5. **Create the Google Doc** using `mcp__claude_ai_Google_Drive__create_file` with:
   - `name`: The determined page title
   - `content`: The prepared markdown content
   - `mimeType`: `application/vnd.google-apps.document` if the tool accepts it; otherwise omit and let the MCP infer the type

6. **Update the local file's frontmatter**:
   - Extract the new Google Doc URL from the API response
   - Use the Edit tool to set `source_url: <new-doc-url>` in the YAML frontmatter
   - If `source_title` is not already present, add `source_title: <title>` as well

7. Report success or any errors encountered, including the URL of the newly created document.
