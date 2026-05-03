# CLAUDE.md

Operational guidance for AI coding assistants working in this repository. For user-facing documentation, see [README.md](README.md).

## Company Directory

Company data lives in the `context/` directory at the repo root:

- `context/company/` — Company research and analysis
- `context/company/source-docs/` — Source documents (annual reports, strategy decks as PDFs)
- `context/competitors/` — Subdirectories for each competitor
- `context/product/` — OKRs, positioning, strategic roadmap, and vision documents
- `context/product/vision/` — Deeper explorations of individual strategic bets
- `context/industry/` — Industry landscape, curated sources, and monitoring digests
- `context/personas/users/` — User role persona files (one per persona)
- `context/personas/buyers/` — Buyer role persona files (one per persona)
- `context/role/` — Role-specific context and notes
- `outputs/` — Generated documents from skill runs

Other key directories:

- `skills/` — Reusable AI skill definitions (see skills/README.md)
- `example/` — Demo content (Acme Anvils) showing the expected format for all document types

Run `/onboard` to create the `context/` directory.

## Document Format

### Competitor/Company Profiles

YAML frontmatter with:

- `company`: Company name
- `website`: Main website URL
- `feed_url`: Google Alerts RSS feed for monitoring
- `linkedin`: LinkedIn company page URL
- `source_title`: Title for the source page (if synced)
- `source_url`: URL to corresponding source page (if synced)

### Internal Documents (OKRs, Strategy)

YAML frontmatter with:

- `title`: Document title
- `period`: Time period (e.g., "H1 FY26")
- `team`: Owning team
- `source_title` and `source_url`: For source sync

### Persona Documents

YAML frontmatter with:

- `persona`: Persona name
- `type`: `user` or `buyer`
- `source_title` and `source_url`: For source sync

## Source Sync

Documents sync to Confluence, Notion, and other sources using unified push/pull commands. The platform is auto-detected from the `source_url` domain in frontmatter.

- `/push path/to/file.md` — creates or updates a source page (Confluence, Notion, etc.)
- `/pull path/to/file.md` — pulls content from the source page to the local file

Relative links between markdown files are automatically converted to source URLs when pushing, and back to relative paths when pulling.

No upfront configuration required — platform credentials are handled by MCP servers, and parent page location is provided as a URL on first push.

## Content Guidelines

When updating research files:

- Use markdown tables for structured data comparisons
- Include source links at the bottom of documents
- Date-stamp significant updates in the executive summary
- Financial figures should specify currency
- Maintain sections per the templates in skills/*/references/
