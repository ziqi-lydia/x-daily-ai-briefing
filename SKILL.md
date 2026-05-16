# X Daily Briefing — Personalized AI-Powered X/Twitter Intelligence

## Overview
Generate a daily personalized X/Twitter briefing by scanning the platform for the past 12-24 hours. Tailored to the user's content pillars, product positioning, competitors, and growth goals.

This skill works for **any user** — founders, creators, marketers, or anyone building a presence on X. The agent collects user-specific context first, then executes a structured research and briefing workflow.

---

## Step 0: Collect User Profile (First Run Only)

On the first run, ask the user for the following. Store in a variable `userProfile` for reuse across sessions. If the user has provided this before, skip to Step 1.

```
userProfile = {
  handle: "",              // Their X handle, e.g. "@ZiqiLiu158430"
  name: "",                // Display name
  email: "",               // Email to send briefing to
  products: [],            // Their product/company X handles, e.g. ["@SimularAI", "@sai_borg"]
  contentPillars: [],      // Topics they post about, e.g. ["AI", "Startup", "GTM", "Workflow Automation"]
  postStyle: "",           // Their voice/tone, e.g. "Casual founder voice, technical but accessible"
  competitors: [],         // Competitor X handles to monitor
  industryKeywords: [],    // Keywords to search on X, e.g. ["computer use agent", "AI coding", "agentic"]
  builders: [],            // Thought leaders / builders to track
  bestFormats: []          // Post formats that work best for them
}
```

**If the user provides only partial info**, fill in reasonable defaults and confirm:
- `contentPillars`: Infer from their recent posts or stated interests
- `competitors`: Ask "Who are your main competitors on X?"
- `builders`: Default to a general AI/tech builder list (see Appendix A) and let user customize
- `bestFormats`: Default to the 5 universal high-performing formats (see Appendix B)
- `email`: Ask where to send the briefing

---

## Step 1: Scan Competitor & Industry Activity (Past 12-24h)

Open X in browser and check each account in `userProfile.competitors`:

For each competitor:
1. Visit their profile page
2. Capture posts from the last 12-24h
3. Note: content summary, engagement metrics (replies, reposts, likes, views), any product launches or announcements

Also check `userProfile.products` accounts for recent engagement metrics on their own posts.

**Output format per competitor:**
```
{ handle, date, content, engagement: { replies, reposts, likes, views }, notable: true/false }
```

---

## Step 2: Scan Trending Topics & Builder Activity

### 2a: Industry Keyword Search
For each keyword in `userProfile.industryKeywords`:
- Search X: `https://x.com/search?q={keyword}&src=typed_query&f=top`
- Capture top 3-5 posts with high engagement from the past 24h

### 2b: Builder/Thought Leader Scan
For top builders in `userProfile.builders` (prioritize 5-8 most active):
- Visit their profiles
- Capture notable posts from the past 24h
- Flag posts that align with user's content pillars

### 2c: X Trending Topics
- Check X's trending sidebar for topics related to user's industry
- Note any trending hashtags or conversations relevant to the user's niche

---

## Step 3: Identify Quote Repost Opportunities

From all collected posts, identify 2-3 best quote repost candidates. Criteria:
- ✅ Post already has decent engagement (ride the wave)
- ✅ Topic directly connects to user's product or content pillars
- ✅ Allows a genuine, non-forced perspective from the user
- ✅ Not a competitor's self-promotion post (unless commenting on industry trend)

For each opportunity, draft a quote repost that:
- Adds unique insight, not just "great post!"
- Connects to user's own experience or product (subtly, not salesy)
- Applies at least one algorithm tactic from Appendix C
- Specifies which tactic is applied and why

---

## Step 4: Generate Original Post Ideas

Based on trending topics and competitor activity, generate 2-3 original post ideas:

For each idea, provide:
- **Format**: Thread / Single post / Quote repost / Reply
- **Hook line**: First sentence that stops the scroll
- **Key message**: Core point in 1-2 sentences
- **Full draft** (optional but preferred)
- **Algorithm tactic applied**: Which of the 7 tactics and why
- **Product connection**: How it relates to user's product (if applicable — don't force it)

Mix of:
- At least 1 trending-topic response (time-sensitive)
- At least 1 evergreen insight or founder reflection
- At least 1 engagement play (question, hot take, or fill-in-blank)

---

## Step 5: Identify Comment/Reply Targets

Find 2-3 high-engagement posts where a thoughtful reply would maximize visibility:
- Posts from accounts with large followings (>10K followers)
- Posts with many replies (high-activity threads)
- Topics where the user has genuine expertise

For each, provide:
- Link to the post
- Suggested reply (2-3 sentences, conversational, adds value)
- Why this reply would perform (visibility, relevance, engagement potential)

---

## Step 6: Compile & Send Briefing Email

Compose a clean, scannable email and send to `userProfile.email`.

**Subject**: 🐦 Daily X Briefing — [Date]

**Email structure:**

