# Validation Techniques Reference

A library of techniques for testing product assumptions, organised by the risk category they best address. When recommending techniques, favour those that are fast, cheap, and provide strong signal relative to effort.

## Evidence Hierarchy

From weakest to strongest signal. Move up this hierarchy as quickly and cheaply as possible.

1. **Opinions** — What people say in interviews and surveys. Initial signal but poor predictor of behaviour.
2. **Demonstrated interest** — Landing page clicks, fake door tests. Slightly stronger.
3. **Behavioural commitment** — Email signups, waitlist joins, time investment. Real interest.
4. **Financial commitment** — Pre-sales, purchases, deposits. Strongest validation.

---

## Desirability (Value Risk) Techniques

### Customer Problem Interviews
- **What**: Explore problems, pain points, and current behaviours using past-tense questions about actual experiences. Never ask "would you use X?" — instead ask "tell me about the last time you needed to solve X."
- **When**: Pre-concept or early concept stage. When you need to validate the problem is real.
- **Effort**: 1-2 weeks, $0-500 (incentives)
- **Signal**: Weak-Moderate (opinions about past behaviour)
- **Watch out for**: Confirmation bias. Requires skilled interviewing. People describe idealised behaviour, not actual behaviour.

### Jobs-to-be-Done Interviews
- **What**: Deep interviews exploring the circumstances and motivations driving switching behaviour. Uncovers functional, social, and emotional dimensions of customer needs.
- **When**: When you need to understand *why* people would switch from current solutions.
- **Effort**: 2-3 weeks, $500-2,000
- **Signal**: Moderate (past switching behaviour is a strong predictor)
- **Watch out for**: Requires trained interviewers. Small sample sizes.

### Landing Page / Smoke Test
- **What**: Create a webpage explaining the concept with a call-to-action (email signup, "get early access"). Drive traffic via ads or organic channels. Measure conversion rates.
- **When**: Concept stage. When you want to measure interest before building anything.
- **Effort**: 1-2 days to build, 1-2 weeks to run, $100-1,000 (ads)
- **Signal**: Moderate (demonstrated interest, not commitment)
- **Watch out for**: Ad copy and page design heavily influence results. High signup rates don't guarantee paid conversion.

### Fake Door Test (Painted Door)
- **What**: Create UI elements for non-existent functionality, track clicks, show "coming soon" message. Measures feature-specific demand within an existing product.
- **When**: When testing demand for a specific feature within an existing product.
- **Effort**: 1-3 days to build, 1-2 weeks to run, minimal cost
- **Signal**: Moderate (behavioural interest in context)
- **Watch out for**: Overuse erodes user trust. Always handle the reveal gracefully — explain you're testing interest and offer beta access.

### Concierge MVP
- **What**: Manually deliver the service to a small number of customers. Customers know it's manual. AirBnB founders hosting guests themselves. Food on the Table's founder personally shopping with customers.
- **When**: When you need to deeply understand the customer experience and refine the value proposition before automating.
- **Effort**: 2-4 weeks of manual delivery, low direct cost but high time investment
- **Signal**: Strong (real usage, real feedback, real value exchange)
- **Watch out for**: Doesn't test whether an automated solution works. Manual quality may exceed what's achievable at scale.

### Wizard of Oz MVP
- **What**: Present a seemingly automated experience while humans perform backend work invisibly. Zappos posting shoe photos then buying from stores. CardMunch appearing to use OCR while using Mechanical Turk.
- **When**: When the automation/technology is expensive to build and you need to validate the customer experience first.
- **Effort**: 1-4 weeks to set up, ongoing manual effort, moderate cost
- **Signal**: Strong (validates whether customers will use the automated experience)
- **Watch out for**: Can be expensive to sustain. Ethical considerations around transparency.

### Pre-sales / Financial Commitment
- **What**: Ask customers to commit budget, place deposits, or pre-order before the product exists. B2B: pre-sales conversations with budget commitment. B2C: crowdfunding campaigns or early-bird pricing.
- **When**: When you need the strongest possible validation that people will pay.
- **Effort**: 2-4 weeks for sales conversations, variable cost
- **Signal**: Strong (financial commitment is the ultimate demand signal)
- **Watch out for**: Early adopters may not represent the mainstream market. Pre-sale terms may not reflect sustainable pricing.

