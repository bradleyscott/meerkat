# Competitor Research

This directory contains a subdirectory for each competitor you're tracking. Skills use these profiles for competitive analysis, positioning recommendations, and monitoring changes over time.

## Structure

Each competitor gets its own subdirectory with a `summary.md` file:

```
competitors/
  coyote-tech/
    summary.md
  roadrunner-systems/
    summary.md
```

## What to Include

Each competitor summary should cover:

- **Executive summary** — Who they are, why they matter, and current threat level
- **Overview** — Key facts, leadership, founding story
- **Funding & financials** — Ownership structure, funding rounds, revenue estimates
- **Products** — Product suite, technical capabilities, and a feature comparison against your offering
- **Customers** — Known customers, target segments, notable wins
- **Revenue model** — Pricing structure and business model
- **Employee sentiment** — Glassdoor ratings and key themes
- **Strengths and weaknesses** — Honest assessment of where they win and where they struggle
- **Strategic assessment** — Threat level, positioning implications, roadmap implications, and key watch areas

The full template is in `skills/research-competitors/references/`.

## File Format

Competitor profiles use YAML frontmatter with monitoring fields:

```yaml
---
company: Competitor Name
website: https://www.competitor.example.com
blog_url: https://www.competitor.example.com/blog
linkedin: https://www.linkedin.com/company/competitor
twitter: https://twitter.com/competitor
subreddit:
feed_url:
confluence_title:
confluence_url:
---
```

The `feed_url` field is used by the `/monitor-competitors` skill to check for new mentions via Google Alerts RSS feeds.

## Why This Matters

When skills read your competitor research, they can:

- Identify how opportunities position you against specific competitors
- Flag assumptions that depend on competitor behaviour
- Suggest validation experiments informed by competitive dynamics
- Generate up-to-date competitive positioning and talking points

## Example Files

- [coyote-tech/summary.md](coyote-tech/summary.md) — VC-backed AI drone startup disrupting traditional hardware
- [roadrunner-systems/summary.md](roadrunner-systems/summary.md) — Established prey evasion company expanding into guaranteed catch services
