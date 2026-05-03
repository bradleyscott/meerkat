# Pull from Google Docs

Platform-specific pull instructions for Google Docs. Called by the `/pull` router command, which has already:
- Read the file and parsed frontmatter (`source_url` required)
- Detected the platform as Google Docs from the `source_url` domain

## Steps

1. **Extract the file ID** from the `source_url`. Google Docs URLs follow these patterns:
   - `https://docs.google.com/document/d/{fileId}/edit`
   - `https://docs.google.com/document/d/{fileId}/view`
   - `https://drive.google.com/file/d/{fileId}/view`
   - `https://drive.google.com/open?id={fileId}`

   In all cases, extract the `{fileId}` segment.

2. Use `mcp__claude_ai_Google_Drive__download_file_content` with the file ID to retrieve the document content. Request markdown or plain text format if the tool allows specifying an export format.

3. If the download returns HTML or another format rather than plain text, convert it to clean markdown:
   - Headings: `<h1>` → `#`, `<h2>` → `##`, etc.
   - Bold: `<strong>` or `<b>` → `**text**`
   - Italic: `<em>` or `<i>` → `*text*`
   - Lists: `<ul>`/`<li>` → `- item`, `<ol>`/`<li>` → `1. item`
   - Links: `<a href="url">text</a>` → `[text](url)`
   - Tables: convert to markdown table syntax
   - Strip remaining HTML tags

4. **Get the document title** using `mcp__claude_ai_Google_Drive__get_file_metadata` with the file ID. Extract the `name` field.

5. **Add H1 heading from document title**:
   - Check if the content already starts with an H1 heading that matches the document title
   - If not, prepend `# {document_title}\n\n` to the content

6. **Ask about converting Google Docs URLs to relative markdown links**:
   - Ask the user: "Convert Google Docs links to relative markdown links?"
   - If the user says yes:
     a. Build a reverse lookup map by scanning all markdown files in the repository:
        - Use Glob to find all `**/*.md` files
        - Read each file's frontmatter to extract `source_url`
        - Build a map: `source_url` → `file_path`
     b. Scan the pulled content for Google Docs URLs
     c. For each Google Docs URL found in markdown links `[text](url)`:
        - Look up the URL in the reverse lookup map
        - If found, calculate the relative path from the current file to the target file
        - Replace the absolute URL with the relative path
        - If not found, leave unchanged
   - If the user says no, skip link conversion

7. **Keep Google Docs image URLs**:
   - Leave all image references as Google-hosted URLs so they render when viewing the markdown
   - Do NOT attempt to download images or convert to local paths

8. **Diff and confirm before updating**:
   - Compare the existing local content (everything after the frontmatter closing `---`) with the new transformed content
   - If the content is identical, report "Already up to date" and stop
   - If there are differences, present a clear summary to the user:
     - Show which sections were added, removed, or changed
     - For small changes, show the diff inline (use markdown code blocks with `-` and `+` prefixes)
     - For large changes, summarise the key differences
   - Ask the user: "Apply these changes from Google Docs to the local file?"
   - If the user says no, report "Pull cancelled" and stop

9. **Update the local file** (only if user confirmed):
   - Preserve the original YAML frontmatter exactly as-is
   - Replace only the content that appears AFTER the closing `---` of the frontmatter
   - Use the Edit tool to replace the old content with the new transformed content

10. Report success and any warnings encountered.
