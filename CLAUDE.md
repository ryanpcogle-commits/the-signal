# The Signal — Project Context

## What This Is
A fully automated daily AI newsletter called **The Signal** that researches AI news and publishes to GitHub Pages every morning.

## Live URLs
- **Website:** https://ryanpcogle-commits.github.io/the-signal/
- **GitHub repo:** https://github.com/ryanpcogle-commits/the-signal
- **Manage schedule:** https://claude.ai/code/scheduled

## File Conventions
- Issues: `ai-newsletter-YYYY-MM-DD.html`
- Archive index: `index.html`
- Issue numbering: started at 12, increment by 1 each run

## Newsletter Design
- **Name:** The Signal
- **Tagline:** "What actually matters in AI — curated, not clickbait."
- **Style:** Newspaper editorial — Georgia serif, cream background `#f0ede8`, red accent `#d4380d`
- **Sections:** Lead story → 3-stat numbers bar → 5-7 story cards → pull quote → "Patterns Worth Watching" dark box → footer
- **Category tag colors:** Models `#e8f4fd`, Infrastructure `#f6ffed`, Policy `#fff7e6`, Hardware `#f9f0ff`, Business `#fff1f0`, Robotics `#e6fffb`
- Reference `ai-newsletter-2026-03-30.html` for the exact HTML/CSS structure

## Daily Agent Instructions
1. Get today's date (`date +"%Y-%m-%d"`)
2. Read `index.html` to find the highest issue number, add 1
3. Run 4 web searches for today's AI news in parallel
4. Write `ai-newsletter-YYYY-MM-DD.html` — same design, fresh content
5. Update `index.html` — new issue at top with `issue-latest` badge, remove badge from previous top item
6. Commit and push as The Signal Bot (`action@github.com`)

## Git Identity (for agent runs)
```
git config user.email "action@github.com"
git config user.name "The Signal Bot"
```

## GitHub Setup
- Username: ryanpcogle-commits
- Branch: master
- GitHub Pages: enabled on master root `/`

## Planned: Instagram Pipeline (not yet built)
Extend the agent to also auto-post Instagram carousels daily.

**Requirements still needed:**
1. New Instagram account (Creator or Business)
2. Facebook Developer App with Instagram Graph API permissions
3. Long-lived Instagram access token
4. Bannerbear account + carousel slide template + API key

**When ready, agent extension flow:**
```
→ pick top 5-6 stories from the day's research
→ call Bannerbear API with story text → get back image URLs (hosted on GitHub Pages)
→ Instagram Graph API: upload each image as a container
→ create carousel container
→ publish with caption + hashtags
```
