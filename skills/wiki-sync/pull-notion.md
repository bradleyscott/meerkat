# Pull from Notion

Platform-specific pull instructions for Notion. Called by the `/pull` router command, which has already:
- Read the file and parsed frontmatter (`wiki_url` required)
- Detected the platform as Notion from the `wiki_url` domain

## Steps

1. Use `notion-fetch` with the Notion page URL to retrieve the page content in markdown format.

2. **Add H1 heading from page title**:
   - Get the page title from the response
   - Check if the content already starts with an H1 heading that matches the title
   - If not, prepend `# {page_title}\n\n` to the content

3. **Ask about converting Notion page URLs to relative markdown links**:
   - Ask the user: "Convert Notion page links to relative markdown links?"
   - If the user says yes, perform the conversion:
     a. Build a reverse lookup map by scanning all markdown files in the repository:
        - Use Glob to find all `**/*.md` files
        - Read each file's frontmatter to extract `wiki_url`
        - Build a map: `wiki_url` → `file_path`
     b. Scan the pulled content for Notion page URLs matching patterns like:
        - `https://www.notion.so/...`
        - `https://notion.so/...`
     c. For each Notion URL found in markdown links `[text](url)`:
        - Look up the URL in the reverse lookup map
        - If found, calculate the relative path from the current file to the target file
        - Replace the absolute Notion URL with the relative path
        - If not found in the map, leave the URL unchanged
   - If the user says no, skip link conversion entirely

4. **Keep Notion image URLs**:
   - Leave all image references as Notion cloud URLs so they render when viewing the markdown
   - Do NOT attempt to download images or convert to local paths

5. **Diff and confirm before updating**:
   - Compare the existing local content (everything after the frontmatter closing `---`) with the new transformed content from Notion
   - If the content is identical, report "Already up to date" and stop
   - If there are differences, present a clear summary to the user:
     - Show which sections were added, removed, or changed
     - For small changes, show the diff inline (use markdown code blocks with `-` and `+` prefixes)
     - For large changes, summarise the key differences (e.g. "3 sections added, 1 section removed, 2 sections modified")
   - Ask the user: "Apply these changes from Notion to the local file?"
   - If the user says no, report "Pull cancelled" and stop

6. **Update the local file** (only if user confirmed):
   - Preserve the original YAML frontmatter exactly as-is
   - Replace only the content that appears AFTER the closing `---` of the frontmatter
   - Use the Edit tool to replace the old content with the new transformed content

7. Report success and any warnings encountered.
