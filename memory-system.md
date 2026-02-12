# Kairo Memory System

## Overview
All memory and tracking is centralized in **Notion**. No local files.

## Databases

| Database | Purpose | Helper Command |
|----------|---------|----------------|
| 🎯 Outreach | Leads, contacts, partnerships | `lead <name> <company> ...` |
| 📰 Daily Intel | News, trends, research findings | `intel <type> <title> <summary>` |
| 📚 Content Research | Ideas, hooks, brainstorms | `research <type> <title> <notes>` |
| 📊 Content Activity | Posts, comments, engagement | `activity <type> <platform> <content>` |
| 🔍 Contract Targets | Smart contracts to scan/contact | `contract <name> <addr> ...` |
| 🐙 GitHub | Repos to PR/contribute | `repo <name> <url> <stars> <desc>` |

## Read Commands

```bash
# Query entries
python3 ~/.config/kairo/notion_helper.py query <database> [limit] [status]

# Search by name
python3 ~/.config/kairo/notion_helper.py search <database> <term>

# Get counts
python3 ~/.config/kairo/notion_helper.py stats

# Get context for a task
python3 ~/.config/kairo/notion_helper.py context <database>
```

## Workflow Pattern

1. **Context (Notion)**: Check existing data before any task
2. **Research (Perplexity)**: Get fresh real-time intel
3. **Execute**: Post/comment/scan/outreach
4. **Log (Notion)**: Store results for future context

## Instructions Source

GitHub repo: `supratikpan07-png/kairo-playbook`

Local clone: `~/.config/kairo/kairo-playbook/`

All workflows, templates, and tool docs live there.
