# Skills

Detailed reference for all available skills. For an overview of the framework and quick start guide, see the [root README](../README.md).

Each skill is a structured prompt that guides an AI coding assistant through a specific PM workflow with domain expertise, templates, and reference material. Skills are **tool-agnostic by design** — they can be wired up to whichever AI coding tool you use.

## Company Directory Convention

Skills find your company data via `config.json` (created by `/onboard`). An example is provided at `config.json.example` — copy it and run `/onboard` to populate it, or edit it manually. See the [root README](../README.md#quick-start) for setup instructions.

## Available Skills

### Getting Started

| Skill                  | Purpose                                                                                                          | Input                    | Output                                                    |
|------------------------|------------------------------------------------------------------------------------------------------------------|--------------------------|-----------------------------------------------------------|
| **company-onboarding** | Sets up your workspace and populates foundational company context through guided conversation and optional research | Conversation with the PM | Company profile, strategy, revenue model, directory structure |

Run `/onboard` as your first step. The skill gathers basic information about your company and product, optionally researches public data to enrich the context, and creates the document structure that all other skills depend on. It can also be re-run to update or enrich existing context.

### Opportunity Pipeline

These skills compose into a pipeline, with each skill's output feeding the next:

```
insights-extractor ──→ opportunity-interviewer → assumption-identifier → validation-suggester
                   └─→ assumption-identifier   (direct risk analysis)
```

| Skill | Purpose | Input | Output |
|-------|---------|-------|--------|
| **insights-extractor** | Extracts product insights from interview transcripts with rigorous provenance tracking, and proposes updates to persona files | Interview transcript(s) | Individual analyses + synthesis document |
| **opportunity-interviewer** | Conducts a structured interview to explore and document a product idea | Conversation with the PM | `opportunity.md` |
| **assumption-identifier** | Analyses a document to surface hidden risks and untested assumptions, then maps them by importance and evidence | Any product idea document | `assumptions.md` |
| **validation-suggester** | Recommends targeted experiments to test the highest-risk assumptions | An assumptions document | `validation-plan.md` |

Each skill can also be used independently — the assumption-identifier can analyse any document, not just interviewer output. The insights-extractor can feed directly into the assumption-identifier or into the opportunity-interviewer for deeper exploration.

#### Output Convention

Each opportunity gets its own folder under `outputs/opportunities/`:

```
outputs/opportunities/mobile-billing-app/
  opportunity.md        ← from opportunity-interviewer
  assumptions.md        ← from assumption-identifier
  validation-plan.md    ← from validation-suggester
```

Interview insights are stored separately under `outputs/insights/`:

```
outputs/insights/2026-02-billing-interviews/
  p01-analysis.md       ← individual transcript analysis
  p02-analysis.md       ← individual transcript analysis
  synthesis.md          ← cross-transcript synthesis
```

Files link to each other via YAML frontmatter (`source_document:`, `assumptions_document:`, `source_transcripts:`).

### Competitive Intelligence

Two complementary skills for competitive research and ongoing monitoring:

```
research-competitors → monitor-competitors (scheduled)
```

| Skill | Purpose | Input | Output |
| --- | --- | --- | --- |
| **research-competitors** | Profiles and strategically assesses a single competitor | Competitor name (or discovery) | `{company_dir}/competitors/<name>/summary.md` |
| **monitor-competitors** | Scans competitors for changes and alerts the team via Slack | Runs autonomously on a schedule | Updated competitor files + Slack posts |

- **research-competitors** is interactive — it works with the user to identify, research, and assess a competitor
- **monitor-competitors** is autonomous — it runs without user interaction, typically on a weekly schedule
- Both skills reference the same competitor profile template and output to the `{company_dir}/competitors/` directory
- Monitor uses Google Alerts RSS feeds (`feed_url` in frontmatter) as its primary signal source
- Slack posting (via Slack MCP) and Confluence sync are optional but recommended for the monitoring skill

### Industry Intelligence

Two complementary skills for industry research and ongoing monitoring, mirroring the competitive intelligence pattern:

```
research-industry-sources → monitor-industry (scheduled)
```

| Skill | Purpose | Input | Output |
| --- | --- | --- | --- |
| **research-industry-sources** | Discovers and curates industry sources organised around strategic topics | Conversation with the PM | `{company_dir}/industry/landscape.md` |
| **monitor-industry** | Scans industry sources for developments and alerts the team via Slack | Runs autonomously on a schedule | `{company_dir}/industry/digests/{date}.md` + Slack posts |

- **research-industry-sources** is interactive — it helps the PM identify strategic topics and curate high-value sources for each
- **monitor-industry** is autonomous — it scans sources, classifies findings by urgency, and posts strategic implications to Slack
- Sources are organised around **strategic topics** derived from company strategy and roadmap, not a flat list
- Uses the same urgency tier system (Act Now / Discuss / FYI) as competitor monitoring for consistency
- Explicit deduplication against competitor monitoring — industry-level developments belong here, competitor-specific ones don't
- Designed to run on the same schedule as competitor monitoring (weekly or fortnightly)

## Skill Structure

Each skill is a directory containing a `SKILL.md` file and supporting references:

```
skills/assumption-identifier/
├── SKILL.md                           # Main instructions and workflow
└── references/
    ├── assumptions-template.md        # Output template
    └── assumption-map-guide.md        # Reference documentation
```

- **SKILL.md** — The main prompt: role definition, workflow steps, principles, and guidance. Has YAML frontmatter with `name` and `description`.
- **references/** — Templates, technique libraries, and guides that the skill references during execution.

## Setting Up Skills in AI Coding Tools

### Claude Code

Claude Code discovers skills automatically from `.claude/skills/`. You have two options:

**Option A: Move skills to `.claude/skills/` (recommended for Claude Code users)**

Copy or symlink the skill directories into the Claude Code skills location:

```bash
# Symlink all skills
ln -s ../../skills/opportunity-interviewer .claude/skills/opportunity-interviewer
ln -s ../../skills/assumption-identifier .claude/skills/assumption-identifier
ln -s ../../skills/validation-suggester .claude/skills/validation-suggester
```

Once in `.claude/skills/`, skills are automatically available as slash commands:
- `/opportunity-interviewer` — start an opportunity interview
- `/assumption-identifier path/to/document.md` — analyse a document for risks
- `/validation-suggester path/to/assumptions.md` — get validation recommendations

Claude Code also auto-invokes skills when it recognises a relevant request from the skill's `description` field.

**Option B: Create wrapper commands in `.claude/commands/`**

If you prefer to keep skills in `skills/` without symlinks, create thin wrapper files in `.claude/commands/` that reference the full skill:

```yaml
# .claude/commands/assumption-identifier.md
---
description: Analyse a document to identify risks and untested assumptions
argument-hint: [document-path]
allowed-tools: Read, Edit, Glob, Write
---

Read and follow the complete skill instructions in skills/assumption-identifier/SKILL.md

The document to analyse is: $ARGUMENTS
```

### Amazon Q Developer CLI

Amazon Q Developer CLI supports custom prompts via the `/dev` command and context files. To use these skills:

1. When starting a task, reference the skill file directly:
   ```
   /dev Read skills/assumption-identifier/SKILL.md and follow those instructions to analyse product/my-feature.md
   ```

2. Alternatively, add a `.qdeveloper/context.md` file that points to the skills directory so the assistant is aware of available workflows.

### Other AI Coding Assistants

These skills work with any AI coding tool that can read files and follow structured prompts. The general approach:

1. Point the assistant to the relevant `SKILL.md` file
2. Ask it to read and follow the workflow
3. The skill's references are linked via relative paths and will be read as needed

## Creating New Skills

To add a new skill:

1. Create a directory: `skills/your-skill-name/`
2. Write `SKILL.md` with YAML frontmatter:
   ```yaml
   ---
   name: your-skill-name
   description: >
     One or two sentences describing what the skill does and when to use it.
   compatibility: Designed for Claude Code (or similar products)
   metadata:
     author: meerkat
     version: "1.0"
   ---
   ```
3. Define a clear workflow with numbered steps
4. Add templates and references in a `references/` subdirectory
5. Wire it up to your AI coding tool using the instructions above