```
🐦 Daily X Briefing — [Date]

Prepared for: [handle] ([name])
Content pillars: [pillars joined by " | "]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

🔥 TOP NEWS (Past 24h)
[3-5 most relevant developments with engagement stats]
[Each item: what happened → why it matters to YOU]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

📊 COMPETITOR WATCH
[Per competitor: what they posted, engagement, notable moves]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

🎯 QUOTE REPOST OPPORTUNITIES
[2-3 posts with full draft copy ready to use]
[Each with: original post summary → your draft → algorithm tactic applied]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

✍️ ORIGINAL POST IDEAS
[2-3 post concepts with hooks and drafts]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

💬 COMMENT/REPLY TARGETS
[2-3 high-visibility posts to reply to with suggested replies]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

📈 YOUR ACCOUNT PULSE
[Recent post performance notes + today's priority recommendations]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Priority Actions for Today:
→ 🔴 Do NOW: [most time-sensitive action]
→ 🟡 Do TODAY: [important but not urgent]
→ 🟢 Do TODAY: [evergreen opportunity]
```

**Formatting rules:**
- Use → arrows for action items, not bullets
- Include direct X links wherever possible
- Keep each section scannable — no walls of text
- Every item must have a "what to do" attached
- Use emoji section headers consistently

---

## Appendix A: Default Builder/Thought Leader List

If the user doesn't provide their own list, start with these and let them customize:

**AI/Tech Leaders:**
- @karpathy — Andrej Karpathy (AI education, ex-Tesla/OpenAI)
- @sama — Sam Altman (OpenAI CEO)
- @rauchg — Guillermo Rauch (Vercel CEO, AI-first dev tools)
- @amasad — Amjad Masad (Replit CEO, AI coding)
- @levie — Aaron Levie (Box CEO, enterprise AI)
- @emollick — Ethan Mollick (Wharton, AI adoption research)
- @garrytan — Garry Tan (YC President)

**AI Product & Engineering:**
- @alexalbert__ — Alex Albert (Anthropic, Claude product)
- @AmandaAskell — Amanda Askell (Anthropic, alignment)
- @kevinweil — Kevin Weil (OpenAI product)
- @joshwoodward — Josh Woodward (Google Labs)
- @mattturck — Matt Turck (FirstMark, AI landscape maps)

**Builders & Creators:**
- @swyx — Swyx (Latent Space, AI engineering)
- @petergyang — Peter Yang (product/AI creator)
- @danshipper — Dan Shipper (Every, AI workflows)
- @steipete — Peter Steinberger (indie dev, AI tools)
- @adityaag — Aditya Agarwal (ex-Dropbox CTO)
- @ryolu_ — Ryo Lu (builder/creator)
- @thenanyu — Nan Yu (AI builder)
- @realmadhuguru — Madhu Guru (AI builder)
- @_catwu — Cat Wu (AI builder)
- @trq212 — Thariq (AI builder)
- @nikunj — Nikunj Kothari (AI builder)
- @zarazhangrui — Zara Zhang (VC, AI/startup)

**Official Accounts:**
- @ycombinator — YC official
- @GoogleLabs — Google Labs official

Always ask the user: "Want to add or remove anyone from this list?"

---

## Appendix B: Universal High-Performing Post Formats

1. **Quote repost with founder insight** — ride trending posts with your unique angle (highest traffic potential)
2. **Product demo with surprising results** — "I told [product] to do X and it did Y" (curiosity + proof)
3. **Step-by-step workflow breakdowns** — numbered lists showing a real process (dwell time + saves)
4. **Founder reflection / build-in-public** — personal lessons, struggles, wins (authenticity + DM shares)
5. **Casual humor / self-deprecating discovery** — "wait, did my own tool just..." (relatability + replies)

---

## Appendix C: X Algorithm Optimization Tactics

Based on X's Phoenix algorithm (Grok-based transformer, predicts 19 user actions):

### High-Value Signals to Optimize For
1. **Replies** — End posts with questions, hot takes, fill-in-blank prompts, controversial (but genuine) opinions
2. **DM Shares** — Write posts people want to send to someone: stats, frameworks, niche insights, "you need to see this" content
3. **Dwell Time** — Longer posts, line breaks, stories with tension, numbered lists, progressive reveals
4. **Video Quality Views** — 30-90 sec, hook in first 2 sec, captions always on
5. **Profile Clicks** — Tease expertise without revealing everything, subtle credentials, "I've been doing X for Y years"
6. **Reposts & Quote Tweets** — Make content feel like a personal discovery the reader wants to amplify

### Signals to Avoid (Score Killers)
- ❌ "Not Interested" — triggered by off-topic or irrelevant content
- ❌ Mute/Block — triggered by aggressive, spammy, or repetitive posting
- ❌ Unfollow — triggered by consistent disappointment

### Structural Rules
- **Author Diversity Filter**: Your 2nd post in a feed gets downranked → space posts 2-3 hours apart
- **Topical Consistency**: The retrieval model uses your last 127 interactions to build a user vector → stay on-topic for your niche
- **Timing matters less than quality**: A great post at 2am beats a mediocre post at peak hours (candidate isolation in ranking)

---

## Notes for the Agent

- **First run**: Always collect `userProfile` before executing. Confirm details with the user.
- **Subsequent runs**: Reuse stored `userProfile`. Ask "any changes to your profile or watchlist?" only occasionally.
- **Manual trigger**: When the user says "run my X briefing" or similar, execute the full workflow immediately.
- **Scheduled trigger**: When run as a cron workflow, execute silently and send the email without confirmation.
- **Adapt the briefing**: The competitor list, builder list, and keyword list should evolve over time based on user feedback. If the user says "add @someone" or "stop tracking @someone", update accordingly.
- **Quality over quantity**: Better to have 3 excellent quote repost drafts than 10 mediocre ones. Every recommendation should be actionable.