### Survey / Quantitative Demand Assessment
- **What**: Structured survey measuring problem severity, willingness to pay, feature preferences across a larger sample. Can use techniques like MaxDiff or conjoint analysis for feature prioritisation.
- **When**: When you have hypotheses from qualitative research and need to quantify demand across a broader population.
- **Effort**: 1-2 weeks, $500-5,000 (depending on panel recruitment)
- **Signal**: Weak-Moderate (stated preferences, not behaviour)
- **Watch out for**: Survey design dramatically affects results. Hypothetical bias means stated willingness to pay often exceeds actual.

---

## Viability (Business Viability Risk) Techniques

### Unit Economics Modelling
- **What**: Build a spreadsheet model of CAC, LTV, LTV:CAC ratio, payback period, and margins. Run sensitivity analyses on key variables (churn, pricing, acquisition cost).
- **When**: Early concept stage. Before committing significant resources.
- **Effort**: 1-3 days, no direct cost
- **Signal**: Moderate (model quality depends on input assumptions)
- **Watch out for**: Models are only as good as their inputs. Small changes in churn (5% vs 3%) or CAC ($50 vs $100) can swing businesses from profitable to unsustainable.

### Pricing Research (Van Westendorp)
- **What**: Survey customers about four price points: too expensive, expensive but worth it, a bargain, and too cheap (questioning quality). Analyse curves to find the optimal price range.
- **When**: When you need to validate pricing assumptions before launch.
- **Effort**: 1-2 weeks, $500-2,000
- **Signal**: Moderate (stated price sensitivity, not actual purchase behaviour)
- **Watch out for**: Hypothetical bias. Context matters — B2B purchasing involves more stakeholders than the survey respondent.

### A/B Price Testing
- **What**: Test different price points with real purchase behaviour. Requires existing traffic or willingness to experiment publicly.
- **When**: When you have a live product or pre-sales channel and need to validate price sensitivity with real behaviour.
- **Effort**: 2-4 weeks, moderate cost (potential revenue impact)
- **Signal**: Strong (actual purchase decisions)
- **Watch out for**: Ethical and brand considerations of showing different prices. Requires sufficient volume for statistical significance.

### Business Model Canvas Review
- **What**: Systematically examine all nine components of the business model (customer segments, value propositions, channels, customer relationships, revenue streams, key resources, key activities, key partnerships, cost structure). Identify assumptions in each component.
- **When**: Early concept stage. When validating strategic and operational fit.
- **Effort**: Half-day workshop, no direct cost
- **Signal**: N/A (framework for identifying assumptions, not a test itself)
- **Watch out for**: Workshop quality depends on participant candour. Easy to gloss over uncomfortable assumptions.

### Stakeholder / Compliance Review
- **What**: Structured review with legal, compliance, finance, and operational stakeholders to validate organisational viability — can and will the company support this?
- **When**: Before committing significant resources, especially for ideas involving new data, new markets, or regulatory considerations.
- **Effort**: 1-2 weeks to schedule and conduct reviews
- **Signal**: High (internal stakeholders can identify hard blockers)
- **Watch out for**: Stakeholders may say "no" to manage risk rather than based on actual constraints. Distinguish between hard blockers and soft concerns.

### Competitive Strategy Assessment
- **What**: Analyse competitive landscape, switching costs, differentiation sustainability, and market dynamics. Assess whether the competitive advantage is real and defensible.
- **When**: When viability depends on competitive positioning.
- **Effort**: 1-2 weeks of research
- **Signal**: Moderate (analysis, not empirical test)
- **Watch out for**: Competitor intentions are hard to predict. Markets shift.

---

## Feasibility (Feasibility Risk) Techniques

### Technical Spike
- **What**: Time-boxed investigation (1-3 days max) exploring a specific technical unknown. Deliverable is information and recommendations, not working software.
- **When**: When a specific technical question needs answering before committing to an approach.
- **Effort**: 1-3 days of engineering time
- **Signal**: High for the specific question addressed
- **Watch out for**: Scope creep — spikes should answer a question, not build a feature. Time-box strictly.

### Proof of Concept (PoC)
- **What**: Build a minimal working version of the most uncertain technical component. Produces functioning code (not production-quality) demonstrating technical viability.
- **When**: When technical risks are substantial and a spike isn't sufficient — you need to see it working, not just researched.
- **Effort**: Days to weeks of engineering time
- **Signal**: Strong for technical viability
- **Watch out for**: PoCs can become prototypes that become products. Be clear about scope and disposability upfront.

### Architecture Review
- **What**: Bring technical experts together to evaluate proposed designs against scalability, security, maintainability, and performance requirements.
- **When**: Before significant implementation begins. When the solution involves new architecture patterns or significant changes to existing systems.
- **Effort**: 1-3 days to prepare and conduct
- **Signal**: High (expert assessment)
- **Watch out for**: Reviewers need sufficient context about the problem and constraints. Abstract architecture discussions without concrete requirements produce vague feedback.

