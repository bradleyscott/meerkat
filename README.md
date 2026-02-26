<p align="center">
  <img src="brand/logo.svg" alt="Meerkat" width="200">
</p>

<h1 align="center">Meerkat</h1>

<p align="center">
  <em>Always on the lookout — so you build the right thing.</em>
</p>

---

A framework that turns AI coding assistants into strategic thinking partners for product managers. Clone this repo, add your company context, and get structured skills for opportunity exploration, assumption testing, competitive intelligence, and validation planning — grounded in your real situation, not generic advice.

## The Problem

There's no shortage of AI tools that help PMs write PRDs, generate wireframes, or prototype features. But far fewer help with the harder upstream question: *are you building the right thing?* That's the decision with the highest leverage — and the one where PMs most often fly blind.

LLMs give frustratingly generic strategy advice because they don't know your company, your competitors, your constraints, or your customers. The knowledge that makes a PM effective — competitive positioning, customer pain points, strategic priorities, team capacity are often not avaliable to your LLM.

I built this because I wanted an AI thinking partner that could help me apply product management best practice and accelerate my work. [Read more about why this exists.](why-i-built-this.md)

## What You Get

### Opportunity Pipeline

Four skills that compose into a pipeline, taking you from raw customer interviews through to a validated experiment plan:

```
/extract-insights ──→ /opportunity-interview → /identify-assumptions → /suggest-validation
                  └─→ /identify-assumptions   (direct risk analysis on any document)
```

- **Insights Extractor** (`/extract-insights`) — Analyses interview transcripts with rigorous provenance tracking. Every insight traces back to a verbatim quote and a specific participant.
- **Opportunity Interviewer** (`/opportunity-interview`) — A Socratic interview that pushes you to articulate and defend your product idea. It asks about past behaviour, not hypotheticals.
- **Assumption Identifier** (`/identify-assumptions`) — Reads any product document and surfaces hidden risks across desirability, viability, feasibility, and usability. Maps them on a 2x2 matrix of importance vs. evidence to help you focus on the riskiest assumptions.
- **Validation Suggester** (`/suggest-validation`) — Designs targeted experiments matched to the nature of each assumption and your specific context.

Each skill can be used independently, but they're designed to flow together — the output of one becomes the input for the next.

### Competitive Intelligence

Two skills for building and maintaining a competitive picture:

- **Research Competitors** (`/research-competitors`) — Deep-dive profiling of a single competitor: products, financials, customers, employee sentiment, feature comparison, and a strategic threat assessment.
- **Monitor Competitors** (`/monitor-competitors`) — Autonomous scanning of all tracked competitors via Google Alerts and web sources. Classifies findings by urgency (Act Now / Discuss / FYI), updates competitor files, and (optionally) posts updates to Slack.

### Industry Intelligence

Two skills that mirror the competitive intelligence pattern for broader market context:

- **Research Industry** (`/research-industry`) — Discovers and curates industry sources organised around 3-7 strategic topics derived from your company strategy. You confirm and supplement what AI finds.
- **Monitor Industry** (`/monitor-industry`) — Autonomous scanning of curated sources for new developments. Writes dated digest files and posts strategic implications to Slack.

Browse the [example content](example/) (a fictional company called Acme Anvils) to see what this looks like in practice.

## Quick Start

```bash
git clone <repo-url> my-pm-context
cd my-pm-context
cp config.json.example config.json
```

Then in [Claude Code](https://claude.ai/code) or [Cursor](https://cursor.com):

1. Run `/onboard` — a guided conversation that captures your company, product, and role context, then builds your workspace (this populates `config.json` for you)
2. Run `/opportunity-interview` to explore your first product idea
3. Run `/research-competitors` to profile a key competitor

Slash commands work out of the box with both **Claude Code** and **Cursor** — no extra configuration needed. For Amazon Q or other AI coding tools, see the [skills setup guide](skills/README.md#setting-up-skills-in-ai-coding-tools).

## How It Works

The framework separates **reusable capabilities** (skills, templates) from **your company context** (profiles, research, strategy). Your data is gitignored, so pulling upstream updates is clean:

```bash
git pull origin main
```

### Directory Structure

| Directory | Tracked | Purpose |
|-----------|---------|---------|
| `skills/` | Yes | Reusable skill definitions ([full reference](skills/README.md)) |
| `example/` | Yes | Demo content (Acme Anvils) |
| `{your-company}/company/` | No | Your company research and context |
| `{your-company}/competitors/` | No | Your competitor profiles |
| `{your-company}/product/` | No | OKRs, positioning, roadmap, and vision documents |
| `{your-company}/personas/` | No | User and buyer role personas |
| `{your-company}/industry/` | No | Industry landscape and monitoring digests |
| `{your-company}/role/` | No | Your role-specific context |
| `{your-company}/outputs/` | No | Generated documents from skill runs |

## Integrations

**Confluence** — Sync documents to and from your wiki with `/push-to-confluence` and `/pull-from-confluence`. Requires the [mcp-atlassian](https://github.com/sooperset/mcp-atlassian) MCP server.

**Slack** — The monitoring skills (`/monitor-competitors`, `/monitor-industry`) can post updates to Slack channels via the [Slack MCP server](https://docs.slack.dev/ai/slack-mcp-server/).

Both Claude Code and Cursor support MCP servers. To configure integrations, copy the example MCP config and fill in your credentials:

```bash
# Claude Code
cp .mcp.json.example .mcp.json

# Cursor — copy to the Cursor-specific location
cp .mcp.json.example .cursor/mcp.json
```

All config files (`config.json`, `.mcp.json`, `.cursor/mcp.json`) are gitignored — your credentials stay local.

## Extending

See [skills/README.md](skills/README.md) for the full skill reference, setup instructions for different AI coding tools, and guidance on creating your own skills.

## Example Content

The [example/](example/) directory contains a complete set of demo content for **Acme Anvils Corp**. Browse it to see the expected format for [company profiles](example/company/acme-anvils.md), [competitor research](example/competitors/), [OKRs](example/product/okrs.md), [roadmaps](example/product/roadmap.md), [vision documents](example/product/vision/), [personas](example/personas/), and [industry intelligence](example/industry/).

## License

MIT
