# Skill: Email Outreach

## Description
Send cold emails using Himalaya CLI. Personalized outreach to leads, audit firms, and protocol teams.

## Prerequisites
- Himalaya configured with Gmail
- Account: supratikpan07@gmail.com
- Config: `~/Library/Application Support/himalaya/config.toml`

## Sending Email

### Basic Send
```bash
himalaya message send << 'EOF'
From: supratikpan07@gmail.com
To: recipient@company.com
Subject: Your subject line

Email body here.

Signature
EOF
```

### With Variables
```bash
cat << EOF | himalaya message send
From: supratikpan07@gmail.com
To: ${EMAIL}
Subject: Quick question about ${COMPANY}'s security

${NAME},

[Personalized content]

Supratik
Kairo AI | kairoaisec.com
EOF
```

## Email Templates

### Protocol Launch (Highest Priority)

**Subject:** Security before [Launch Date]?

```
[Name],

Saw [Protocol] is launching [timeline]. Congrats on the momentum.

At your scale, smart contracts will be prime targets from day one. Traditional audits are great, but they're point-in-time snapshots - they won't catch what happens after deployment.

We built Kairo specifically for protocols at your stage - AI-powered scanning that catches vulnerabilities audits miss, integrated into your CI/CD so nothing ships without review.

Worth 15 minutes before launch to see what we'd flag?

Best,
Supratik
Kairo AI | kairoaisec.com
```

### Post-Funding

**Subject:** Now that [Company] raised, security should be next

```
[Name],

Congrats on the [round size] [round type]. That's a major milestone.

Now that you have runway, security should be top of the list. We've seen too many protocols lose months of work (and user funds) because security was an afterthought.

Kairo gives you continuous AI-powered monitoring - not just a one-time audit that's outdated by your next deployment. We integrate directly into your workflow.

Would love to show you what we're seeing in similar protocols. 15 min call?

Supratik
Kairo AI | kairoaisec.com
```

### Audit Firm Partnership

**Subject:** Partnership idea: [Firm] + Kairo AI

```
[Name],

[Firm] has a strong reputation for [specific thing]. The demand for quality audits is only growing.

We built Kairo as an AI-powered scanning layer that complements manual audits - catches the obvious stuff automatically, freeing your auditors to focus on business logic and complex interactions.

Some audit firms are white-labeling our tech to increase throughput without expanding headcount. Could be interesting for [Firm].

Open to a quick call to explore?

Supratik
Kairo AI | kairoaisec.com
```

### Post-Hack (Similar Protocol)

**Subject:** After [Hacked Protocol] - your security posture

```
[Name],

Saw what happened with [Hacked Protocol]. [Brief description].

[Your Protocol] has similar [architecture/features]. The same attack vector could apply.

Kairo's continuous monitoring would have caught [vulnerability type] before deployment. We're helping protocols like yours implement detection for exactly these patterns.

Worth a quick call to review exposure? No pitch, just useful intel.

Supratik
Kairo AI | kairoaisec.com
```

### Follow-Up (24h)

**Subject:** Re: [Original Subject]

```
[Name],

Following up - I know [busy time / launch prep].

Quick version: Kairo = AI security monitoring that catches what audits miss. 15 min to show you what we'd flag in [Protocol]?

Supratik
```

### Follow-Up (48h - Different Channel)

Try Twitter DM, LinkedIn, or Telegram instead:

```
Hey [Name], shot you an email about [Protocol]'s security - might have hit spam.

Quick question: how are you handling continuous monitoring post-audit?
```

## Workflow Integration

### From Notion Lead → Email
```bash
# 1. Get lead from Notion
python3 ~/.config/kairo/notion_helper.py search leads "Company"

# 2. Get email draft from Notion (if stored)
# or compose new email

# 3. Send
himalaya message send << 'EOF'
[email content]
EOF

# 4. Update Notion status
# Mark as "Contacted" in Notion UI
```

### Batch Sending
```bash
# Send to multiple leads (be careful with rate limits)
for lead in "${leads[@]}"; do
    # Compose personalized email
    # Send via himalaya
    # Log to Notion
    sleep 60  # Don't spam
done
```

## Best Practices

### Personalization
- Always include their name
- Reference specific company/protocol
- Mention the signal (why reaching out now)
- Keep it short (3-4 paragraphs max)

### Timing
- Avoid weekends
- Best: Tuesday-Thursday, 9-11 AM recipient's timezone
- Follow up: 24h, then 48h

### Subject Lines
- Keep under 50 characters
- Be specific, not clickbait
- Include company name or topic

### Don'ts
- Don't send identical emails
- Don't follow up more than 2x
- Don't be pushy
- Don't forget to log in Notion

## Tracking

### In Notion Leads
Update status after each action:
- **New** → Lead identified
- **Researched** → Enriched with Apollo
- **Contacted** → Email sent
- **Replied** → Got response
- **Meeting** → Call scheduled
- **Won/Lost** → Outcome

### Track Metrics
- Emails sent per day
- Response rate
- Time to response
- Conversion to meetings

## Reading Responses

### Check Inbox
```bash
himalaya envelope list
```

### Read Specific Email
```bash
himalaya message read <id>
```

### Reply to Email
```bash
himalaya reply <id>
```

## Error Handling

### Send Failed
- Check internet connection
- Verify recipient email
- Check spam/sending limits

### No Response
- Follow up after 24h
- Try different channel after 48h
- Mark as cold after 3 attempts

### Bounce Back
- Email invalid
- Remove from list
- Try to find alternative contact
