---
name: check-prd-ready
description: >
  Reviews an opportunity or PRD document for delivery readiness — checks it against the
  sections a delivery-ready document should contain, flags gaps by severity, and produces
  a readiness assessment. Use when a PM has been iterating on a document with designers
  and engineering leads and wants to verify nothing major has been missed before handing
  off to engineering.
argument-hint: "[document-path or source-url]"
compatibility: Designed for Claude Code (or similar products)
metadata:
  author: meerkat
  version: "1.0"
---

# Check PRD Ready

Review an opportunity or PRD document for delivery readiness. This is a readiness audit, not a content-building interview — the PM has been updating the document as they work with designers and engineering leads. This skill checks what they have against what a delivery-ready document should contain, and flags gaps.

Be constructively challenging — push back on vague or missing areas. The goal is to catch gaps before dedicated engineering work begins, not after.

## Workflow

Follow these steps in order:

```
Readiness Check Progress:
- [ ] Step 1: Load context
- [ ] Step 2: Read and understand the document
- [ ] Step 3: Triage relevant sections
- [ ] Step 4: Evaluate against readiness criteria
- [ ] Step 5: Present gap analysis
- [ ] Step 6: Address gaps (if PM chooses)
- [ ] Step 7: Save assessment
```

### Step 1: Load context

Read the relevant context files:

- `context/company/` — company profile, strategy, revenue model
- `context/competitors/` — competitor profiles
- `context/product/` — OKRs, positioning, roadmap, vision documents
- `context/role/` — PM's role context
- `context/personas/users/` and `context/personas/buyers/` — persona files (if they exist)

This context is needed to assess whether the document is grounded in real strategic and user context, not just to tick boxes.

### Step 2: Read and understand the document

Read the document the PM wants reviewed. Accept either:
- A **local file path** — read with the `Read` tool
- A **source URL** — detect the platform from the domain and fetch accordingly:
  - `atlassian.net` → `confluence_get_page`
  - `notion.so` → `notion-fetch`
  - Any other URL → `WebFetch`

Also look for related documents in the same folder or linked from the document:
- If an `assumptions.md` exists (from `identify-prd-assumptions`), read it
- If a `validation-plan.md` exists (from `suggest-discovery-plan`), read it
- If a `synthesis.md` exists (from `synthesise-research`), read it
- Follow any linked Figma prototypes, design docs, or technical designs mentioned in the document body

Summarise back to the PM what you found:
- What the document covers
- Which related documents exist
- A brief assessment of the current state (e.g., "The document has a clear problem statement and proposed solution, but I don't see design references or NFRs")

Confirm your understanding before proceeding.

### Step 3: Triage relevant sections

Read the [readiness checklist](references/readiness-checklist.md) and the [NFR taxonomy](references/nfr-taxonomy.md).

Before evaluating in depth, triage with the PM. Based on the nature of the feature:

1. Identify which checklist sections are likely relevant vs. clearly inapplicable (e.g., a backend-only change doesn't need UI design references; a read-only reporting feature probably doesn't need a complex rollout strategy)
2. For NFR categories specifically: identify which are relevant for this type of feature. Skip inapplicable ones entirely — no justification needed.
3. Present the triage: "Based on what I've read, these sections seem relevant: [list]. These likely don't apply: [list]. Agree, or should I adjust?"

Only evaluate the relevant sections in depth.

### Step 4: Evaluate against readiness criteria

For each relevant section, assess:
- **Present and sufficient** — the section exists and has enough depth and specificity
- **Present but partial** — the section exists but is vague, incomplete, or lacks measurable criteria
- **Missing** — the section doesn't exist or is empty

Use the probing questions from the [readiness checklist](references/readiness-checklist.md) to test whether each section meets the bar.

### Step 5: Present gap analysis

Present the readiness assessment grouped by severity:

- **Blockers** — must be resolved before handing off to engineering. These are gaps that would cause an engineering team to immediately ask "what does this mean?" or "what should happen here?" Examples: no design references at all for a UI feature, no success metrics, a critical NFR category unaddressed.
- **Should address** — should be resolved before or early in engineering. The team can start but will need answers before completing. Examples: some interactive states undocumented, rollout sequence unclear.
- **Nice to have** — would strengthen the document but won't block progress. Examples: competitive context could be richer, future extensibility intent not documented.

Present a coverage summary table at a glance, then detailed findings grouped by severity.

After presenting, ask the PM: "Would you like to work through any of these gaps now, or is this assessment what you needed?"

### Step 6: Address gaps (if PM chooses)

If the PM wants to address gaps in conversation:
- Work through them one at a time, starting with blockers
- Use the probing questions from the checklist to help the PM think through what's needed
- Capture their answers and draft the missing content
- Update the running assessment as gaps are resolved

If the PM prefers to address gaps on their own, that's fine — the assessment itself is the deliverable.

**Principle: audit, don't author.** Your job is to identify what's missing, not to fill it in yourself. The PM knows their feature better than you do. When gaps are found, probe for what's needed rather than generating content from thin air. The exception is when the PM explicitly asks you to draft a section — then draft it, but make clear it needs their review and validation.

### Step 7: Save assessment

Save the readiness assessment as `readiness-check.md` in the same folder as the opportunity document (e.g., `context/outputs/opportunities/{slug}/readiness-check.md`). If no opportunity folder exists, ask the PM where to save it.

Use this frontmatter:

```yaml
---
title: Readiness Check — [opportunity name]
date: [today's date]
source_document: [relative path to opportunity document]
status: [Ready / Blockers present / Assessment only]
source_url: ""
---
```

The `source_url` field is left blank for the PM to fill in if they want to push this to Confluence or Notion via `/push`.

**After saving, tell the PM:**
- If no blockers: "This document is ready for engineering. Share it with your engineering lead."
- If blockers present: "There are [N] blockers to resolve before handoff. Address these, then run `/check-prd-ready` again or proceed to engineering if you're confident the gaps are covered."

## Principles

- **Audit, don't author.** Identify what's missing; don't generate it unless asked. The PM has context you don't.
- **Business level only.** Never suggest technical solutions. "Search must return results in under 2 seconds" is a valid NFR. Saying which search technology to use is not. If the PM starts describing implementation, redirect: "That's an engineering decision — let's capture the business requirement."
- **Pragmatic, not exhaustive.** Triage first, depth only where it matters. A PM who finds this skill tedious will stop using it. The worst outcome is a check that's so burdensome it gets skipped.
- **Flag, don't block.** Open items should be surfaced clearly but shouldn't prevent the PM from completing the check. The PM and their engineering lead decide together what must be resolved before work begins.
- **Conscious exclusions beat silent gaps.** An NFR category explicitly marked "not applicable" is better than one that was never considered. A non-goal is better than an unstated assumption about scope.
