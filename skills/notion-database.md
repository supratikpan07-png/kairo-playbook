# Skill: Notion Database Management

## Description
Manage Kairo's Notion databases for leads, contracts, content, and intel. Read, write, query, and analyze data.

## Prerequisites
- Notion API token configured
- `~/.config/kairo/notion_helper.py` installed

## Commands

### Writing Data

#### Add a lead
```bash
python3 ~/.config/kairo/notion_helper.py lead "Name" "Company" "Role" "Notes" "Priority"
```
- Priority: High, Medium, Low
- Example:
```bash
python3 ~/.config/kairo/notion_helper.py lead "Andre Cronje" "Flying Tulip" "Founder" "Launching Feb 16, $290M raised" "High"
```

#### Add a contract target
```bash
python3 ~/.config/kairo/notion_helper.py contract "Name" "0xAddress" "Chain" "0xDeployer" "Score" "LOC" "Notes"
```
- Chains: Ethereum, Base, Arbitrum, Solana
- LOC auto-sets size (Small <500, Medium 500-2000, Large 2000+)
- Example:
```bash
python3 ~/.config/kairo/notion_helper.py contract "APU Token" "0x40e72e905ad6B666CD831125473fe9F1378b3d5f" "Ethereum" "0x123..." "85" "337" "Potential vulnerabilities in transfer logic"
```

#### Log content activity
```bash
python3 ~/.config/kairo/notion_helper.py activity "Type" "Platform" "Content" "URL" "Target"
```
- Types: Post, Comment, Repost, Thread
- Platforms: X, LinkedIn
- Example:
```bash
python3 ~/.config/kairo/notion_helper.py activity "Comment" "X" "Great analysis, but audits miss post-deployment changes" "https://x.com/..." "@samczsun"
```

#### Add research/ideas
```bash
python3 ~/.config/kairo/notion_helper.py research "Type" "Title" "Notes" "URL" "Platform"
```
- Types: Trend, Hook, Meme Idea, Thread Idea, News, Competitor Intel, Stats/Data
- Example:
```bash
python3 ~/.config/kairo/notion_helper.py research "Hook" "$86M stolen in January" "16 hacks, 58% had passed audits" "https://source.com" "X"
```

#### Add with full content (piped)
```bash
echo "Full content here..." | python3 ~/.config/kairo/notion_helper.py raw <database> "Title" "Type"
```
- Databases: intel, research, activity, leads, contracts, repos
- Example:
```bash
echo "LEAD: Andre Cronje
Company: Flying Tulip
Signal: Public sale Feb 16
Confidence: 92%

OUTREACH MESSAGE:
..." | python3 ~/.config/kairo/notion_helper.py raw leads "Andre Cronje - 2026-02-12" "High-Intent"
```

### Reading Data

#### Query recent entries
```bash
python3 ~/.config/kairo/notion_helper.py query <database> [limit] [status]
```
- Example:
```bash
python3 ~/.config/kairo/notion_helper.py query leads 10 "New"
python3 ~/.config/kairo/notion_helper.py query contracts 20 "To Scan"
```

#### Search by name
```bash
python3 ~/.config/kairo/notion_helper.py search <database> "term"
```
- Example:
```bash
python3 ~/.config/kairo/notion_helper.py search leads "Aave"
python3 ~/.config/kairo/notion_helper.py search contracts "Token"
```

#### Get database stats
```bash
python3 ~/.config/kairo/notion_helper.py stats
```

#### Get context summary (IMPORTANT - use before tasks!)
```bash
python3 ~/.config/kairo/notion_helper.py context <database>
```
- Shows grouped/organized view
- Use to avoid duplicates
- Example:
```bash
python3 ~/.config/kairo/notion_helper.py context activity  # See recent posts/comments
python3 ~/.config/kairo/notion_helper.py context leads     # See leads by status
```

## Workflow Patterns

### Before creating content
```bash
# Check what we've already posted
python3 ~/.config/kairo/notion_helper.py context activity
```

### Before adding leads
```bash
# Check if lead already exists
python3 ~/.config/kairo/notion_helper.py search leads "Company Name"
```

### After any action, log it
```bash
# Always log posts, comments, outreach
python3 ~/.config/kairo/notion_helper.py activity "Post" "X" "content" "url" ""
```

## Database Schemas

### Leads (🎯 Outreach)
| Field | Type | Values |
|-------|------|--------|
| Name | title | - |
| Company | text | - |
| Role | text | - |
| Email | email | - |
| Status | select | New, Researched, Contacted, Replied, Meeting, Won, Lost |
| Priority | select | High, Medium, Low |
| Notes | text | - |
| Email Draft | text | - |

### Contracts (🔍 Contract Targets)
| Field | Type | Values |
|-------|------|--------|
| Name | title | - |
| Contract Address | text | - |
| Chain | select | Ethereum, Base, Arbitrum, Solana |
| Status | select | To Scan, Scanned, Contacted, Replied |
| Deployer | text | - |
| Score | text | - |
| Lines of Code | number | - |
| Contract Size | select | Small, Medium, Large |

### Activity (📊 Content Activity)
| Field | Type | Values |
|-------|------|--------|
| Content | title | - |
| Type | select | Post, Comment, Repost, Thread |
| Platform | select | X, LinkedIn |
| URL | url | - |
| Target Account | text | - |
| Views/Likes/Replies | number | - |

## Error Handling

### "Unknown database"
- Check database name is valid: intel, research, activity, leads, contracts, repos

### Content truncated
- Use `raw` command to pipe full content

### Duplicate entries
- Always run `search` before adding new entries

## Best Practices

1. **Always check context first** - Avoid duplicates
2. **Log everything** - Future runs depend on history
3. **Use raw for long content** - Preserves formatting
4. **Update status** - Keep pipeline accurate
