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

Each competitor summary should cover (in this order):

- **TL;DR** — One-sentence description, where they lead, key threat, key advantage
- **Strategic assessment** — Threat level, where they win/lose, positioning in a live deal, roadmap implications, key watch areas
- **Value driver assessment** — How this competitor maps against your key value drivers
- **Recent developments** — Dated entries with confidence indicators (✅ Verified / 💬 Anecdotal / 🔍 Inferred)
- **Field intel from Slack** — First-hand signals from internal Slack channels
- **Products** — Product suite, technical capabilities, and a feature comparison against your offering
- **Customers** — Known customers, target segments, notable wins
- **Pricing intel** — Pricing structure, known deal sizes, field intelligence
- **Company overview** — Key facts (including revenue), leadership, funding history
- **Employee sentiment** — Glassdoor ratings and key themes
- **Competitive landscape** — How they position themselves and who they compete against

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
slack_channel:
refresh_due:
source_title:
source_url:
---
```

- `feed_url` — used by `/monitor-competitors` to check for new mentions via Google Alerts RSS feeds
- `slack_channel` — optional internal Slack channel for field intel (e.g. `#intel-competitor-name`); read by `/monitor-competitors` as an additional signal source
- `refresh_due` — date when the profile is due for its next research refresh

## Why This Matters

When skills read your competitor research, they can:

- Identify how opportunities position you against specific competitors
- Flag assumptions that depend on competitor behaviour
- Suggest validation experiments informed by competitive dynamics
- Generate up-to-date competitive positioning and talking points

## Example Files

- [coyote-tech/summary.md](coyote-tech/summary.md) — VC-backed AI drone startup disrupting traditional hardware
- [roadrunner-systems/summary.md](roadrunner-systems/summary.md) — Established prey evasion company expanding into guaranteed catch services
