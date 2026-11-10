# Measuring AI visibility and agent usage

## 1. Prompt panel (the main metric)
- Write 20–50 prompts a real buyer would ask: "best [category] for [audience]", "[brand] vs [competitor]", "alternatives to [competitor]", "[brand] pricing", "is [brand] good for [use case]".
- Run them monthly in ChatGPT, Claude, Perplexity, Gemini and Google AI Mode. Record for each: brand mentioned? site cited? recommended? anything wrong?
- Track "mentioned", "cited" and "recommended" separately. Mentions without citations mean off-site reputation is working but your pages aren't the source.
- Brand gap: list prompts where competitors appear and you don't, and topics AI ties to someone else.
- Tools if they want automation: Ahrefs Brand Radar, Semrush AI toolkit, Peec AI (named by the creators researched; not endorsements).

## 2. Traffic
- Create an "AI assistants" channel in GA4 for referrers like chatgpt.com, claude.ai, perplexity.ai, gemini.google.com, copilot.microsoft.com. It undercounts (many AI visits arrive as direct).
- Watch delayed effects: branded searches and direct visits rising in the weeks after AI visibility improves.
- Add "How did you hear about us?" to signup/checkout with an "AI assistant (ChatGPT, Claude…)" option. Ahrefs reported AI visitors were 0.5% of traffic but 12.1% of signups (their data).
- Find 404s from AI referrers and redirect them.

## 3. Bots
- From server or CDN logs, count hits by AI bot type (training / search / user-triggered) per page. Verify against the vendors' published IP ranges, since user agents can be faked.
- Track fetches of robots.txt, sitemap.xml, llms.txt, .md pages, /.well-known files, the OpenAPI spec and /mcp.
- Cloudflare's AI Crawl Control dashboard shows this without log work.

## 4. Agent usage (if they have an API/MCP)
- MCP connections, tool calls per tool, error rate, OAuth sign-ins, paid calls.
- "Agent defaults" test: give real tasks to clean agent sessions (Claude, ChatGPT, a coding agent) and record which product the agent picks.

## 5. Re-audit
Re-run this audit and Lighthouse's Agentic browsing check after each round of fixes; compare scores.
