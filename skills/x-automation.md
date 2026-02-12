# Skill: X/Twitter Automation

## Description
Automate posting and commenting on X/Twitter as @kairo_security using browser automation.

## Prerequisites
- Browser profile `openclaw` with X session
- Logged into @kairo_security account
- Notion helper for logging

## Account Details
- **Handle:** @kairo_security
- **Profile:** Browser profile `openclaw`
- **Purpose:** Kairo AI brand presence in crypto security

## Browser Commands

### Open X Home
```bash
browser action=open profile=openclaw targetUrl="https://x.com/home"
```

### Take Snapshot (See Feed)
```bash
browser action=snapshot profile=openclaw targetId=<id>
```

### Navigate to Search
```bash
browser action=navigate profile=openclaw targetId=<id> targetUrl="https://x.com/search?q=smart%20contract%20security&f=live"
```

### Navigate to Profile
```bash
browser action=navigate profile=openclaw targetId=<id> targetUrl="https://x.com/<username>"
```

## Posting Workflow

### Step 1: Open Compose
From home feed, find and click the compose/post button.

### Step 2: Type Content
```bash
browser action=act profile=openclaw targetId=<id> request='{"kind": "type", "ref": "<textbox_ref>", "text": "Your post content here"}'
```

### Step 3: Post
Click the Post button.

### Step 4: Get URL
After posting, navigate to your profile to get the post URL.

### Step 5: Log to Notion
```bash
python3 ~/.config/kairo/notion_helper.py activity "Post" "X" "Your post content" "https://x.com/kairo_security/status/..." ""
```

## Commenting Workflow

### Step 1: Find Target Post
Navigate to the post you want to comment on.

### Step 2: Click Reply
Find the reply/comment button and click it.

### Step 3: Type Comment
```bash
browser action=act profile=openclaw targetId=<id> request='{"kind": "type", "ref": "<reply_textbox>", "text": "Your comment"}'
```

### Step 4: Submit Reply
Click the Reply button.

### Step 5: Log to Notion
```bash
python3 ~/.config/kairo/notion_helper.py activity "Comment" "X" "Your comment" "https://x.com/..." "@target_account"
```

## Content Strategy

### Post Types

#### Hot Take
```
[Contrarian statement]

[2-3 supporting points]

[Security insight]

#SmartContractSecurity #DeFi
```

#### Data Shock
```
$[amount] stolen in [timeframe].

That's:
- $X per day
- X hacks total
- X% had audits

[Insight]
```

#### Thread Starter
```
🧵 [Topic]

Here's what everyone's missing:
```

### Comment Strategies

#### Add an Angle
```
This, but also [additional insight they missed].

[Specific example or data point].
```

#### Challenge Respectfully
```
Interesting take. Counter-point: [your angle].

[Evidence/example].
```

#### Drop Data
```
The numbers back this up:
- [Stat 1]
- [Stat 2]

[Source if relevant]
```

## Target Accounts

### Security Researchers
- @immunefi
- @pashov
- @samczsun
- @code4rena
- @OpenZeppelin
- @spearbitdao

### DeFi/Crypto News
- @RektHQ
- @WuBlockchain
- @theaboredape

### Founders/VCs
- @AndreCronjeTech
- @staborswap
- @chrisdior777

## Best Practices

### DO:
- Research before posting (use Perplexity)
- Check Notion context (avoid repeats)
- Add specific data/examples
- Engage meaningfully
- Log everything

### DON'T:
- Generic "great post!" comments
- Spam same content
- Hard sell Kairo
- Comment without adding value
- Forget to log to Notion

## Scheduling

- Every 30 minutes (0,30 * * * *)
- 10 comments + 1 post per session
- Skip dead hours (2-6 AM)

## Troubleshooting

### Session expired
- Re-login via browser
- Check cookies are valid

### Rate limited
- Slow down actions
- Space out posts/comments

### Content not posting
- Check character limit (280)
- Verify button clicks working

## Integration with Research

### Before Posting
```bash
# 1. Check what we've posted
python3 ~/.config/kairo/notion_helper.py context activity

# 2. Get fresh research
python3 ~/.config/kairo/perplexity_research.py "latest DeFi security news"

# 3. Create informed content
# 4. Post
# 5. Log to Notion
```

## Metrics to Track

- Post impressions (views)
- Comment likes
- Follower growth
- Profile visits
- Engagement rate

Update Notion Activity entries with metrics periodically.
