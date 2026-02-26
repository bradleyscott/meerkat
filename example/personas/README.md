# Personas

This directory contains persona documents for the user roles and buyer roles relevant to your product. Skills use these to ground opportunity analysis, assumption mapping, and validation planning in real user and buyer context.

## Structure

Personas are split into two subdirectories by type:

```text
personas/
├── users/
│   ├── field-operator.md       # A user who interacts with the product day-to-day
│   └── operations-manager.md   # A user who oversees operations and reporting
└── buyers/
    └── procurement-director.md # A buyer who makes purchasing decisions
```

## What to Include

Each persona should cover:

- **Role title** — What the person does and their relationship to your product
- **Role context** — Seniority, team, reporting lines, typical company size
- **Goals and motivations** — What success looks like for them
- **Pain points and frustrations** — What gets in the way today
- **Product interaction** — How they use (or would use) your product, key workflows, frequency
- **Decision-making context** — What influences their choices, who they consult, what they care about when evaluating solutions
- **Quotes or representative behaviours** — Grounding details that make the persona feel real

## File Format

Persona documents use YAML frontmatter:

```yaml
---
persona: "Field Operations Specialist"
type: user
confluence_title:
confluence_url:
---
```

The `type` field should be `user` (someone who uses the product) or `buyer` (someone who makes or influences the purchasing decision). Some personas may be both — pick the primary lens and note the overlap in the document.

## Why This Matters

When skills read your personas, they can:

- Evaluate opportunities through the lens of specific user and buyer needs
- Identify assumptions about user behaviour that need validation
- Recommend validation techniques appropriate to each persona (e.g., shadowing a field operator vs. interviewing a procurement director)
- Ground positioning and messaging in real buyer priorities
- Flag when a strategic bet serves one persona at the expense of another

## Example Files

- [users/field-operator.md](users/field-operator.md) — Front-line operator who deploys and manages anvil installations in the field
- [users/operations-manager.md](users/operations-manager.md) — Manager overseeing field operations and reporting
- [buyers/procurement-director.md](buyers/procurement-director.md) — Senior leader responsible for technology and equipment purchasing decisions
