# Kairo AI Playbook 🦁

The operational knowledge base for Kairo AI's automated growth engine.

## Overview

This repo contains detailed instructions, workflows, and SOPs for:
- **X/Twitter Engagement** - Automated posting and commenting
- **LinkedIn Engagement** - Professional content and networking  
- **Lead Generation** - Finding and qualifying prospects
- **Contract Scanning** - Security analysis pipeline
- **Content Research** - Perplexity-powered insights
- **Notion Integration** - Central data management

## Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                     KAIRO GROWTH ENGINE                      │
├─────────────────────────────────────────────────────────────┤
│                                                              │
│  ┌──────────┐    ┌──────────────┐    ┌──────────────────┐  │
│  │  NOTION  │◄──►│  CRON JOBS   │◄──►│   PERPLEXITY     │  │
│  │ (Context)│    │  (Executor)  │    │   (Research)     │  │
│  └──────────┘    └──────────────┘    └──────────────────┘  │
│       │                 │                     │             │
│       ▼                 ▼                     ▼             │
│  ┌──────────────────────────────────────────────────────┐  │
│  │                    OUTPUTS                            │  │
│  │  • X Posts/Comments    • LinkedIn Posts               │  │
│  │  • Lead Outreach       • Contract Reports             │  │
│  │  • Research Insights   • Daily Intel                  │  │
│  └──────────────────────────────────────────────────────┘  │
│                                                              │
└─────────────────────────────────────────────────────────────┘
```

## Quick Start

### Check System Status
```bash
# Notion database stats
python3 ~/.config/kairo/notion_helper.py stats

# Recent activity context
python3 ~/.config/kairo/notion_helper.py context activity

# Test Perplexity
python3 ~/.config/kairo/perplexity_research.py "latest DeFi hacks"
```

### Core Workflow Pattern
Every automated task follows:
1. **Context** - Query Notion for existing data
2. **Research** - Get fresh intel from Perplexity
3. **Execute** - Create content/take action
4. **Log** - Store results back to Notion

## Directory Structure

```
kairo-playbook/
├── README.md                 # This file
├── workflows/                # Step-by-step SOPs
│   ├── x-engagement.md       # X/Twitter automation
│   ├── linkedin-engagement.md
│   └── lead-generation.md
├── tools/                    # Tool documentation
│   ├── notion-helper.md      # Notion API helper
│   └── perplexity.md         # Research API
├── integrations/             # External service configs
│   ├── api-keys.md           # All API credentials
│   └── notion.md             # Database schemas
├── skills/                   # Reusable skill guides
│   ├── notion-database.md    # Database operations
│   ├── perplexity-research.md # Research queries
│   ├── x-automation.md       # X/Twitter posting
│   ├── lead-enrichment.md    # Apollo + research
│   ├── contract-scanning.md  # Security analysis
│   └── email-outreach.md     # Himalaya emails
├── templates/                # Reusable templates
│   ├── outreach-emails.md
│   └── x-posts.md
└── examples/                 # Real examples
    └── (to be added)
```

## Key Links

- **Kairo Website**: https://kairoaisec.com
- **X/Twitter**: @kairo_security
- **LinkedIn**: Kairo AI Security

## Cron Schedule

| Time | Job | Output |
|------|-----|--------|
| 7:00 AM | Crypto Trends Newsletter | Notion Intel |
| 7:30 AM | Investor Digest | Notion Intel |
| 8:00 AM | Morning Post Research | Notion Research |
| 9:00 AM | High-Intent Leads | Notion Leads |
| 9:00 AM | LinkedIn Engagement | LinkedIn |
| 9:30 AM | Contract Scan Pipeline | Notion Contracts |
| 1:00 PM | Daily Contract Targets | Notion Contracts |
| 1:00 PM | LinkedIn Engagement | LinkedIn |
| 5:00 PM | LinkedIn Engagement | LinkedIn |
| 8:00 PM | Evening Post Research | Notion Research |
| Every 30m | X Engagement | X + Notion Activity |

---

*Last updated: 2026-02-12*
