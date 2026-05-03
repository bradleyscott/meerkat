# Assumption Mapping Guide

## What Is an Assumption Map?

An assumption map is a 2×2 matrix that helps product teams prioritise which assumptions to test first. It was created by Jeff Gothelf and popularised by David J. Bland. The two axes are:

- **Importance** (vertical axis): What happens if this assumption is false?
  - **High**: The product fails, the business case collapses, or users can't achieve their goals. This is a "leap of faith" assumption.
  - **Low**: Minor inconvenience, easy workaround, or the product still works with adjustments.

- **Evidence level** (horizontal axis): How much data supports this assumption?
  - **High**: Quantitative data, validated research, demonstrated user behaviour, financial commitments, or strong analogous evidence.
  - **Low**: Opinions, hunches, untested hypotheses, or "we think" statements with no supporting data.

## The Four Quadrants

```
                    Low Evidence          High Evidence
                ┌─────────────────┬─────────────────┐
High Importance │  🔴 TEST NOW    │  🟢 MONITOR     │
                │                 │                 │
                │  Leap-of-faith  │  Well-supported │
                │  assumptions.   │  but important. │
                │  Focus here.    │  Watch for      │
                │                 │  changes.       │
                ├─────────────────┼─────────────────┤
Low Importance  │  🟡 TEST IF     │  ⚪ IGNORE      │
                │  CONVENIENT     │                 │
                │                 │  Low stakes,    │
                │  Low stakes,    │  well-evidenced.│
                │  unvalidated.   │  Move on.       │
                │  Opportunistic. │                 │
                └─────────────────┴─────────────────┘
```

## How to Assess Importance

Ask: "If this assumption is wrong, what happens?"

**High importance indicators:**
- The entire value proposition depends on this being true
- Revenue model breaks if this is false
- Users cannot achieve their primary goal
- We'd need to fundamentally redesign the solution
- Regulatory or legal consequences if wrong
- Significant wasted investment if false

**Low importance indicators:**
- The product still works, just slightly differently
- Easy to adjust the approach later
- Affects a secondary use case or edge case
- Low financial exposure if wrong
- Can be fixed post-launch without major rework

## How to Assess Evidence Level

Ask: "What data supports this belief?"

**High evidence indicators:**
- Quantitative data from analytics, research, or market data
- Direct observation of user behaviour (not just stated preferences)
- Financial commitments (pre-sales, contracts, purchases)
- Validated through experiments (A/B tests, prototypes, pilots)
- Strong analogous evidence from comparable products/markets
- Expert consensus with supporting data

**Low evidence indicators:**
- "We think..." or "Users will probably..."
- Based on a single anecdote or conversation
- Stakeholder opinion without supporting data
- Assumed based on personal experience
- Extrapolated from a different context or market
- No one has actually asked users or customers
- Based on what competitors do (without understanding why)

## Writing Good Assumptions

Assumptions should be **concrete and falsifiable**. This means you could design an experiment to prove them true or false.

**Bad (vague, untestable):**
- "Users will like this feature"
- "The market is big enough"
- "We can build this"

**Good (specific, falsifiable):**
- "Utility billing managers at mid-tier retailers spend more than 2 hours per week manually handling billing exceptions"
- "At least 30% of existing customers on legacy plans would upgrade to a plan that includes automated exception handling at $X/month"
- "Our team can integrate with the SAP billing API within one sprint using our existing middleware layer"
- "New users can complete their first billing exception review without consulting help documentation"

## Tagging by Risk Category

Tag each assumption with its risk category to spot patterns:

- **[D]** Desirability / Value Risk
- **[V]** Viability / Business Risk
- **[F]** Feasibility Risk
- **[U]** Usability Risk

If one category dominates the 🔴 quadrant, that tells you where the idea is most vulnerable and where to focus validation effort.

## Common Pitfalls

- **Testing the easy stuff instead of the scary stuff.** Teams naturally gravitate toward feasibility spikes and usability tests because they're comfortable. But desirability and viability assumptions more often kill products.
- **Treating assumptions as facts.** Just because something was discussed in a meeting doesn't make it validated. Insist on evidence.
- **Not being specific enough.** "Users want this" isn't an assumption you can test. "Users in segment X will pay $Y for capability Z" is.
- **Ignoring the bottom-left quadrant entirely.** Low-importance, low-evidence assumptions occasionally contain hidden dependencies. Give them a quick scan.
- **Mapping once and never updating.** Assumption maps are living artefacts. Update them as evidence accumulates, as context changes, and as new assumptions emerge.
