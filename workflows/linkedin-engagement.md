# LinkedIn Engagement Workflow

## Overview
Build Kairo's professional presence on LinkedIn through thought leadership content and strategic engagement.

## Schedule
- **Frequency**: 3x daily (9 AM, 1 PM, 5 PM EST)
- **Targets per session**: 5 comments + 1 post
- **Daily totals**: 15 comments + 3 posts

## Account Details
- **Profile**: Kairo Employee (Sales and Marketing @ Kairo AI)
- **Company Page**: Kairo (1,772 followers)
- **Login**: Google OAuth (supratikpan07@gmail.com)

## Step-by-Step Process

### Step 1: Context Check (Notion)
```bash
python3 ~/.config/kairo/notion_helper.py search activity LinkedIn
python3 ~/.config/kairo/notion_helper.py context research
```

Check:
- Recent LinkedIn posts (avoid duplicates)
- Unused research/hooks from Content Research db
- Topics already covered

### Step 2: Research (Perplexity)
```bash
python3 ~/.config/kairo/perplexity_research.py "Web3 enterprise blockchain security smart contract audit news this week"
```

LinkedIn audience prefers:
- Enterprise/institutional angles
- Professional tone
- Data-backed insights
- Industry trends

### Step 3: Open LinkedIn Feed
```bash
browser action=open profile=openclaw targetUrl="https://linkedin.com/feed"
browser action=snapshot profile=openclaw
```

### Step 4: Find Posts to Comment On

**Target topics:**
- Smart contract security
- Web3/DeFi news
- Crypto hacks & vulnerabilities
- Audit announcements
- Developer tooling
- Enterprise blockchain adoption

**Target profiles:**
- Security researchers
- Protocol founders
- VCs in crypto
- Enterprise blockchain leaders
- Audit firm partners

### Step 5: Comment Strategy

**LinkedIn tone (differs from X):**
- More professional
- Longer form acceptable
- Add credentials/experience angle
- Reference industry trends
- Still be insightful, not generic

**Example good comment:**
```
Great breakdown. One thing often overlooked: the timing of audits matters as much as the quality.

We're seeing protocols rush to audit right before launch, then ship 10 updates in the first month post-deployment - none of which get reviewed.

The industry needs to shift from "audit before launch" to "continuous security monitoring." The threat landscape evolves daily; our defenses should too.
```

### Step 6: Create Original Post

**LinkedIn post formula:**
1. Hook (question or bold statement)
2. Context with data
3. Insight or opinion
4. Call to discussion

**Example:**
```
The $86M stolen from DeFi in January wasn't a failure of code review.

58% of exploited protocols had passed audits. The audits worked - they found the bugs that existed at that moment.

But smart contracts aren't static. Every upgrade, every new integration, every parameter change creates new attack surface.

What the industry needs:
→ Continuous monitoring, not one-time audits
→ Automated detection of vulnerability patterns
→ Real-time alerts when code changes
→ Incident response plans before the hack

Security isn't a checkbox. It's infrastructure.

What's your take - are traditional audits still enough? 👇

#SmartContractSecurity #DeFi #Web3 #Blockchain #Cybersecurity
```

### Step 7: Log to Notion

```bash
# Log comments
python3 ~/.config/kairo/notion_helper.py activity "Comment" "LinkedIn" "Comment text" "https://linkedin.com/..." "@Person Name"

# Log posts
python3 ~/.config/kairo/notion_helper.py activity "Post" "LinkedIn" "Post text" "https://linkedin.com/..." ""
```

## Browser Navigation

### Access feed
```bash
browser action=open profile=openclaw targetUrl="https://linkedin.com/feed"
```

### Start a post
1. Find "Start a post" button (ref varies)
2. Click to open composer
3. Type content
4. Click Post

### Comment on a post
1. Scroll to find relevant post
2. Click "Comment" button
3. Type comment
4. Press Enter or click Post

### Search for topics
```bash
browser action=navigate profile=openclaw targetUrl="https://linkedin.com/search/results/content/?keywords=smart%20contract%20security"
```

## Content Guidelines

### DO:
- Use professional language
- Back claims with data
- Ask questions to drive engagement
- Tag relevant people/companies when appropriate
- Use 3-5 hashtags

### DON'T:
- Be overly casual
- Hard sell Kairo
- Post memes (save for X)
- Engage in controversial non-security topics
- Spam connections

## Tracking

**Monitor in Notion:**
- Post impressions (visible on LinkedIn)
- Comment engagement
- Profile views
- Company page visitors

**LinkedIn Analytics:**
- Profile: /in/kairo-employee-50a1503b0/
- Company: /company/110457254/admin/analytics/
