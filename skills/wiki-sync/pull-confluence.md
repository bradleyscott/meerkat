# Pull from Confluence

Platform-specific pull instructions for Confluence. Called by the `/pull` router command, which has already:
- Read the file and parsed frontmatter (`wiki_url` required)
- Detected the platform as Confluence from the `wiki_url` domain

## Steps

1. Extract the page ID from the `wiki_url`. The URL format is typically:
   - `https://<domain>.atlassian.net/wiki/x/<shortcode>` - use the shortcode as the page_id
   - `https://<domain>.atlassian.net/wiki/spaces/<space>/pages/<page_id>/<title>` - use the page_id

2. Use `confluence_get_page` with the page_id to retrieve the page content:
   - Set `convert_to_markdown: true` to get markdown content
   - Set `include_metadata: true` to get the page title

3. **Add H1 heading from page title**:
   - Get the page title from the response metadata
   - Check if the content already starts with an H1 heading that matches the title
   - If not, prepend `# {page_title}\n\n` to the content

4. **Ask about converting Confluence page URLs to relative markdown links**:
   - Ask the user: "Convert Confluence page links to relative markdown links?"
   - If the user says yes, perform the conversion:
     a. Build a reverse lookup map by scanning all markdown files in the repository:
        - Use Glob to find all `**/*.md` files
        - Read each file's frontmatter to extract `wiki_url`
        - Build a map: `wiki_url` → `file_path`
     b. Scan the pulled content for Confluence page URLs matching patterns:
        - `https://<domain>.atlassian.net/wiki/spaces/.../pages/{pageId}/...`
        - `https://<domain>.atlassian.net/wiki/x/{shortcode}`
     c. For each Confluence URL found in markdown links `[text](url)`:
        - Look up the URL in the reverse lookup map
        - If found, calculate the relative path from the current file to the target file
        - Replace the absolute Confluence URL with the relative path (e.g., `./path/to/file.md` or `../other/file.md`)
        - If not found in the map, leave the URL unchanged
   - If the user says no, skip link conversion entirely

5. **Keep Confluence image URLs**:
   - Leave all image references as Confluence cloud URLs so they render when viewing the markdown
   - Do NOT attempt to download images or convert to local paths

6. **Diff and confirm before updating**:
   - Compare the existing local content (everything after the frontmatter closing `---`) with the new transformed content from Confluence
   - If the content is identical, report "Already up to date" and stop
   - If there are differences, present a clear summary to the user:
     - Show which sections were added, removed, or changed
     - For small changes, show the diff inline (use markdown code blocks with `-` and `+` prefixes)
     - For large changes, summarise the key differences (e.g. "3 sections added, 1 section removed, 2 sections modified")
   - Ask the user: "Apply these changes from Confluence to the local file?"
   - If the user says no, report "Pull cancelled" and stop

7. **Update the local file** (only if user confirmed):
   - Preserve the original YAML frontmatter exactly as-is
   - Replace only the content that appears AFTER the closing `---` of the frontmatter
   - Use the Edit tool to replace the old content with the new transformed content

8. Report success and any warnings encountered.
