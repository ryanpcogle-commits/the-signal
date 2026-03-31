# The Signal — Full Project Memory

## What This Is
A fully automated daily AI newsletter called **The Signal**, built on March 30, 2026.
It researches AI news every morning using web searches, generates a styled HTML newsletter,
and publishes it to GitHub Pages automatically — no manual work required.

---

## Live URLs
- **Website (main bookmark):** https://ryanpcogle-commits.github.io/the-signal/
- **GitHub repo:** https://github.com/ryanpcogle-commits/the-signal
- **Manage schedule:** https://claude.ai/code/scheduled

---

## How It Was Built (Session Summary)

1. Ran `/last30days AI news and announcements` to research the first issue
2. Built `ai-newsletter.html` as a styled newspaper-format newsletter ("The Signal")
3. Renamed to dated format `ai-newsletter-2026-03-30.html` (Issue No. 12)
4. Created `ai-newsletter-index.html` as an archive page linking to all issues
5. Created `c:\Users\ryanp\Projects\the-signal\` folder, copied files in
6. Initialised git, created GitHub repo `ryanpcogle-commits/the-signal` via `gh` CLI
7. Enabled GitHub Pages on master branch root via GitHub API
8. Set up a Claude Code remote scheduled agent at claude.ai/code/scheduled
9. Agent fired immediately and published Issue 13 (March 31, 2026) confirming it works

---

## File Conventions
- Issues: `ai-newsletter-YYYY-MM-DD.html`
- Archive index: `index.html`
- Issue numbering: started at 12, increment by 1 each run
- Reference `ai-newsletter-2026-03-30.html` for the canonical HTML/CSS structure

---

## Newsletter Design System
- **Name:** The Signal
- **Tagline:** "What actually matters in AI — curated, not clickbait."
- **Background:** `#f0ede8` (warm cream)
- **Accent:** `#d4380d` (red)
- **Body font:** Georgia serif
- **UI font:** Helvetica Neue / Arial
- **Max width:** 680px centered

### Sections (in order)
1. Header — masthead, issue bar (black background)
2. Lead story — label, h2 headline, italic deck, 3 paragraphs
3. Numbers bar — 3-cell grid with big red stats
4. Section heading — "This Month/Week/Today in AI"
5. Story cards (5-7) — tag chip, h3, paragraph
6. Pull quote — bordered blockquote with cite
7. Patterns Worth Watching — dark (#1a1a1a) box, numbered list
8. Footer — name + date, sources list

### Category tag colors
| Tag | Background | Text |
|-----|-----------|------|
| Models | `#e8f4fd` | `#1a6b9a` |
| Infrastructure | `#f6ffed` | `#2d7738` |
| Policy | `#fff7e6` | `#b35a00` |
| Hardware | `#f9f0ff` | `#6b21a8` |
| Business | `#fff1f0` | `#cf1322` |
| Robotics | `#e6fffb` | `#006d75` |

---

## Daily Automation

### Scheduled agent
- **Platform:** Claude Code remote agent (Anthropic cloud)
- **Schedule:** `0 14 * * *` — 7am Phoenix time (America/Phoenix, UTC-7) daily
- **Environment:** claude-code-default (id: env_01MuFtQ9CnBzDZqkTnehk9KA)
- **Model:** claude-sonnet-4-6
- **Repo cloned:** https://github.com/ryanpcogle-commits/the-signal

### What the agent does each run
1. Gets today's date via `date +"%Y-%m-%d"`
2. Reads `index.html` to find the highest issue number, adds 1
3. Runs 4 parallel web searches for today's AI news
4. Writes `ai-newsletter-YYYY-MM-DD.html` — same CSS, fresh content
5. Updates `index.html` — new issue at top with `issue-latest` badge, removes badge from previous top item
6. Commits and pushes as The Signal Bot
7. GitHub Pages rebuilds automatically (~1 min)

### Git identity used by agent
```bash
git config user.email "action@github.com"
git config user.name "The Signal Bot"
```

---

## GitHub / Local Setup
- **GitHub username:** ryanpcogle-commits
- **Branch:** master
- **GitHub Pages:** enabled on master root `/`
- **Local clone:** `c:\Users\ryanp\Projects\the-signal\`
- **Local git identity:** ryanpcogle-commits / ryanpcogle-commits@users.noreply.github.com
- Git 2.53.0 and GitHub CLI 2.89.0 installed on local machine
- Python is NOT installed locally (Microsoft Store stub only — don't rely on it)
- OS: Windows 11 Home, shell: bash (Git Bash / VS Code terminal)

---

## Planned: Instagram Pipeline

### The idea
Extend the daily agent to also auto-post an Instagram carousel each morning using
the same AI news content. Zero manual work — fully automated alongside the newsletter.

### Why it makes sense
- AI news carousels perform well on Instagram
- Content is already being researched daily
- Images can be hosted on GitHub Pages (already set up)
- Instagram Graph API is free for posting

### Full pipeline when built
```
Agent runs at 7am
  → researches AI news (already done)
  → generates newsletter HTML (already done)
  → picks top 5-6 stories for carousel slides
  → calls Bannerbear API with story text → returns styled PNG images
  → calls Instagram Graph API:
      - uploads each image as a media container
      - creates carousel container from all containers
      - publishes carousel with caption + hashtags
  → commits newsletter HTML to GitHub (already done)
```

### What still needs to be set up
1. **Instagram account** — create new account, switch to Creator or Business (free)
2. **Facebook Developer App** — create app at developers.facebook.com, add Instagram Graph API product, get permissions: `instagram_basic`, `instagram_content_publish`, `pages_read_engagement`
3. **Long-lived access token** — exchange short-lived token, valid 60 days (needs refresh automation)
4. **Bannerbear account** — design a carousel slide template once (cover slide + story slide), get API key. Free tier available at bannerbear.com. Alternative: Canva API.
5. **Extend the agent prompt** — add Steps 7-10 to the existing scheduled agent prompt at claude.ai/code/scheduled

### Instagram API posting flow (technical reference)
```
# Step 1: Upload each image as a container
POST https://graph.instagram.com/v18.0/{ig-user-id}/media
  → image_url, is_carousel_item=true, access_token
  → returns: container_id

# Step 2: Create carousel container
POST https://graph.instagram.com/v18.0/{ig-user-id}/media
  → media_type=CAROUSEL, children=[id1,id2,...], caption, access_token
  → returns: carousel_container_id

# Step 3: Publish
POST https://graph.instagram.com/v18.0/{ig-user-id}/media_publish
  → creation_id=carousel_container_id, access_token
```

### Carousel slide design (suggested)
- **Slide 1 (Cover):** "The Signal" logo, date, "Today in AI" headline
- **Slides 2-6:** One story per slide — category tag, headline, 2-line summary
- **Slide 7 (CTA):** "Follow for daily AI news · Link in bio for full newsletter"
- Size: 1080x1080px or 1080x1350px
- Use same brand colours: `#f0ede8` background, `#d4380d` accent, dark headlines

---

## Issue History
| Issue | Date | Notes |
|-------|------|-------|
| 12 | March 30, 2026 | First issue — built manually in this session |
| 13 | March 31, 2026 | First automated issue — agent fired same day |
