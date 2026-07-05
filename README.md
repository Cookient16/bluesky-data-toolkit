# Bluesky Data Toolkit — APIs, code examples & ready-made tools

Everything you need to pull **public data out of Bluesky** (27M+ MAU, fully open AT Protocol): raw API examples, working code, and hosted tools for mentions monitoring, profile analytics, and follower exports. No login or API key required for any of it.

> 📈 **[Bluesky This Week](./reports/)** — auto-generated weekly snapshot of trending topics and mention volumes, produced with the tools below.

## The 60-second API tour

**Search posts (mentions monitoring):**
```bash
curl "https://api.bsky.app/xrpc/app.bsky.feed.searchPosts?q=YOUR_BRAND&sort=latest&limit=100"
```

**Get any profile:**
```bash
curl "https://api.bsky.app/xrpc/app.bsky.actor.getProfile?actor=bsky.app"
```

**Export followers (paginated):**
```bash
curl "https://api.bsky.app/xrpc/app.bsky.graph.getFollowers?actor=bsky.app&limit=100"
```

**Trending topics:**
```bash
curl "https://api.bsky.app/xrpc/app.bsky.unspecced.getTrendingTopics?limit=10"
```

⚠️ Note: `public.api.bsky.app` returns **403 for search** since mid-2026 — use `api.bsky.app`.

## Node.js example: brand mentions with engagement

```js
const res = await fetch('https://api.bsky.app/xrpc/app.bsky.feed.searchPosts?q=anthropic&sort=latest&limit=25');
const { posts } = await res.json();
for (const p of posts) {
    console.log(`${p.author.handle}: ${p.record.text.slice(0, 80)} [♥${p.likeCount} ↻${p.repostCount}]`);
}
```

## Hosted tools (no code, scheduled runs, CSV/JSON export)

| Tool | What it does |
|---|---|
| [Bluesky Mentions Scraper](https://apify.com/cooki/bluesky-mentions-scraper) | Brand/keyword monitoring with sentiment, engagement filters & author enrichment |
| [Bluesky Profile Scraper](https://apify.com/cooki/bluesky-profile-scraper) | Bulk profiles + full follower/following exports |
| [AI Brand Visibility Tracker](https://apify.com/cooki/ai-brand-visibility-tracker) | Does ChatGPT / Perplexity / Gemini mention your brand? (GEO tracking) |

All three also work as **MCP tools** inside Claude, Cursor, and other AI agents via [Apify's MCP server](https://mcp.apify.com).

## FAQ

**Is this allowed?** These endpoints serve public data and the AT Protocol is open by design. Respect rate limits and applicable laws when using the data.

**Do I need a Bluesky account?** No — all endpoints above are unauthenticated.

**How fresh is search?** Posts appear in search within seconds; `sort=latest` returns newest first.
