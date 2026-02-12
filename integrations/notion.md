# Notion Integration

## Workspace
Kairo teamspace on Notion (Business trial - 163 days remaining as of Feb 2026)

## API Token
```
YOUR_NOTION_TOKEN_HERE
```
Stored in `~/.config/kairo/notion_helper.py`

## Database Schemas

### 📰 Daily Intel
ID: `304f3f84-aa35-8142-9905-db1fd2a733d9`

| Property | Type | Options |
|----------|------|---------|
| Name | title | - |
| Type | select | Crypto Trends, Investor Digest, Security Alert |
| Date | date | - |
| Status | select | New, Reviewed |
| Summary | rich_text | - |

### 🎯 Outreach (Leads)
ID: `304f3f84-aa35-8193-9587-d5cb644a7fe5`

| Property | Type | Options |
|----------|------|---------|
| Name | title | - |
| Company | rich_text | - |
| Role | rich_text | - |
| Email | email | - |
| LinkedIn | url | - |
| Status | select | New, Researched, Contacted, Replied, Meeting, Won, Lost |
| Priority | select | High, Medium, Low |
| Notes | rich_text | - |
| Email Draft | rich_text | - |

### 🔍 Contract Targets
ID: `304f3f84-aa35-8171-ad8c-f31dc26fccb2`

| Property | Type | Options |
|----------|------|---------|
| Name | title | - |
| Contract Address | rich_text | - |
| Chain | select | Ethereum, Base, Arbitrum, Solana |
| Status | select | To Scan, Scanned, Contacted, Replied |
| Source | select | Etherscan, Blockscan, Manual |
| Deployer | rich_text | - |
| Score | rich_text | - |
| Lines of Code | number | - |
| Contract Size | select | Small (<500 LOC), Medium (500-2000 LOC), Large (2000+ LOC) |
| Notes | rich_text | - |
| Date Added | date | - |

### 🐙 GitHub Repos
ID: `304f3f84-aa35-8176-8870-d90de8d8d2d3`

| Property | Type | Options |
|----------|------|---------|
| Name | title | - |
| URL | url | - |
| Stars | number | - |
| Lines of Code | number | - |
| Repo Size | select | Small (<500 LOC), Medium (500-2000 LOC), Large (2000+ LOC) |
| Description | rich_text | - |
| Status | select | New, PR Sent, Merged, Declined |
| Owner Contact | rich_text | - |
| PR Type | select | - |

### 📚 Content Research
ID: `304f3f84-aa35-81a1-8d7a-daeb2705b1e7`

| Property | Type | Options |
|----------|------|---------|
| Name | title | - |
| Type | select | Trend, Hook, Meme Idea, Thread Idea, News, Competitor Intel, Stats/Data |
| Platform | select | X, LinkedIn, Both |
| Source URL | url | - |
| Notes | rich_text | - |
| Status | select | New, Researched, Ready, Used |
| Priority | select | High, Medium, Low |
| Date | date | - |

### 📊 Content Activity
ID: `304f3f84-aa35-81b7-b480-ec4adf3ebb0b`

| Property | Type | Options |
|----------|------|---------|
| Content | title | - |
| Type | select | Post, Comment, Repost, Thread |
| Platform | select | X, LinkedIn |
| URL | url | - |
| Target Account | rich_text | - |
| Views | number | - |
| Likes | number | - |
| Replies | number | - |
| Status | select | Posted, Scheduled, Draft |
| Time | date | - |

## Current Counts (as of 2026-02-12)

| Database | Count |
|----------|-------|
| Daily Intel | 2+ |
| Outreach | 208+ |
| Contract Targets | 38+ |
| GitHub Repos | 50 |
| Content Research | 2+ |
| Content Activity | 20+ |

## Common Operations

### Query with filters
```python
import urllib.request
import json

TOKEN = "YOUR_NOTION_TOKEN_HERE"
DB_ID = "304f3f84-aa35-8193-9587-d5cb644a7fe5"

url = f"https://api.notion.com/v1/databases/{DB_ID}/query"
headers = {
    "Authorization": f"Bearer {TOKEN}",
    "Notion-Version": "2022-06-28",
    "Content-Type": "application/json"
}
data = {
    "filter": {
        "property": "Status",
        "select": {"equals": "New"}
    },
    "page_size": 100
}
```

### Update a page
```python
url = f"https://api.notion.com/v1/pages/{PAGE_ID}"
data = {
    "properties": {
        "Status": {"select": {"name": "Contacted"}}
    }
}
# Use PATCH method
```

### Create a page
```python
url = "https://api.notion.com/v1/pages"
data = {
    "parent": {"database_id": DB_ID},
    "properties": {
        "Name": {"title": [{"text": {"content": "Title"}}]},
        "Status": {"select": {"name": "New"}}
    }
}
# Use POST method
```

## Rate Limits
- ~3 requests/second is safe
- Notion will return 429 if exceeded
- Add 0.3s sleep between bulk operations
