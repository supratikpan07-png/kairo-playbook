# Skill: Perplexity Research

## Description
Use Perplexity AI for real-time web research. Get current data, news, and facts that go beyond training data cutoffs.

## Prerequisites
- Perplexity API key configured
- `~/.config/kairo/perplexity_research.py` installed
- Config at `~/.config/kairo/perplexity.json`

## Basic Usage

```bash
python3 ~/.config/kairo/perplexity_research.py "your query here"
```

## Query Strategies

### For DeFi Security News
```bash
python3 ~/.config/kairo/perplexity_research.py "latest DeFi hacks smart contract exploits this week February 2026"
```

**What you get:**
- Recent hack amounts ($)
- Protocol names
- Vulnerability types
- Timeline of events

### For Protocol Launches
```bash
python3 ~/.config/kairo/perplexity_research.py "DeFi protocol launches token sales mainnet this week February 2026"
```

**What you get:**
- Protocols launching soon
- Launch dates
- Funding raised
- Team info

### For Funding News
```bash
python3 ~/.config/kairo/perplexity_research.py "crypto blockchain funding rounds seed series A this week"
```

**What you get:**
- Companies that raised
- Round sizes
- Investors
- What they're building

### For Market Context
```bash
python3 ~/.config/kairo/perplexity_research.py "ETH SOL BTC price DeFi TVL market trends today"
```

**What you get:**
- Current prices
- TVL changes
- Market sentiment
- Major movements

### For Bug Bounty News
```bash
python3 ~/.config/kairo/perplexity_research.py "bug bounty payouts smart contract security Immunefi this week"
```

**What you get:**
- Recent payouts
- Vulnerability types
- Programs with high bounties

### For Competitor Intel
```bash
python3 ~/.config/kairo/perplexity_research.py "smart contract audit firms news partnerships this week"
```

**What you get:**
- Audit firm announcements
- New partnerships
- Market movements

## Query Best Practices

### Include Timeframes
```bash
# Good - specific time
"DeFi hacks February 2026"
"crypto news this week"
"funding rounds last 7 days"

# Bad - too vague
"DeFi hacks"
"crypto news"
```

### Be Specific
```bash
# Good - specific topic
"reentrancy vulnerabilities DeFi exploits 2026"
"Solana smart contract security issues"

# Bad - too broad
"blockchain security"
"crypto problems"
```

### Ask for Data
```bash
# Good - asks for numbers
"DeFi hacks with dollar amounts this month"
"protocols launching with funding raised"

# Bad - vague
"DeFi hacks"
"new protocols"
```

## Integration Patterns

### Research → Notion
```bash
# Save research directly to Notion
python3 ~/.config/kairo/perplexity_research.py "query" | python3 ~/.config/kairo/notion_helper.py raw research "Title" "Trend"
```

### Research → Content
```bash
# Get research, use for content
RESEARCH=$(python3 ~/.config/kairo/perplexity_research.py "latest DeFi hacks")
echo "$RESEARCH"
# Now use the data in your post/comment
```

### Multi-Query Research
```bash
# Combine multiple queries for comprehensive research
python3 ~/.config/kairo/perplexity_research.py "DeFi hacks this week"
python3 ~/.config/kairo/perplexity_research.py "smart contract vulnerabilities found"
python3 ~/.config/kairo/perplexity_research.py "bug bounty payouts Immunefi"
```

## Use Cases by Task

### X/Twitter Posting
1. Research current security news
2. Extract shocking stats ($ amounts)
3. Find trending topics
4. Create posts with real data

```bash
python3 ~/.config/kairo/perplexity_research.py "crypto security news trending X Twitter today"
```

### Lead Generation
1. Find protocols launching
2. Identify funding announcements
3. Discover security needs

```bash
python3 ~/.config/kairo/perplexity_research.py "DeFi protocols launching mainnet needing security audit"
```

### Content Ideas
1. Research trending topics
2. Find contrarian angles
3. Get data for hot takes

```bash
python3 ~/.config/kairo/perplexity_research.py "controversial opinions smart contract security audits"
```

## Output Format

Perplexity returns structured responses with:
- **Facts** - Specific data points
- **Numbers** - $ amounts, percentages
- **Dates** - When things happened
- **Sources** - [1], [2] citations
- **Tables** - When appropriate

## Example Output

```
Query: "DeFi hacks January 2026"

Response:
January 2026 saw $86M stolen across 16 DeFi hacks[1]:

| Protocol | Amount | Vulnerability |
|----------|--------|---------------|
| Truebit | $26.4M | Mint/burn bug |
| Step Finance | $27M | Treasury compromise |
| SwapNet | $13.4M | Smart contract |

Key findings:
- 58% of hacked protocols had passed audits[2]
- Average hack: $5.4M
- Most common: smart contract bugs, oracle manipulation

[1] PeckShield report
[2] CertiK analysis
```

## Error Handling

### Timeout
- Try simpler query
- Check internet connection

### Empty response
- Query too vague
- Try different wording

### Rate limiting
- Space out queries
- Don't spam requests

## Advanced Usage

### Custom system prompt
Edit `~/.config/kairo/perplexity_research.py` to change the context:

```python
context = "You are a crypto security researcher. Provide concise, factual information with specific examples, numbers, and recent events."
```

### Different models
Edit `~/.config/kairo/perplexity.json`:
```json
{
  "model": "sonar-large"  // More detailed
}
```

## Cost Considerations

- Perplexity API has usage-based pricing
- Each query costs tokens
- Cache results when possible
- Avoid redundant queries
