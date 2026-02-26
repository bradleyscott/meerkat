---
description: Push a markdown file to Confluence wiki (project)
argument-hint: <file-path>
allowed-tools: Read, Edit, Glob, mcp__mcp-atlassian__confluence_get_page, mcp__mcp-atlassian__confluence_update_page, mcp__mcp-atlassian__confluence_create_page
---

# Push to Confluence

Push a markdown file to its corresponding Confluence page.

## Instructions

A file path must be provided in `$ARGUMENTS`. If not provided, ask the user for the file path.

1. Read the file at the provided path: $ARGUMENTS

2. Parse the YAML frontmatter (between the opening and closing `---` lines) to extract:
   - `confluence_url`: (optional) The URL of the Confluence page to update
   - `confluence_title`: (optional) The title to set for the page

3. Determine the page title:
   - If `confluence_title` exists in the frontmatter, use that value
   - Otherwise, find the first H1 heading (line starting with `#`) in the markdown content and use its text as the title

4. Extract the markdown content that appears AFTER the closing `---` of the frontmatter. Do NOT include the frontmatter in the Confluence content.

5. **Remove leading H1 heading from content**:
   - Check if the first non-empty line of the content is an H1 heading (line starts with `#` followed by a space)
   - Count the total number of H1 headings in the document
   - If the first content is an H1 AND there is only one H1 in the entire document:
     - Remove that H1 line from the content (the Confluence page title will serve as this heading)
     - Also remove any blank lines immediately following the removed heading (to avoid extra whitespace at the top)
   - Otherwise, leave the content unchanged

6. **Replace relative links with Confluence URLs**:
   - Scan the markdown content for relative links matching the pattern `[text](./path/to/file.md)` or `[text](../path/to/file.md)` or `[text](path/to/file.md)`
   - For each relative link found:
     a. Resolve the full path relative to the current file's directory
     b. Read that target file's YAML frontmatter
     c. Extract the `confluence_url` value from the target file's frontmatter
     d. If a `confluence_url` exists, replace the relative link with the Confluence URL
     e. If no `confluence_url` exists in the target file, leave the link unchanged and note a warning
   - This ensures links remain navigable when the markdown is pushed to Confluence

7. **Detect image references in markdown**:
   - Scan the markdown content for image patterns: `![alt text](path/to/image.ext)`
   - Match common image extensions: png, jpg, jpeg, gif, svg, webp
   - For each image reference, extract the filename from the path (e.g., `./images/diagram.png` → `diagram.png`)
   - Store the list of image filenames referenced in the document for use in step 9

8. If `confluence_url` EXISTS in the frontmatter:
   - Extract the page ID from the URL. The URL format is typically:
     - `https://<domain>.atlassian.net/wiki/x/<shortcode>` - use the shortcode as the page_id
     - `https://<domain>.atlassian.net/wiki/spaces/<space>/pages/<page_id>/<title>` - use the page_id
   - Use `confluence_get_page` with the page_id to retrieve the page metadata, including attachments
   - Build a map of attachment filenames from the response's `attachments` array

9. **Rewrite image references to Confluence attachment URLs** (only when `confluence_url` exists):
   - For each image reference found in step 7:
     a. Check if an attachment with that filename exists (from step 8's attachment list)
     b. If attachment EXISTS:
        - Extract the Confluence domain from the file's `confluence_url` (e.g., `https://mycompany.atlassian.net/wiki/...` → `mycompany.atlassian.net`)
        - Replace `![alt](./filename.png)` with `![alt](https://{domain}/wiki/download/attachments/{pageId}/filename.png)`
        - Use the page_id extracted in step 8
     c. If attachment DOES NOT EXIST:
        - Leave the image reference unchanged in the content
        - Add the filename to a list of missing attachments
   - After processing all images, if any attachments are missing, output a warning:
     ```
     Warning: The following images are referenced but not found as attachments:
       - missing-image.png
     Upload these files to the Confluence page manually, then re-run /push-to-confluence
     ```

10. Use `confluence_update_page` to update the page with:
     - `page_id`: The ID extracted from the confluence_url
     - `title`: The determined page title from step 3
     - `content`: The markdown content (with image links rewritten)

11. If `confluence_url` does NOT exist in the frontmatter:
    - If any image references were found in step 7, output a warning before creating the page:
      ```
      Note: This document contains images that won't display until uploaded to Confluence.
      After the page is created, upload these files as attachments, then re-run /push-to-confluence:
        - image1.png
        - image2.png
      ```
    - **Load Confluence configuration:** Read `config.json` from the project root to get `confluence.space_key` and `confluence.parent_id`. If the file does not exist or the confluence fields are empty, ask the user for:
      - Their Confluence space key (e.g., `~612345abcdef` for a personal space, or `TEAM` for a team space)
      - The parent page ID under which new pages should be created (the numeric ID from the page URL)
      - Save these values to the `confluence` object in `config.json` at the project root for future use
    - Use `confluence_create_page` to create a new page with:
      - `space_key`: from `config.json`
      - `parent_id`: from `config.json`
      - `title`: The determined page title from step 3
      - `content`: The markdown content (image links unchanged since no attachments exist yet)
    - After successful creation, update the original markdown file's frontmatter:
      - Extract the page URL from the API response (look for `_links.base` + `_links.webui`, or construct from the page `id`)
      - Use the Edit tool to add `confluence_url: <new-page-url>` to the YAML frontmatter

12. Report success or any errors encountered.
