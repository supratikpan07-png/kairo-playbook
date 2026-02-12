# Skill: Lead Enrichment

## Description
Find and enrich leads using Perplexity research and Apollo API. Convert names/companies into actionable contact data.

## Prerequisites
- Perplexity API configured
- Apollo API key: `C9ADUAQzr6liLtihcI9DGQ`
- Notion helper for storage

## Lead Discovery

### Using Perplexity

#### Find Launching Protocols
```bash
python3 ~/.config/kairo/perplexity_research.py "DeFi protocols launching mainnet token sale this week February 2026"
```

#### Find Funded Companies
```bash
python3 ~/.config/kairo/perplexity_research.py "crypto blockchain funding rounds seed series A this week"
```

#### Find Security-Conscious Teams
```bash
python3 ~/.config/kairo/perplexity_research.py "smart contract audit announcements DeFi security partnerships"
```

### From Research → Lead Data

Extract from Perplexity results:
- **Name:** Person's name (founder, CTO, etc.)
- **Company:** Protocol/project name
- **Role:** Their position
- **Signal:** What triggered the lead (launch, funding, etc.)
- **Timeline:** When do they need security

## Apollo Enrichment

### Important: Apollo Requirements
Apollo's `/people/match` endpoint requires BOTH:
- First name + Last name
- Organization name

**Org-only searches return empty results.**

### API Call
```python
import requests

response = requests.post(
    "https://api.apollo.io/api/v1/people/match",
    headers={"x-api-key": "C9ADUAQzr6liLtihcI9DGQ"},
    json={
        "first_name": "Andre",
        "last_name": "Cronje",
        "organization_name": "Flying Tulip"
    }
)

data = response.json()
email = data["person"]["email"]
linkedin = data["person"]["linkedin_url"]
title = data["person"]["title"]
```

### What Apollo Returns
```json
{
  "person": {
    "email": "andre@flyingtulip.com",
    "linkedin_url": "https://linkedin.com/in/...",
    "title": "Founder",
    "organization": {
      "name": "Flying Tulip",
      "website_url": "https://flyingtulip.com"
    }
  }
}
```

## Enrichment Workflow

### Step 1: Research (Perplexity)
```bash
python3 ~/.config/kairo/perplexity_research.py "DeFi protocols launching with founders names"
```

### Step 2: Extract Leads
From research, identify:
- Person name
- Company name
- Why they're a lead (signal)

### Step 3: Check Notion (Avoid Duplicates)
```bash
python3 ~/.config/kairo/notion_helper.py search leads "Company Name"
```

### Step 4: Apollo Enrichment
If lead is new, call Apollo to get email.

### Step 5: Save to Notion
```bash
python3 ~/.config/kairo/notion_helper.py lead "Andre Cronje" "Flying Tulip" "Founder" "Launching Feb 16, $290M raised, email: andre@flyingtulip.com" "High"
```

Or with full details:
```bash
echo "LEAD: Andre Cronje
Company: Flying Tulip
Role: Founder
Email: andre@flyingtulip.com
LinkedIn: https://linkedin.com/in/...
Signal: Public sale Feb 16, $290M raised
Confidence: 92%

OUTREACH:
Andre, saw Flying Tulip is launching the public sale on Feb 16..." | python3 ~/.config/kairo/notion_helper.py raw leads "Andre Cronje - 2026-02-12" "High-Intent"
```

## Lead Scoring

### 90-100% (Hot)
- Launching in <2 weeks
- Just raised >$5M
- Actively seeking security
- Email/contact available

### 70-89% (Warm)
- Launching in 1-3 months
- Recent funding
- Active development
- Contact findable

### 50-69% (Nurture)
- Early stage
- No timeline
- May lack budget
- Worth tracking

### <50% (Skip)
- No clear timeline
- No funding signals
- Ghost team

## Alternative Enrichment Methods

### If Apollo Fails

#### LinkedIn Search
```bash
browser action=open profile=openclaw targetUrl="https://linkedin.com/search/results/people/?keywords=Andre%20Cronje%20Flying%20Tulip"
```

#### Google Search
```bash
python3 ~/.config/kairo/perplexity_research.py "Andre Cronje Flying Tulip email contact"
```

#### Twitter DM
If they have open DMs, reach out there.

#### Discord/Telegram
Many protocols have community channels with team contacts.

## Bulk Processing

### Process Multiple Leads
```python
leads = [
    {"first": "Andre", "last": "Cronje", "org": "Flying Tulip"},
    {"first": "Sam", "last": "Sun", "org": "Paradigm"},
    # ...
]

for lead in leads:
    # Check if exists in Notion
    # Call Apollo
    # Save to Notion
    time.sleep(1)  # Rate limit
```

## Data Quality

### Validation
- Verify email format
- Check LinkedIn URL works
- Confirm company match

### Updates
- Re-enrich stale leads
- Track status changes
- Update contact info

## Pipeline Management

### Status Flow
```
New → Researched → Contacted → Replied → Meeting → Won/Lost
```

### After Enrichment
Update Notion with:
- Email (if found)
- LinkedIn URL
- Confidence score
- Ready status

## Troubleshooting

### Apollo Returns Empty
- Check you have both name AND org
- Verify spelling
- Try variations (Inc, LLC, etc.)

### Wrong Person Found
- Add more context (title, location)
- Verify against LinkedIn

### Rate Limits
- Space out Apollo calls
- Cache results
- Don't re-enrich same person
