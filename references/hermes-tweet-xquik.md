# Hermes Tweet / Xquik Evidence Route

Use this route when the agent has `XQUIK_API_KEY` or `HERMES_TWEET_API_KEY`.
It gives the daily briefing a repeatable read-only collection path before the
agent drafts recommendations.

## Environment

```bash
export XQUIK_API_KEY="xq_..."
# Optional for compatible deployments:
export XQUIK_BASE_URL="https://xquik.com"
```

If no key is configured, continue with the browser-based workflow in
`SKILL.md`.

## Collection Plan

1. Normalize the briefing window to the past 12-24 hours.
2. Fetch each competitor and product account timeline.
3. Search each `industryKeywords` item with a recency qualifier.
4. Fetch recent posts from the highest-priority builders.
5. Read thread or reply context only for posts being considered as quote repost
   or reply targets.
6. Deduplicate by post URL before ranking opportunities.

## Evidence Log

Keep a private working log while researching. Do not include API keys or raw
headers in the log.

```text
source_type: keyword | profile | post | thread | replies
source: "@handle" or "keyword query"
collected_at: ISO-8601 timestamp
method: hermes-tweet-xquik
url: direct X post/profile URL
summary: one factual sentence
metrics: replies, reposts, likes, views when available
briefing_section: top_news | competitor_watch | quote_repost | post_idea | reply_target | account_pulse
```

## Output Rules

- Cite direct post URLs in the briefing wherever possible.
- Keep observed evidence separate from inferred recommendations.
- Treat metrics as point-in-time observations.
- Use browser verification for any ambiguous, deleted, or protected content.
- Do not perform write actions. Draft quote reposts and replies as suggestions
  only.
