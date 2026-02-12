# Perplexity Research Tool

## Location
```
~/.config/kairo/perplexity_research.py
```

## Overview
Real-time web search using Perplexity AI for current data that goes beyond training cutoffs.

## Configuration
```
~/.config/kairo/perplexity.json
```

Contains:
- API key
- Base URL (https://api.perplexity.ai)
- Model (sonar)

## Usage

```bash
python3 ~/.config/kairo/perplexity_research.py "your query here"
```

## Example Queries

### DeFi Security News
```bash
python3 ~/.config/kairo/perplexity_research.py "latest DeFi hacks smart contract exploits this week"
```

### Protocol Launches
```bash
python3 ~/.config/kairo/perplexity_research.py "DeFi protocol launches token sales February 2026"
```

### Funding News
```bash
python3 ~/.config/kairo/perplexity_research.py "crypto blockchain funding rounds seed series A this week"
```

### Audit News
```bash
python3 ~/.config/kairo/perplexity_research.py "smart contract audit announcements blockchain security news"
```

### Market Context
```bash
python3 ~/.config/kairo/perplexity_research.py "ETH SOL BTC price DeFi TVL market trends"
```

### Stablecoin News
```bash
python3 ~/.config/kairo/perplexity_research.py "stablecoin news USDT USDC DAI market cap changes"
```

## Output Format

Perplexity returns structured responses with:
- Specific facts and figures
- Recent dates and events
- Source citations [1], [2], etc.
- Tables when appropriate

## Best Practices

### Be Specific with Dates
```bash
# Good - includes timeframe
"DeFi hacks February 2026"

# Bad - too vague
"DeFi hacks"
```

### Include Context Keywords
```bash
# Good - specific topic
"smart contract vulnerabilities reentrancy flash loan attacks"

# Bad - too broad
"crypto security"
```

### Ask for What You Need
```bash
# Good - asks for actionable data
"DeFi protocols launching this week with dates and funding amounts"

# Bad - vague
"upcoming DeFi launches"
```

## Integration with Notion

### Pipe research directly to Notion
```bash
python3 ~/.config/kairo/perplexity_research.py "query" | python3 ~/.config/kairo/notion_helper.py raw research "Title" "Trend"
```

### Save research before using
```bash
# Get research
RESEARCH=$(python3 ~/.config/kairo/perplexity_research.py "latest DeFi hacks")

# Use in content creation
echo "$RESEARCH"

# Save to Notion
echo "$RESEARCH" | python3 ~/.config/kairo/notion_helper.py raw intel "DeFi Hacks - $(date +%Y-%m-%d)" "Security Alert"
```

## Use Cases

### X/LinkedIn Content
1. Research current events
2. Extract specific numbers/facts
3. Create posts with real data
4. Comments backed by recent examples

### Lead Generation
1. Find protocols launching soon
2. Identify funding announcements
3. Discover companies seeking security
4. Track post-hack recovery efforts

### Daily Newsletters
1. Stablecoin market movements
2. Security incidents
3. Bug bounty payouts
4. Market trends

## Rate Limits

- API allows reasonable usage
- Space out queries if doing many
- Cache results when possible

## Error Handling

If query fails:
- Check API key is valid
- Verify internet connection
- Try simpler query
- Check Perplexity service status

## Model Options

Current: `sonar` (default, good balance of speed/quality)

Other options:
- `sonar-small` - faster, less detailed
- `sonar-medium` - balanced
- `sonar-large` - most detailed, slower
