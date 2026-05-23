# x-daily-ai-briefing
Sai Skill: Daily personalized X/Twitter AI briefing — tracks competitors, trending topics, and generates post inspiration tailored to your content pillars, product, and industry.

## Optional Hermes Tweet / Xquik Data Route

This skill can use Hermes Tweet / Xquik for read-only X evidence collection when
the agent has an API key:

- `XQUIK_API_KEY` or `HERMES_TWEET_API_KEY`
- `XQUIK_BASE_URL` (optional, defaults to `https://xquik.com`)

Use the optional route for keyword searches, profile timelines, post reads, and
thread context before drafting the daily briefing. Browser-based research still
works as the default fallback when an API key is not configured.

See `references/hermes-tweet-xquik.md` for the collection plan and evidence log
format.
