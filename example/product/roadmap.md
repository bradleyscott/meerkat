---
title: Strategic Roadmap
period: FY26
team: AnvilOS Platform
confluence_title:
confluence_url:
---

# AnvilOS Platform — Strategic Roadmap

## Context

This roadmap covers Pat Hammer's full scope: the AnvilOS platform including AI targeting, enterprise migration, and urban market entry. It represents an integrated prioritisation across competing demands on shared engineering capacity (3 squads, 12 engineers).

The roadmap is deliberately one document rather than per-product — because the trade-offs between these initiatives are the whole point. Splitting them would hide the resource tensions that drive prioritisation decisions.

## Now (H1 FY26)

Active work with committed resources and delivery targets.

### AnvilOS 2.0 Launch

| Initiative | Target | Status |
|-----------|--------|--------|
| AI-powered predictive targeting | Q1 FY26 | In progress — model at 18% accuracy, target 22% |
| Enterprise client migration (batch 1) | Q2 FY26 | 15 clients identified, migration tooling in development |
| Platform stability for migration | Ongoing | 99.9% uptime target during migration period |

**Dependencies:** Reliability team (Sam Catapult) delivering platform stability improvements in parallel. Shared data analyst supporting both AI model training and failure analysis.

### Urban-Safe Variant (Discovery & MVP)

| Initiative | Target | Status |
|-----------|--------|--------|
| Urban-safe AnvilOS variant (no explosives, noise-dampened) | Q2 FY26 | Design phase — constraints defined |
| Urban pilot programme | Q2 FY26 | Targeting 3 pilot customers |
| Urban field trials | Q2 FY26 | 15% success rate target |

**Dependencies:** Budget approval for H2 expansion contingent on pilot results. CTO sign-off on urban deployment architecture.

## Next (H2 FY26)

Planned work with directional commitment. Scope and timing subject to H1 results.

### Enterprise Migration Scale-Up

- Expand migration programme from 15 to 50 enterprise clients
- Self-service migration tooling to reduce professional services dependency
- Success-based pricing model pilot (pay-per-catch) for 5 enterprise accounts

### AI Targeting v2

- Incorporate real-time weather and terrain data into targeting model
- Target 30% accuracy rate (up from 22% H1 target)
- Multi-species support — extend beyond roadrunner-specific models

### Urban Market Expansion (if pilots succeed)

- Scale from 3 to 15 urban customers
- Urban-specific prey behaviour models
- Partnership with city councils for pest control contracts

## Later (FY27+)

Strategic direction. Not yet committed — depends on how Now and Next play out.

### Platform Ecosystem

- Gadget Marketplace opening to third-party developers
- API-first architecture enabling partner integrations
- Predictive maintenance for hardware fleet based on AnvilOS telemetry

### International Expansion

- European market entry via Elmer Fudd GmbH partnership
- Southeast Asian market assessment
- Localised AnvilOS variants for regional prey species

### Adjacent Verticals

- Security and surveillance applications for AnvilOS targeting
- Construction and demolition use cases for precision hardware delivery
- Environmental management (invasive species control)

## Trade-offs and Constraints

| Tension | How we're managing it |
|---------|----------------------|
| Urban pilots vs. enterprise migration | Urban gets 1 squad in H1; enterprise gets 2. If urban pilots fail, capacity shifts to migration scale-up. |
| AI accuracy vs. platform stability | AI model improvements ship behind a feature flag. No accuracy experiments on production traffic during migration. |
| New features vs. reliability | Reliability team (Sam) owns stability. We coordinate on shared uptime targets but don't take engineering capacity from reliability work. |

## What's NOT on this roadmap

- **Hardware R&D** — Gadget Innovation Lab operates independently; we integrate their outputs into AnvilOS
- **Reliability programme** — Owned by Sam Catapult; tracked in their roadmap
- **Competitor response** — Reactive moves (e.g., matching Coyote Tech features) are handled through the competitive positioning process, not roadmapped in advance
