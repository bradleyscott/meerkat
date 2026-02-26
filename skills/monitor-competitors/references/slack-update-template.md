# Slack Update Templates

## Single Update (Act Now)

```
:red_circle: *Act Now* | *{Competitor Name}* | {Event Category}

*What happened:*
{2-3 sentences describing the development factually. Include specific numbers, dates, and names.}

*So what:*
• {First strategic implication — what this means for our positioning, deals, or roadmap}
• {Second implication — be specific about affected markets, segments, or initiatives}
• {Third implication if needed}

*Recommended response:*
• {Specific, actionable recommendation with timeline}
• {Second recommendation if needed}

:page_facing_up: Updated profile: `competitors/{name}/summary.md`
Source: {primary source URL}
```

## Single Update (Discuss)

```
:large_yellow_circle: *Discuss* | *{Competitor Name}* | {Event Category}

*What happened:*
{2-3 sentences describing the development factually.}

*So what:*
• {Strategic implication — what this could mean and why it warrants discussion}
• {Second implication if needed}

:page_facing_up: Updated profile: `competitors/{name}/summary.md`
Source: {primary source URL}
```

## Consolidated Update (multiple competitors, multiple findings)

Use this format when a single monitoring run surfaces findings across multiple competitors.
Only include Act Now and Discuss items — FYI items are silently added to competitor files.

```
:satellite: *Competitive Intelligence Update* | {date}

---

:red_circle: *Act Now*

*{Competitor Name} — {Event headline}*
{2-3 sentence summary}
• *Implication:* {what this means for us}
• *Recommended response:* {specific action}

---

:large_yellow_circle: *Discuss*

*{Competitor Name} — {Event headline}*
{1-2 sentence summary}
• *Implication:* {what this could mean}

*{Another Competitor} — {Event headline}*
{1-2 sentence summary}
• *Implication:* {what this could mean}

---

:memo: *FYI items added to competitor profiles:* {count} updates across {n} competitors (no action needed)

All profiles updated in `competitors/`
```

## Event Categories

Use these standardised categories in the headline to make updates scannable:

| Category | Examples |
|----------|----------|
| Funding | New investment round, IPO filing, acquisition |
| Product Launch | New product, major feature release, platform pivot |
| Pricing Change | Price increase/decrease, new pricing model, free tier change |
| Market Expansion | Entry into new geography, new vertical, new customer segment |
| Partnership | Strategic alliance, technology partnership, channel deal |
| Leadership | CEO/CTO/CPO change, major hiring spree, layoffs |
| Customer Win/Loss | Major customer announcement, lost customer signal |
| Financial Results | Earnings, revenue milestones, profitability changes |
| Sentiment Shift | Glassdoor rating change, G2/Capterra trend shift, emerging customer complaints |
| Strategy Shift | Rebrand, pivot, new messaging, changed positioning |
