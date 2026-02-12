# X/Twitter Engagement Workflow

## Overview
Automated engagement on X as @kairo_security to build brand presence and thought leadership in crypto security space.

## Schedule
- **Frequency**: Every 30 minutes (0,30 * * * *)
- **Timezone**: America/New_York (EST)
- **Targets per session**: 10 comments + 1 post

## Step-by-Step Process

### Step 1: Context Check (Notion)
Before creating any content, check what we've already posted to avoid repetition.

```bash
python3 ~/.config/kairo/notion_helper.py context activity
```

This returns:
- Recent posts (last 5-10)
- Recent comments with target accounts
- Topics we've already covered

**Use this to:**
- Avoid repeating the same hot takes
- Find new angles on similar topics
- Track which accounts we've engaged with

### Step 2: Research (Perplexity)
Get fresh, real-time intel to inform content.

```bash
python3 ~/.config/kairo/perplexity_research.py "latest DeFi hacks smart contract exploits crypto security news this week"
```

**Key data to extract:**
- Recent hack amounts ($ values)
- Protocol names and vulnerability types
- Trending security topics
- Bug bounty news
- New audit announcements

### Step 3: Find Posts to Comment On
Use browser to navigate X and find high-value posts.

```bash
# Open X in browser
browser action=open profile=openclaw targetUrl="https://x.com/home"

# Take snapshot to see feed
browser action=snapshot profile=openclaw
```

**Target post criteria:**
- Security researchers sharing findings
- DeFi/protocol announcements
- Hack post-mortems
- Crypto VCs discussing infrastructure
- Posts with 1K+ views on security topics

**Priority accounts:**
- @immunefi
- @pashov
- @samczsun
- @RektHQ
- @code4rena
- @OpenZeppelin
- @chrisdior777
- @spearbitdao

### Step 4: Comment Strategy
Comments should be the **smartest reply in the thread**.

**DO:**
- Add an angle they missed
- Drop specific data from Perplexity research
- Reference recent hacks with $ amounts
- Challenge their take respectfully (engagement bait)
- Connect to broader security implications
- Keep it short, punchy, quotable

**DON'T:**
- Generic "great post!" energy
- Obvious self-promotion
- Repeat points already made in thread
- Comment without adding value

**Example good comment:**
```
This, but also worth noting the audit passed with flying colors 3 months ago. 

Point-in-time snapshots miss what continuous monitoring catches. Step Finance's $27M loss wasn't a code bug - it was compromised OpSec the audit never touched.
```

### Step 5: Create Original Post
One high-impact post per session using research data.

**Post formula:**
1. Hook with shocking stat/fact
2. Security insight or hot take
3. Implicit Kairo angle (without being salesy)
4. Relevant hashtags

**Example:**
```
$86M stolen in January alone. 16 separate hacks.

The common thread? 58% of exploited protocols had "passed" audits.

Audits are compliance theater. Real security is:
- 24/7 monitoring
- Automated vulnerability detection
- Incident response plans

One-time audits ≠ ongoing security.

#SmartContractSecurity #DeFi #Web3
```

### Step 6: Log Everything to Notion
Every action must be logged for future context.

**Log comments:**
```bash
python3 ~/.config/kairo/notion_helper.py activity "Comment" "X" "Your comment text" "https://x.com/link" "@target_account"
```

**Log posts:**
```bash
python3 ~/.config/kairo/notion_helper.py activity "Post" "X" "Your post text" "https://x.com/link" ""
```

## Browser Automation Details

### Navigate to X
```bash
browser action=open profile=openclaw targetUrl="https://x.com/home"
```

### Search for topics
```bash
browser action=navigate profile=openclaw targetUrl="https://x.com/search?q=smart%20contract%20security&f=live"
```

### Post a tweet
1. Click compose button
2. Type content
3. Click post

### Reply to a tweet
1. Navigate to tweet
2. Click reply button
3. Type comment
4. Click reply

## Quality Metrics

Track these in Notion Activity database:
- Views (update manually or via scraping)
- Likes
- Replies
- Reposts

**Success indicators:**
- Comments getting likes/replies
- Posts getting engagement
- Follower growth
- Profile visits

## Troubleshooting

### Browser not loading X
- Check profile=openclaw is correct
- Verify cookies are valid
- May need to re-login

### Rate limiting
- Space out actions
- Don't post same content twice
- Vary comment styles

### Content feels repetitive
- Run `context activity` to see recent posts
- Check Notion for topics covered
- Use Perplexity for fresh angles
