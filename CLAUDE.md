# CLAUDE.md

Operational guidance for AI coding assistants working in this repository. For user-facing documentation, see [README.md](README.md).

## Company Directory

Read `config.json` to get the `company_dir` value. Company data lives in these subdirectories:

- `{company_dir}/company/` — Company research and analysis
- `{company_dir}/company/context/` — Source documents (annual reports, strategy decks as PDFs)
- `{company_dir}/competitors/` — Subdirectories for each competitor
- `{company_dir}/product/` — OKRs, positioning, strategic roadmap, and vision documents
- `{company_dir}/product/vision/` — Deeper explorations of individual strategic bets
- `{company_dir}/industry/` — Industry landscape, curated sources, and monitoring digests
- `{company_dir}/personas/users/` — User role persona files (one per persona)
- `{company_dir}/personas/buyers/` — Buyer role persona files (one per persona)
- `{company_dir}/role/` — Role-specific context and notes
- `{company_dir}/outputs/` — Generated documents from skill runs

Other key directories:

- `skills/` — Reusable AI skill definitions (see skills/README.md)
- `example/` — Demo content (Acme Anvils) showing the expected format for all document types

Run `/onboard` to create the company directory and populate `config.json`.

## Document Format

### Competitor/Company Profiles

YAML frontmatter with:

- `company`: Company name
- `website`: Main website URL
- `feed_url`: Google Alerts RSS feed for monitoring
- `linkedin`: LinkedIn company page URL
- `wiki_title`: Title for wiki page (if synced)
- `wiki_url`: URL to corresponding wiki page (if synced)

### Internal Documents (OKRs, Strategy)

YAML frontmatter with:

- `title`: Document title
- `period`: Time period (e.g., "H1 FY26")
- `team`: Owning team
- `wiki_title` and `wiki_url`: For wiki sync

### Persona Documents

YAML frontmatter with:

- `persona`: Persona name
- `type`: `user` or `buyer`
- `wiki_title` and `wiki_url`: For wiki sync

## Wiki Integration

Documents sync to Confluence or Notion using unified push/pull commands. The platform is auto-detected from the `wiki_url` domain in frontmatter, or from `config.json` settings.

- `/push path/to/file.md` — creates or updates a wiki page (Confluence or Notion)
- `/pull path/to/file.md` — pulls content from the wiki page to the local file

Relative links between markdown files are automatically converted to wiki URLs when pushing, and back to relative paths when pulling.

On first use, you'll be prompted for platform-specific configuration (saved to `config.json`):
- **Confluence**: space key and parent page ID. Requires the `mcp-atlassian` MCP server with API token auth
- **Notion**: parent page ID. Uses Notion's hosted MCP server with OAuth — no API tokens needed

## Content Guidelines

When updating research files:

- Use markdown tables for structured data comparisons
- Include source links at the bottom of documents
- Date-stamp significant updates in the executive summary
- Financial figures should specify currency
- Maintain sections per the templates in skills/*/references/
