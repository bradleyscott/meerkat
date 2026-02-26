# Product Strategy

This directory is for documents that describe your product's strategic direction — OKRs, positioning, roadmaps, and vision documents. Skills use this to align their recommendations with what you're actually trying to achieve.

## What to Include

- **OKRs** — Objectives and key results for the current period, with owners and rationale
- **Positioning** — Competitive positioning guide with head-to-head comparisons and talking points
- **Roadmap** — Integrated strategic roadmap showing Now / Next / Later priorities across your full scope
- **Vision documents** — Deeper explorations of specific strategic bets (e.g., AI strategy, market entry plans), one file per bet in the `vision/` subfolder

## Structure

```text
product/
├── okrs.md              # Team-level objectives and key results
├── positioning.md       # Competitive positioning and sales talking points
├── roadmap.md           # Integrated strategic roadmap
└── vision/
    ├── ai-targeting.md  # Vision for AI-powered predictive targeting
    └── urban-market.md  # Vision for urban pest control market entry
```

## Why one roadmap, not per-product?

If you own multiple product areas, you might be tempted to create separate folders or roadmaps for each. Resist that instinct — here's why:

- **The roadmap IS the integrated view.** The whole point is showing how you balance competing priorities across your scope with shared capacity. Per-product roadmaps hide the trade-offs that drive real prioritisation decisions.
- **OKRs are team-level.** They span your full scope and often include cross-functional work. Splitting them per-product creates artificial boundaries.
- **Positioning is competitive, not product-scoped.** It's about how your portfolio competes. Fragmenting it loses the cross-product story.
- **Vision documents already provide per-bet separation.** Each vision doc explores one strategic direction in depth — that's the right level of granularity.

If you truly own independent products (separate markets, separate teams, separate competitive dynamics), you likely need a separate company directory for each — not just subfolders. At that point, you're effectively acting as two PMs.

## File Format

Product documents use YAML frontmatter:

```yaml
---
title: OKRs
period: H1 FY26
team: Product Development
confluence_title:
confluence_url:
---
```

Vision documents follow the same pattern:

```yaml
---
title: "Vision: AI-Powered Predictive Targeting"
confluence_title:
confluence_url:
---
```

## Why This Matters

When skills read your product strategy, they can:

- Evaluate opportunities against your current OKRs and priorities
- Identify assumptions embedded in your strategic plans and vision documents
- Recommend validation approaches that align with your roadmap timeline
- Flag conflicts between new opportunities and existing commitments
- Assess whether a new bet fits your current capacity and trade-off landscape

## Example Files

- [okrs.md](okrs.md) — Quarterly objectives and key results with owners and success metrics
- [positioning.md](positioning.md) — Competitive positioning guide with head-to-head comparisons and sales talking points
- [roadmap.md](roadmap.md) — Integrated strategic roadmap with Now / Next / Later horizons and trade-off analysis
- [vision/ai-targeting.md](vision/ai-targeting.md) — Vision for AI-powered predictive targeting: hypothesis, success metrics, unknowns, and risks
- [vision/urban-market.md](vision/urban-market.md) — Vision for urban pest control market entry: opportunity, competitive context, and validation approach