### Vendor / Tool Evaluation
- **What**: Identify requirements, research build-vs-buy options, test leading candidates through trials and demos. Assess features, pricing, support quality, and integration effort.
- **When**: When the solution might be better served by existing tools or third-party services rather than custom development.
- **Effort**: 1-2 weeks
- **Signal**: Moderate-High (direct evaluation of alternatives)
- **Watch out for**: Vendor demos show best-case scenarios. Trial with realistic data and workflows.

### Integration Spike
- **What**: Specifically test connectivity, data format compatibility, and API behaviour of systems that need to integrate. A specialised form of technical spike focused on the boundary between systems.
- **When**: When the solution depends on integrating with external or internal systems with unknown behaviour.
- **Effort**: 1-3 days
- **Signal**: High for integration-specific questions
- **Watch out for**: Test environments may not reflect production behaviour. Edge cases in data formats often cause problems.

---

## Usability (Usability Risk) Techniques

### Cognitive Walkthrough
- **What**: Evaluators step through user workflows answering four questions at each step: Will users know what to do next? Will they see the relevant control? Will they recognise it's the right control? Will they understand the feedback?
- **When**: Early design stage. Works with paper sketches, wireframes, or high-fidelity designs.
- **Effort**: 2-4 hours per workflow, no direct cost
- **Signal**: Moderate (expert assessment, not real user behaviour)
- **Watch out for**: Experts think differently than actual users. Catches structural issues but misses domain-specific confusion.

### Heuristic Evaluation
- **What**: Examine designs against established usability principles (Nielsen's 10 heuristics). 3-5 independent evaluators collectively find 75-80% of usability problems.
- **When**: Early design stage. Good for catching broad issues before user testing.
- **Effort**: 1-2 days, no direct cost if using internal evaluators
- **Signal**: Moderate (expert evaluation against established principles)
- **Watch out for**: Evaluators may flag issues that don't matter to actual users. Prioritise findings before acting on all of them.

### Prototype Usability Testing
- **What**: Give real users task scenarios with a prototype (paper, wireframe, or high-fidelity) and observe without helping. Note confusion, errors, task completion rates, and time.
- **When**: Design stage, before development. Five users find ~85% of usability problems.
- **Effort**: 1-2 weeks from planning through analysis, $500-2,000
- **Signal**: Strong (real user behaviour with realistic tasks)
- **Watch out for**: Prototype fidelity affects results. Very low-fidelity prototypes may test comprehension of the prototype, not the concept. Facilitators must resist helping.

### Card Sorting / Tree Testing
- **What**: Card sorting: users group items into categories to inform information architecture. Tree testing: users find items in a proposed navigation structure.
- **When**: When the product has significant information architecture decisions — navigation, categorisation, terminology.
- **Effort**: 1-2 weeks, $200-1,000 (tools and recruitment)
- **Signal**: Moderate-Strong (task-based measurement of findability)
- **Watch out for**: Results are specific to the items and tasks tested. May not generalise to broader navigation scenarios.

### Five-Second Test
- **What**: Show a design to users for five seconds, then ask what they remember. Tests whether key information and purpose are communicated at a glance.
- **When**: When discoverability and first impressions matter — landing pages, dashboards, key UI states.
- **Effort**: 1-3 days, $100-500
- **Signal**: Moderate (immediate comprehension, not task completion)
- **Watch out for**: Tests comprehension only, not ability to complete tasks. Best as a complement to other usability methods.

### Post-Launch Analytics and Session Replay
- **What**: Track behavioural metrics (completion rates, time on task, error rates, feature adoption, user paths) and watch recordings of actual user sessions using tools like Hotjar, Contentsquare, or Amplitude.
- **When**: After launch. Reveals where users struggle with real data and real motivations.
- **Effort**: Ongoing, $0-500/month (tooling)
- **Signal**: Strong (actual behaviour in production)
- **Watch out for**: Analytics show *what* but not *why*. Combine with qualitative research to understand root causes.

### A/B Testing
- **What**: Compare design variations with live traffic, measuring task completion, error rates, time to completion, or satisfaction.
- **When**: Post-launch optimisation. Requires sufficient traffic for statistical significance.
- **Effort**: 2-4 weeks per test, moderate setup cost
- **Signal**: Strong (real behaviour, real goals, controlled comparison)
- **Watch out for**: Requires volume. Testing trivial variations wastes time. Focus on meaningful differences informed by prior research.
