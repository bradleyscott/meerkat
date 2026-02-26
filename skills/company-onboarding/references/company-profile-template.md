# Company Profile Template

Use this template to structure the company profile document. Populate sections from the conversation, source documents, and research. Mark sections that lack information with `<!-- TODO: ... -->` HTML comments.

## Frontmatter

```yaml
---
company: {Full Company Name}
website: {URL}
feed_url:
linkedin: {LinkedIn company URL}
confluence_title:
confluence_url:
---
```

## Sections

### Company Overview

2–3 paragraphs covering:

- What the company does (plain language)
- Headquarters, founding date, approximate employee count
- Key business segments or divisions
- Market position and any notable milestones

### Funding Structure

- Ownership type: public (ticker, exchange), private, VC-backed, etc.
- Key funding milestones (IPO, funding rounds)
- Current capital structure table (if public):

| Metric | Value |
|--------|-------|
| Market Capitalisation | |
| Net Cash Position | |
| Debt | |
| Shares Outstanding | |

- Major shareholders (if known)
- Strategic investments and partnerships

### Financial Performance

Key financial metrics and growth trajectory. Use a table:

| Metric | FY{year} | FY{year} |
|--------|----------|----------|
| Revenue | | |
| Recurring Revenue | | |
| EBITDA | | |
| NPAT | | |
| Cash | | |

Key financial characteristics as bullet points (growth rates, revenue mix, margins, guidance).

Always specify currency for financial figures.

### Products

Core platform and product suite. Start with an overview paragraph, then use a table:

| Component | Description |
|-----------|-------------|
| | |

Include any innovation or R&D initiatives if known.

### Customers

- Target customer segments
- Notable customer relationships (with context on depth of relationship)
- Geographic revenue split (if known)

### Revenue Model

Brief overview of revenue streams — keep this high-level. The full detail goes in `revenue-model.md`.

- Recurring revenue streams and approximate mix
- Non-recurring revenue streams
- Pricing structure (if publicly available)

### Employee Sentiment

If available from Glassdoor or similar sources:

- Overall rating
- Key positive and negative themes
- Stats table:

| Metric | Score |
|--------|-------|
| Overall Rating | |
| Would recommend to a friend | |
| Work-life balance | |
| Culture and values | |
| Career opportunities | |

### Competitive Landscape

Brief overview of the competitive environment. Keep this high-level — detailed competitor profiles belong in the `competitors/` directory.

- Market structure (who plays where)
- Primary competitors table:

| Competitor | Overview | Strengths | Weaknesses |
|------------|----------|-----------|------------|
| | | | |

- Company's competitive position: advantages and disadvantages

### Summary for Competitive Analysis

SWOT-style summary table for quick reference:

| Category | Details |
|----------|---------|
| Strengths | |
| Weaknesses | |
| Opportunities | |
| Threats | |
