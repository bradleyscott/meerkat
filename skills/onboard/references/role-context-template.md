# Role Context Template

Use this template to structure the PM's role context document. This information is used by every skill to calibrate recommendations — team size affects what's realistic, influence boundaries affect what validation approaches make sense, and stakeholder context shapes how to frame strategic advice.

Populate from the conversation. Mark sections that weren't discussed with `<!-- TODO: ... -->` comments. A thin file with just role and team is still valuable.

## Frontmatter

```yaml
---
title: Role Context
---
```

## Sections

### Current Role

Role title and product/area ownership. One or two sentences.

Example: "Senior Product Manager, AnvilOS Platform — responsible for the core targeting and delivery management capabilities."

### Team

Who the PM works with directly. Include:

- Team size and roles (designers, analysts, engineers)
- Whether resources are dedicated or shared
- Any notable gaps or constraints

Example:
```
- 2 product designers
- 1 data analyst
- Shared engineering team (12 engineers across 3 squads)
```

### Scope

What the PM owns and their decision-making boundaries:

- What they can decide independently (e.g., backlog prioritisation, feature scoping)
- What needs approval and from whom (e.g., roadmap changes need VP sign-off)
- Reporting lines (direct and dotted-line)

Example: "Own the AnvilOS roadmap, backlog prioritisation, and stakeholder alignment. Report to VP Product. Dotted line to CTO on technical architecture decisions."

### Stakeholders

Key relationships and decision-makers:

- Who needs to approve or buy in to major decisions
- Cross-functional partners (engineering leads, design leads, sales, marketing)
- Any political dynamics that affect what's possible

This section is optional and sensitive — only include what the PM volunteers.

### Current Focus

What the PM is focused on this quarter or half. Bullet list of 2–4 priorities.

Example:
```
- AnvilOS 2.0 launch (AI-powered targeting)
- Enterprise client migration programme
- Reliability improvement initiative (cross-functional)
```

### Constraints

Any practical constraints that should inform recommendations:

- Budget limitations
- Timeline pressures or hard deadlines
- Headcount constraints
- Technical debt or platform limitations
- Organisational constraints (e.g., change freezes, compliance requirements)

This section is optional — only include what the PM volunteers. Don't probe if they seem reluctant.
