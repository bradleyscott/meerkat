# Source Discovery Guide

A reference for identifying and evaluating industry sources by type. Use this during Step 3 of the research-industry-sources skill.

## Source Types and What They Reveal

### Industry Analysts and Research Firms

**What they provide:** Market sizing, trend analysis, vendor rankings (Magic Quadrants, Waves), technology maturity assessments, strategic forecasts.

**How to find them:**
- Search for `"{industry}" analyst report` or `"{industry}" market research`
- Well-known firms: Gartner, Forrester, IDC, McKinsey, BCG, Deloitte, Accenture, PwC
- Domain-specific firms vary by industry — search for `"{industry}" research firm` to find specialists
- Look at "About the Author" sections in industry reports for individual analysts to follow

**Evaluation criteria:**
- Do they cover your specific market segment (not just the broader industry)?
- How frequently do they publish on your topics?
- Are their reports freely available, gated behind registration, or fully paywalled?

**Accessibility reality:** Most analyst reports are paywalled ($2,000–$10,000+). However:
- Executive summaries and press releases about reports are often free
- Analyst blog posts and conference presentations are typically free
- Knowing a report exists is useful — the PM may have corporate subscriptions

### Trade Publications and Industry News

**What they provide:** Breaking news, feature articles, interviews with industry leaders, event coverage, job market trends.

**How to find them:**
- Search for `"{industry}" news`, `"{industry}" magazine`, `"{industry}" trade journal`
- Check Wikipedia's list of trade magazines for your industry
- Look at what sources competitor blogs cite

**Evaluation criteria:**
- Publication frequency (daily/weekly is better for monitoring than quarterly)
- Editorial independence vs. sponsored content ratio
- Whether they have RSS feeds or email newsletters
- Geographic focus — ensure coverage of markets your company operates in

### Newsletters

**What they provide:** Curated summaries of industry developments, often with expert commentary. High signal-to-noise ratio because a human has already filtered.

**How to find them:**
- Search for `"{industry}" newsletter`, `"{topic}" weekly digest`
- Check Substack, Beehiiv, and LinkedIn newsletters for your industry
- Ask on industry subreddits: "What newsletters do you read?"

**Accessibility reality:** Newsletters are email-based and cannot be directly fetched by monitoring tools. However:
- Many newsletters have web archives that CAN be fetched
- Substack newsletters always have a public web version
- Record the web archive URL, not just the subscribe URL

### Regulatory Bodies and Government Agencies

**What they provide:** Policy changes, regulatory consultations, compliance requirements, market structure decisions. Often the highest-impact source for strategic planning.

**How to find them:**
- Search for `"{industry}" regulator`, `"{industry}" regulatory body {country}`
- Check government department websites for your industry
- Look for consultation papers, policy statements, and decision documents

**Evaluation criteria:**
- Directly relevant to your company's operating markets
- Publishes consultations and decisions (not just static information)
- Has an RSS feed or announcements page that can be monitored

**Note:** Regulatory sources are often the most actionable for "so what" analysis — a new regulation can directly affect product requirements, market entry, and competitive dynamics.

### Industry Associations and Standards Bodies

**What they provide:** Industry statistics, policy positions, standards updates, member directories, conference announcements.

**How to find them:**
- Search for `"{industry}" association`, `"{industry}" trade body`, `"{industry}" standards`
- Check if your company or competitors are members of any associations

**Evaluation criteria:**
- Do they publish useful data (market reports, benchmarks, surveys)?
- Do they influence standards or regulation your product must comply with?
- How active are they (regular publications vs. static website)?

### Conferences and Events

**What they provide:** Strategic direction signals from keynotes, new product announcements, networking context, panel discussions revealing industry sentiment.

**How to find them:**
- Search for `"{industry}" conference`, `"{industry}" summit`, `"{industry}" expo`
- Check where competitors present or exhibit
- Look at industry association event calendars

**Monitoring approach:** Conferences are periodic (usually annual), so they don't provide continuous signal. Instead:
- Record the conference name, typical date, and website
- During monitoring runs near conference dates, search for coverage and announcements
- Conference speaker lists and agenda topics are leading indicators of what the industry considers important

### Individual Thought Leaders

**What they provide:** Early trend signals, contrarian perspectives, industry commentary, opinions that shape discourse.

**How to find them:**
- Check who writes for the trade publications you've identified
- Search Twitter/X and LinkedIn for active voices on your topics
- Look at conference speaker lists
- Check who industry association boards include
- Search for `"{topic}" expert` or `"{topic}" thought leader`

**Evaluation criteria:**
- Active and publishing regularly (not dormant accounts)
- Genuine expertise vs. self-promotion
- Audience size and engagement (are others in the industry engaging with their content?)
- Do they have a blog, newsletter, or other monitorable output?

### Blogs

**What they provide:** In-depth analysis, practitioner perspectives, technical deep-dives, opinion pieces.

**How to find them:**
- Search for `"{topic}" blog`, `site:medium.com "{topic}"`, `site:substack.com "{topic}"`
- Check if analysts, thought leaders, or companies you've identified have blogs
- Look at blog rolls and recommended reading lists from known sources

**Evaluation criteria:**
- Publishing frequency and recency
- Depth and quality of analysis
- RSS feed availability (most blogs have RSS)

### Podcasts

**What they provide:** Long-form interviews and discussions, expert panels, trend analysis.

**How to find them:**
- Search for `"{industry}" podcast` on Apple Podcasts, Spotify, or Google
- Check if identified thought leaders host or appear on podcasts

**Monitoring approach:** Podcasts are harder to monitor via automated tools (audio content). However:
- Episode titles and descriptions are text-searchable
- Many podcasts publish show notes or transcripts
- Record the podcast feed URL for episode title monitoring

### Forums and Communities

**What they provide:** Unfiltered practitioner sentiment, emerging issues before they hit mainstream coverage, real-world implementation stories.

**How to find them:**
- Search `site:reddit.com "{topic}"` to find relevant subreddits
- Check Stack Exchange for industry-specific sites
- Look for specialist forums (every industry has niche forums)
- Check Discord and Slack communities

**Evaluation criteria:**
- Active community with regular posts
- Quality of discussion (informed practitioners vs. general audience)
- Relevance to your specific market segment

## Assessing Source Quality

When evaluating any source, consider:

| Factor | Strong Signal | Weak Signal |
|--------|--------------|-------------|
| **Frequency** | Publishes weekly or more | Last post 6+ months ago |
| **Specificity** | Covers your exact market segment | Covers the broad industry tangentially |
| **Evidence** | Data-driven, cites sources, names specifics | Vague generalisations, unsourced claims |
| **Independence** | Editorial content, not sponsored | Primarily vendor-sponsored content |
| **Accessibility** | Free or has web archive; has RSS feed | Paywalled with no free content |
| **Actionability** | Content that prompts strategic questions | Content that's interesting but not decision-relevant |

## Source Redundancy

Don't add sources that cover the same ground. If three publications all report the same industry news with similar depth, pick the best one and note the others as alternatives. The goal is a curated, high-signal source list — not a comprehensive directory.
