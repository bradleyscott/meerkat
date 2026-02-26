---
description: Pull content from Confluence wiki to local markdown file (project)
argument-hint: <file-path>
allowed-tools: Read, Edit, Glob, AskUserQuestion, mcp__mcp-atlassian__confluence_get_page
---

# Pull from Confluence

Pull content from a Confluence wiki page to the corresponding local markdown file.

## Instructions

1. Read the file at the provided path: $ARGUMENTS

2. Parse the YAML frontmatter (between the opening and closing `---` lines) to extract:
   - `confluence_url`: (required) The URL of the Confluence page to pull from
   - If `confluence_url` is not present, abort with an error message

3. Extract the page ID from the `confluence_url`. The URL format is typically:
   - `https://<domain>.atlassian.net/wiki/x/<shortcode>` - use the shortcode as the page_id
   - `https://<domain>.atlassian.net/wiki/spaces/<space>/pages/<page_id>/<title>` - use the page_id

4. Use `confluence_get_page` with the page_id to retrieve the page content:
   - Set `convert_to_markdown: true` to get markdown content
   - Set `include_metadata: true` to get the page title

5. **Add H1 heading from page title**:
   - Get the page title from the response metadata
   - Check if the content already starts with an H1 heading that matches the title
   - If not, prepend `# {page_title}\n\n` to the content

6. **Ask about converting Confluence page URLs to relative markdown links**:
   - Use AskUserQuestion to ask: "Convert Confluence page links to relative markdown links?"
     - Option 1: "Yes" - Convert links to local markdown files where possible
     - Option 2: "No" - Keep all Confluence URLs as-is
   - If the user selects "Yes", perform the conversion:
     a. Build a reverse lookup map by scanning all markdown files in the repository:
        - Use Glob to find all `**/*.md` files
        - Read each file's frontmatter to extract `confluence_url`
        - Build a map: `confluence_url` → `file_path`
     b. Scan the pulled content for Confluence page URLs matching patterns:
        - `https://<domain>.atlassian.net/wiki/spaces/.../pages/{pageId}/...`
        - `https://<domain>.atlassian.net/wiki/x/{shortcode}`
     c. For each Confluence URL found in markdown links `[text](url)`:
        - Look up the URL in the reverse lookup map
        - If found, calculate the relative path from the current file to the target file
        - Replace the absolute Confluence URL with the relative path (e.g., `./path/to/file.md` or `../other/file.md`)
        - If not found in the map, leave the URL unchanged
   - If the user selects "No", skip link conversion entirely

7. **Keep Confluence image URLs**:
   - Leave all image references as Confluence cloud URLs so they render when viewing the markdown
   - Do NOT attempt to download images or convert to local paths

8. **Update the local file**:
   - Preserve the original YAML frontmatter exactly as-is
   - Replace only the content that appears AFTER the closing `---` of the frontmatter
   - Use the Edit tool to replace the old content with the new transformed content

9. Report success and any warnings encountered.
