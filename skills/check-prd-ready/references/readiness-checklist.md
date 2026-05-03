# Delivery Readiness Checklist

A delivery-ready opportunity or PRD document should address each of these sections well enough that an engineering team can begin work without needing to ask fundamental questions. Not every section applies to every feature — triage first.

---

## 1. Problem Statement

**What to look for:** A specific, evidenced description of the problem being solved. Not a solution description masquerading as a problem.

**Probing questions:**
- What specific problem are users experiencing? Can you describe it without mentioning the solution?
- What evidence exists that this is a real problem? (interviews, support tickets, analytics, direct observation)
- How severe is the problem? What happens when users can't solve it today?
- Who specifically has this problem? Is it the same people who will use the solution?

**Pass criteria:** The problem is clearly stated, distinguishable from the solution, and backed by at least some evidence.

---

## 2. Goals and Success Metrics

**What to look for:** Measurable outcomes — what does success look like and how will you know when you've achieved it?

**Probing questions:**
- What does success look like 3 months after launch?
- How will you measure it? What specific metrics will move?
- What's the baseline today?
- What's the minimum outcome that would make this feature worth building?

**Pass criteria:** At least one measurable success metric with a clear definition. Ideally a target value or directional expectation.

---

## 3. Target Users

**What to look for:** Specific user roles or personas — not "all users" or vague segments.

**Probing questions:**
- Who specifically will use this? What role do they have? What do they do day-to-day?
- Are these the same people who experience the problem, or different people?
- Are there users who are explicitly out of scope for this release?
- What permissions or access do they need?

**Pass criteria:** Named user roles or personas. If personas exist in `context/personas/`, cross-reference them.

---

## 4. Functional Requirements

**What to look for:** What the feature must do — concrete, testable statements. Not how to build it.

**Probing questions:**
- What are the core user actions? (e.g., "A user can create a new X with these fields")
- What are the edge cases? What happens when inputs are invalid, data is missing, or errors occur?
- Are there any business rules that must be enforced?
- What should the feature explicitly NOT do (non-goals — see section 10)?

**Pass criteria:** The core user flows are described with enough detail that someone could write acceptance criteria. Edge cases are addressed.

---

## 5. Design References

**What to look for:** Prototypes, mockups, wireframes, or design specifications that show how the feature looks and behaves.

**Probing questions:**
- Are there Figma prototypes or mockups for the main user flows?
- Do the designs cover all the states (empty state, loading, error, success)?
- Are there interactive states or animations that need to be described?
- Are the designs complete enough to begin implementation, or are they indicative only?

**Pass criteria:** Design references exist and cover the main user flows. Links are provided in the document. Note: for backend-only changes, this section may not apply.

---

## 6. Constraints and Dependencies

**What to look for:** Technical constraints, organisational constraints, external dependencies, and timeline considerations.

**Probing questions:**
- Are there existing systems, APIs, or data structures this must integrate with?
- Are there things this feature must not break?
- Are there dependencies on other teams or external vendors?
- Are there regulatory, legal, or compliance constraints?
- Are there timeline constraints (e.g., must ship before X event)?

**Pass criteria:** Known constraints are listed. Dependencies on other teams or systems are named. "None known" is an acceptable answer if the PM has actively considered this.

---

## 7. Non-Functional Requirements (NFRs)

Read [nfr-taxonomy.md](nfr-taxonomy.md) for the full taxonomy. Evaluate each relevant NFR category.

**Probing approach:** For each relevant category, ask: "What are the business-level requirements here?" Keep it at business requirements — not technical implementation.

**Pass criteria:** Relevant categories are addressed with business-level requirements. Inapplicable categories are noted as such (no justification needed — the conscious decision is what matters).

---

## 8. Analytics and Measurement Plan

**What to look for:** What events, metrics, or data will be tracked to understand adoption, usage, and impact.

**Probing questions:**
- What user actions should be instrumented? (e.g., feature opened, action completed, error encountered)
- What dashboards or reports will you use to monitor this post-launch?
- How will you know if something is going wrong after release?
- Are there any analytics events that need to be defined before development starts?

**Pass criteria:** Key events to track are identified. Connection to the success metrics in section 2 is clear.

---

## 9. Rollout Approach

**What to look for:** How the feature will be released — phasing, feature flags, target customers for early access, and any migration considerations.

**Probing questions:**
- Will this be released to all users at once or rolled out gradually?
- Are there specific customers or user segments for an early access or beta phase?
- Is a feature flag needed? Who controls it?
- Is there any data migration or backward compatibility concern?
- What's the rollback plan if something goes wrong?

**Pass criteria:** The release approach is described at a high level. If a phased rollout or beta is planned, the initial scope is defined.

---

## 10. Non-Goals

**What to look for:** An explicit statement of what this feature will NOT do — scope boundaries that the team has consciously decided.

**Probing questions:**
- What have you explicitly decided to leave out of scope for this release?
- Are there related features or use cases that might be assumed but are actually out of scope?
- Are there future iterations already in mind that this release should not try to address?

**Pass criteria:** At least 2-3 explicit non-goals or out-of-scope items. This section often prevents scope creep and engineering misunderstandings.

---

## Coverage Summary Table

Use this table to present the readiness assessment at a glance:

| Section | Status | Severity |
|---------|--------|----------|
| Problem statement | ✅ / ⚠️ / ❌ | — / Should address / Blocker |
| Goals and success metrics | ✅ / ⚠️ / ❌ | |
| Target users | ✅ / ⚠️ / ❌ | |
| Functional requirements | ✅ / ⚠️ / ❌ | |
| Design references | ✅ / ⚠️ / N/A | |
| Constraints and dependencies | ✅ / ⚠️ / ❌ | |
| NFRs | ✅ / ⚠️ / ❌ | |
| Analytics plan | ✅ / ⚠️ / ❌ | |
| Rollout approach | ✅ / ⚠️ / ❌ | |
| Non-goals | ✅ / ⚠️ / ❌ | |

Legend: ✅ Present and sufficient · ⚠️ Present but partial · ❌ Missing · N/A Not applicable
