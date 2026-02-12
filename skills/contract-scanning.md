# Skill: Smart Contract Scanning

## Description
Discover, analyze, and track smart contracts for security outreach. Use Etherscan/Blockscout for source code, Kairo for scanning.

## Prerequisites
- Browser for Etherscan access
- Blockscout API (free, no key)
- Notion helper for tracking
- Access to kairoaisec.com for scanning

## Contract Discovery

### Etherscan Verified Contracts
Navigate to recently verified contracts:
```bash
browser action=open profile=openclaw targetUrl="https://etherscan.io/contractsVerified"
```

### Filter Criteria
Look for:
- Recent deployments (last 24-48h)
- Token contracts
- DeFi protocols
- High transaction count
- Verified source code

### Multi-Chain Sources
- **Ethereum:** etherscan.io/contractsVerified
- **Base:** basescan.org/contractsVerified  
- **Arbitrum:** arbiscan.io/contractsVerified
- **Solana:** solscan.io (different format)

## Getting Source Code

### Blockscout API (Recommended - Free)
```bash
curl -s "https://eth.blockscout.com/api/v2/smart-contracts/0x<address>" | jq '.source_code'
```

**Chains:**
- Ethereum: `eth.blockscout.com`
- Base: `base.blockscout.com`
- Arbitrum: `arbitrum.blockscout.com`

### Response Includes:
- `source_code` - Main contract code
- `additional_sources` - Imported files
- `name` - Contract name
- `compiler_version` - Solidity version

### Counting Lines of Code
```python
import urllib.request
import json

def get_loc(address, chain="Ethereum"):
    apis = {
        "Ethereum": "https://eth.blockscout.com/api/v2/smart-contracts/",
        "Base": "https://base.blockscout.com/api/v2/smart-contracts/",
    }
    
    url = f"{apis[chain]}{address}"
    with urllib.request.urlopen(url) as resp:
        data = json.loads(resp.read())
        source = data.get("source_code", "")
        return source.count("\n") + 1
```

## Scanning with Kairo

### Via Browser
1. Navigate to kairoaisec.com
2. Login (Google OAuth)
3. Paste contract code
4. Run audit score
5. Review findings

### Scan Results Include:
- **Score:** 0-100 (lower = more vulnerable)
- **Critical:** Severe vulnerabilities
- **High:** Significant risks
- **Medium:** Moderate concerns
- **Low:** Minor issues

## Adding to Notion

### Basic Entry
```bash
python3 ~/.config/kairo/notion_helper.py contract "APU Token" "0x40e72e905ad6B666CD831125473fe9F1378b3d5f" "Ethereum" "0x123..." "25" "337" "2 critical, 3 high findings"
```

### With Full Report (Piped)
```bash
echo "CONTRACT: APU Token
Address: 0x40e72e905ad6B666CD831125473fe9F1378b3d5f
Chain: Ethereum
Deployer: 0x123...
Score: 25/100

CRITICAL (2):
1. Reentrancy in withdraw()
2. Unchecked external call

HIGH (3):
1. Missing access control
2. Integer overflow
3. Unsafe delegatecall

DEPLOYER CONTACT:
Twitter: @apudeployer
Telegram: t.me/apu_erc

OUTREACH:
[Draft message]" | python3 ~/.config/kairo/notion_helper.py raw contracts "APU Token - 2026-02-12" "Scanned"
```

## Contract Size Classification

| Size | LOC | Priority |
|------|-----|----------|
| Small | <500 | Quick wins, easy to scan |
| Medium | 500-2000 | Standard complexity |
| Large | 2000+ | Complex, more findings |

### Size Strategy
- Start with **Small** contracts for quick outreach
- **Medium** for balanced effort/reward
- **Large** for high-value targets

## Finding Deployer Contacts

### From Contract
Check contract for:
- Comments with links
- Website URLs
- Social media handles

### From Etherscan
- Check deployer address
- Look for ENS name
- Check transaction history

### From Token Info
If it's a token:
- Check token website
- Look up on CoinGecko/CMC
- Find social links

### Blockscan Chat
Direct message deployers via Blockscan:
1. Navigate to Blockscan chat
2. Connect wallet
3. Send message to deployer address

## Scanning Pipeline

### Daily Workflow
1. **Discover:** Check Etherscan for new contracts
2. **Filter:** Select promising targets
3. **Scan:** Run through Kairo
4. **Analyze:** Review findings
5. **Contact:** Reach out to vulnerable contracts
6. **Track:** Log everything in Notion

### Automation (Cron)
```
9:30 AM - Contract Scan Pipeline
1:00 PM - Daily Contract Targets
```

## Outreach Templates

### For Vulnerable Contract
```
Hey [deployer],

Ran your contract through our scanner - found some issues you should know about:

- [Critical finding]
- [High finding]

These are exploitable. Happy to walk you through fixes.

[Kairo signature]
```

### For Blockscan Chat
```
Your contract [address] has vulnerabilities our scanner flagged:

🔴 [Critical issue]
🟠 [High issue]

Worth 10 min to review? Could save you from an exploit.
```

## Tracking in Notion

### Status Flow
```
To Scan → Scanned → Contacted → Replied → Meeting → Won/Lost
```

### Update After Each Step
```bash
# After scanning
python3 ~/.config/kairo/notion_helper.py contract "Name" "0x..." "Ethereum" "0x..." "25" "500" "Scanned, 2 critical"

# After contacting - update via Notion UI or API
```

## Quality Metrics

### Track:
- Contracts scanned per day
- Average score
- Response rate
- Conversion to meetings

### Success Indicators:
- Low scores = more outreach opportunities
- Small contracts = faster wins
- Active deployers = higher response
