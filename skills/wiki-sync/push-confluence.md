# Push to Confluence

Platform-specific push instructions for Confluence. Called by the `/push` router command, which has already:
- Read the file and parsed frontmatter (`wiki_url`, `wiki_title`)
- Determined the page title
- Extracted markdown content after frontmatter
- Removed the leading H1 heading (if applicable)

Continue from here with the prepared content.

## Steps

1. **Replace relative links with Confluence URLs**:
   - Scan the markdown content for relative links matching the pattern `[text](./path/to/file.md)` or `[text](../path/to/file.md)` or `[text](path/to/file.md)`
   - For each relative link found:
     a. Resolve the full path relative to the current file's directory
     b. Read that target file's YAML frontmatter
     c. Extract the `wiki_url` value from the target file's frontmatter
     d. If a `wiki_url` exists, replace the relative link with the Confluence URL
     e. If no `wiki_url` exists in the target file, leave the link unchanged and note a warning
   - This ensures links remain navigable when the markdown is pushed to Confluence

2. **Detect image references in markdown**:
   - Scan the markdown content for image patterns: `![alt text](path/to/image.ext)`
   - Match common image extensions: png, jpg, jpeg, gif, svg, webp
   - For each image reference, extract the filename from the path (e.g., `./images/diagram.png` → `diagram.png`)
   - Store the list of image filenames referenced in the document for use in step 4

3. If `wiki_url` EXISTS in the frontmatter:
   - Extract the page ID from the URL. The URL format is typically:
     - `https://<domain>.atlassian.net/wiki/x/<shortcode>` - use the shortcode as the page_id
     - `https://<domain>.atlassian.net/wiki/spaces/<space>/pages/<page_id>/<title>` - use the page_id
   - Use `confluence_get_page` with the page_id to retrieve the page metadata, including attachments
   - Build a map of attachment filenames from the response's `attachments` array

4. **Rewrite image references to Confluence attachment URLs** (only when `wiki_url` exists):
   - For each image reference found in step 2:
     a. Check if an attachment with that filename exists (from step 3's attachment list)
     b. If attachment EXISTS:
        - Extract the Confluence domain from the file's `wiki_url` (e.g., `https://mycompany.atlassian.net/wiki/...` → `mycompany.atlassian.net`)
        - Replace `![alt](./filename.png)` with `![alt](https://{domain}/wiki/download/attachments/{pageId}/filename.png)`
        - Use the page_id extracted in step 3
     c. If attachment DOES NOT EXIST:
        - Leave the image reference unchanged in the content
        - Add the filename to a list of missing attachments
   - After processing all images, if any attachments are missing, output a warning:
     ```
     Warning: The following images are referenced but not found as attachments:
       - missing-image.png
     Upload these files to the Confluence page manually, then re-run /push
     ```

5. **Diff and confirm** (only when `wiki_url` EXISTS — i.e. updating an existing page):
    - Extract the current page body content from the `confluence_get_page` response in step 3 (the API returns the page content)
    - Compare the current Confluence content against the new markdown content (from steps 1–4)
    - Display the differences to the user in a unified-diff style format:
      - Lines removed from the current Confluence page: prefix with `- `
      - Lines added in the new local version: prefix with `+ `
      - Unchanged lines shown for context (2–3 surrounding lines), prefixed with a space
      - Group changes into hunks with `@@ ... @@` headers, like a git diff
    - Before diffing, normalize both texts to reduce noise:
      - Trim trailing whitespace from each line
      - Collapse runs of 3+ blank lines into 2
      - Ignore differences that are only whitespace or blank-line count changes
    - If there are **no meaningful differences**, report "No changes to push — Confluence page is already up to date." and stop
    - If there **are** differences, display the diff and ask the user:
      ```
      The above changes will be pushed to Confluence. Proceed? (yes/no)
      ```
    - If the user answers **no**, stop without making changes
    - If the user answers **yes**, continue to step 6

6. Use `confluence_update_page` to update the page with:
     - `page_id`: The ID extracted from the wiki_url
     - `title`: The determined page title
     - `content`: The markdown content (with image links rewritten)

7. If `wiki_url` does NOT exist in the frontmatter:
    - If any image references were found in step 2, output a warning before creating the page:
      ```
      Note: This document contains images that won't display until uploaded to Confluence.
      After the page is created, upload these files as attachments, then re-run /push:
        - image1.png
        - image2.png
      ```
    - **Load Confluence configuration:** Read `config.json` from the meerkat project root to get `confluence.space_key` and `confluence.parent_id`. If the file does not exist or the confluence fields are empty, ask the user for:
      - Their Confluence space key (e.g., `~612345abcdef` for a personal space, or `TEAM` for a team space)
      - The parent page ID under which new pages should be created (the numeric ID from the page URL)
      - Save these values to the `confluence` object in `config.json` for future use
    - Use `confluence_create_page` to create a new page with:
      - `space_key`: from `config.json`
      - `parent_id`: from `config.json`
      - `title`: The determined page title
      - `content`: The markdown content (image links unchanged since no attachments exist yet)
    - After successful creation, update the original markdown file's frontmatter:
      - Extract the page URL from the API response (look for `_links.base` + `_links.webui`, or construct from the page `id`)
      - Use the Edit tool to add `wiki_url: <new-page-url>` to the YAML frontmatter

8. Report success or any errors encountered.
