# Notion Helper Tool

## Location
```
~/.config/kairo/notion_helper.py
```

## Overview
Unified CLI for reading from and writing to Kairo's Notion databases.

## Databases

| Name | ID | Purpose |
|------|-----|---------|
| intel | 304f3f84-aa35-8142-9905-db1fd2a733d9 | Daily Intel (Crypto Trends, Investor Digest) |
| leads | 304f3f84-aa35-8193-9587-d5cb644a7fe5 | Outreach (people/leads with emails) |
| contracts | 304f3f84-aa35-8171-ad8c-f31dc26fccb2 | Contract Targets (smart contracts to scan) |
| repos | 304f3f84-aa35-8176-8870-d90de8d8d2d3 | GitHub Repos (for PR outreach) |
| research | 304f3f84-aa35-81a1-8d7a-daeb2705b1e7 | Content Research (brainstorm, hooks, ideas) |
| activity | 304f3f84-aa35-81b7-b480-ec4adf3ebb0b | Content Activity (posts/comments tracking) |

## Write Commands

### intel
Add entry to Daily Intel database.
```bash
python3 ~/.config/kairo/notion_helper.py intel "Crypto Trends" "Title Here" "Summary text"
```

### research
Add to Content Research (brainstorm/trends).
```bash
python3 ~/.config/kairo/notion_helper.py research "Hook" "Title" "Notes" "https://source.url" "X"
```
Types: Trend, Hook, Meme Idea, Thread Idea, News, Competitor Intel, Stats/Data
Platforms: X, LinkedIn, Both

### activity
Log content activity (posts/comments).
```bash
python3 ~/.config/kairo/notion_helper.py activity "Post" "X" "Your post content" "https://x.com/link" ""
python3 ~/.config/kairo/notion_helper.py activity "Comment" "X" "Your comment" "https://x.com/link" "@target_account"
```
Types: Post, Comment, Repost, Thread
Platforms: X, LinkedIn

### lead
Add to Outreach database.
```bash
python3 ~/.config/kairo/notion_helper.py lead "Name" "Company" "Role" "Notes" "High"
```
Priority: High, Medium, Low

### contract
Add to Contract Targets.
```bash
python3 ~/.config/kairo/notion_helper.py contract "Name" "0xAddress" "Ethereum" "0xDeployer" "75" "500" "Notes"
```
Arguments: name, address, chain, deployer, score, LOC, notes
Chains: Ethereum, Base, Arbitrum, Solana
LOC auto-sets Contract Size (Small <500, Medium 500-2000, Large 2000+)

### repo
Add to GitHub Repos.
```bash
python3 ~/.config/kairo/notion_helper.py repo "owner/name" "https://github.com/..." "1234" "Description"
```

### raw
Pipe any content to any database (preserves full content in page body).
```bash
echo "Full content here..." | python3 ~/.config/kairo/notion_helper.py raw intel "Title" "Type"
echo "Full content here..." | python3 ~/.config/kairo/notion_helper.py raw leads "Name" "High-Intent"
```

## Read Commands

### query
Query database entries.
```bash
python3 ~/.config/kairo/notion_helper.py query leads 10
python3 ~/.config/kairo/notion_helper.py query contracts 20 "To Scan"
```
Arguments: database, limit (optional), status filter (optional)

### search
Search database by name/content.
```bash
python3 ~/.config/kairo/notion_helper.py search leads "Aave"
python3 ~/.config/kairo/notion_helper.py search contracts "APU"
```

### stats
Show database counts.
```bash
python3 ~/.config/kairo/notion_helper.py stats
```

Output:
```
📊 NOTION DATABASE STATS
==================================================
intel        | 1+  | Test Full Content
leads        | 1+  | Arjun Raj Jain
contracts    | 1+  | NativeNames
repos        | 1+  | morph-l2/morph
research     | 1+  | Test - .4B stolen in 2025
activity     | 1+  | M bounty to ily2...
```

### context
Get context summary for a database (use before tasks!).
```bash
python3 ~/.config/kairo/notion_helper.py context activity
python3 ~/.config/kairo/notion_helper.py context leads
python3 ~/.config/kairo/notion_helper.py context contracts
```

Shows grouped/organized view of recent entries. Essential for avoiding duplicates.

## Common Patterns

### Before creating content
```bash
# Check what we've posted recently
python3 ~/.config/kairo/notion_helper.py context activity
```

### Before adding leads
```bash
# Check if lead already exists
python3 ~/.config/kairo/notion_helper.py search leads "Company Name"
```

### Log full research to Notion
```bash
# Pipe Perplexity output directly to Notion
python3 ~/.config/kairo/perplexity_research.py "query" | python3 ~/.config/kairo/notion_helper.py raw research "Research Title" "Trend"
```

## API Details

- **Token**: Stored in script (ntn_654901683732...)
- **Version**: 2022-06-28
- **Rate Limits**: ~3 requests/second safe

## Troubleshooting

### "Unknown database"
Check database name is one of: intel, research, activity, leads, contracts, repos

### Content truncated
Use `raw` command to pipe full content - it goes into page body without truncation.

### Missing properties
Different databases have different schemas. Check the database in Notion UI for available fields.
