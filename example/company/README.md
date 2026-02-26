# Company Context

This directory is for files that describe your company — its profile, financials, strategy, and revenue model. Skills use this to ground their recommendations in your company's real situation.

## What to Include

- **Company profile** — Overview, products, customers, financials, competitive landscape (see the template in `skills/research-competitors/references/`)
- **Revenue model** — How you make money, pricing tiers, unit economics, revenue mix evolution
- **Strategy** — Vision, strategic pillars, key initiatives, TAM, partnerships, risks
- **Source documents** — Drop annual reports, strategy decks, and investor presentations into a `context/` subfolder as PDFs

## File Formats

The company profile uses the same YAML frontmatter as competitor profiles:

```yaml
---
company: Your Company Name
website: https://www.example.com
feed_url:
linkedin: https://www.linkedin.com/company/your-company
confluence_title:
confluence_url:
---
```

Strategy and revenue model files use document frontmatter:

```yaml
---
title: Revenue Model
confluence_title:
confluence_url:
---
```

## Why This Matters

When skills read your company context, they can:

- Compare your position against competitors with real data
- Ground opportunity analysis in your actual strategic direction and constraints
- Identify assumptions that conflict with your financial reality
- Recommend validation approaches appropriate to your company's stage and resources

## Example Files

- [acme-anvils.md](acme-anvils.md) — Full company profile with financials, products, customers, and competitive landscape
- [revenue-model.md](revenue-model.md) — Revenue streams, pricing, unit economics, and business model evolution
- [strategy.md](strategy.md) — Strategic pillars, TAM analysis, partnerships, and risks to monitor
