# Lead Generation Workflow

## Overview
Identify and qualify high-intent prospects for Kairo's smart contract security platform.

## Schedule
- **High-Intent Leads**: Daily at 9 AM EST
- **Contract Scan Pipeline**: Daily at 9:30 AM EST
- **Daily Contract Targets**: Daily at 1 PM EST

## Lead Sources

### 1. Protocol Launches (Highest Intent)
Protocols about to launch or just launched need security urgently.

**Perplexity query:**
```bash
python3 ~/.config/kairo/perplexity_research.py "DeFi protocol launches token sales this week February 2026"
```

**Signals:**
- Announced mainnet launch date
- Token sale upcoming
- Testnet going live
- New chain deployment

### 2. Funding Announcements
Projects that just raised have budget for security.

**Perplexity query:**
```bash
python3 ~/.config/kairo/perplexity_research.py "crypto blockchain funding rounds seed series A this week"
```

**Signals:**
- Seed round closed
- Series A/B announced
- Treasury allocation for security
- Grant received

### 3. Feature Announcements
New features = new code = new risk.

**Perplexity query:**
```bash
python3 ~/.config/kairo/perplexity_research.py "DeFi protocol new features upgrades announcements this week"
```

**Signals:**
- V2/V3 upgrade announced
- New product launch
- Cross-chain expansion
- Major integration

### 4. Post-Hack Recovery
Projects that got hacked are now security-conscious.

**Perplexity query:**
```bash
python3 ~/.config/kairo/perplexity_research.py "DeFi hacks exploits recovery February 2026"
```

**Signals:**
- Announced security improvements
- Hiring security roles
- Seeking audit partners

## Lead Qualification

### Confidence Scoring (0-100)

**90-100%: Hot Lead**
- Launching in <2 weeks
- Just raised >$5M
- Publicly seeking security partners
- DM or email accessible

**70-89%: Warm Lead**
- Launching in 1-3 months
- Raised funding recently
- Active development
- Contact info findable

**50-69%: Nurture Lead**
- Early stage
- No announced timeline
- May not have budget yet
- Worth tracking

**<50%: Cold/Skip**
- No clear launch timeline
- No funding
- Minimal social presence
- Ghost team

## Lead Data Collection

For each lead, gather:

| Field | Example |
|-------|---------|
| Name | Andre Cronje |
| Company | Flying Tulip |
| Role | Founder |
| Email | (if available) |
| Twitter | @AndreCronjeTech |
| Signal | Public sale Feb 16, $290M raised |
| Confidence | 92% |
| Outreach Message | Personalized draft |

## Notion Integration

### Check existing leads first
```bash
python3 ~/.config/kairo/notion_helper.py context leads
python3 ~/.config/kairo/notion_helper.py search leads "Company Name"
```

### Add new lead
```bash
python3 ~/.config/kairo/notion_helper.py lead "Name" "Company" "Role" "Notes about signal" "High"
```

### Add with full details (piped)
```bash
echo "LEAD: Andre Cronje
Company: Flying Tulip
Role: Founder
Signal: Public sale Feb 16, $290M raised, DeFi super app
Confidence: 92%

OUTREACH:
Andre, saw Flying Tulip is launching the public sale on Feb 16 - congrats on the momentum.

At that scale ($290M raised), your smart contracts will be prime targets from day one. 

We built Kairo specifically for protocols at your stage - AI-powered scanning that catches vulns audits miss, integrated into your CI/CD so nothing ships without review.

Worth 15 min before the sale to see what we'd flag?

Supratik
Kairo AI" | python3 ~/.config/kairo/notion_helper.py raw leads "Andre Cronje - $(date +%Y-%m-%d)" "High-Intent"
```

## Outreach Templates

### For Protocol Launches
```
[Name], saw [Protocol] is launching [timeline]. 

At that scale, your contracts will be targets from day one. We built Kairo specifically for protocols at your stage - AI scanning that catches what audits miss.

Worth 15 min before launch to see what we'd flag?
```

### For Post-Funding
```
[Name], congrats on the [round]. 

Now that you have runway, security should be top of the list. We've helped protocols like [similar company] secure $[amount] in TVL with continuous AI monitoring.

Open to a quick call?
```

### For Post-Hack (Competitor)
```
[Name], saw what happened with [hack]. 

The good news: there's a path forward that doesn't rely on point-in-time audits. Kairo's continuous monitoring would have caught [specific vuln type] before deployment.

Happy to show you how - no pitch, just useful intel.
```

## Apollo Enrichment

For leads with only name + company, use Apollo to get email:

```python
# Apollo API (requires both name and org)
import requests

response = requests.post(
    "https://api.apollo.io/api/v1/people/match",
    headers={"x-api-key": "YOUR_KEY"},
    json={
        "first_name": "Andre",
        "last_name": "Cronje", 
        "organization_name": "Flying Tulip"
    }
)
email = response.json()["person"]["email"]
```

**Note:** Apollo requires name + organization. Org-only searches don't work.

## Pipeline Management

### Status Flow
```
New → Researched → Contacted → Replied → Meeting → Won/Lost
```

### Follow-up Rules
- No reply in 24h → Follow up
- No reply in 48h → Mark cold, try different channel
- Replied interested → Book meeting ASAP
- Replied not interested → Note reason, nurture list
