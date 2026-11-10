# Audit checklist

Mark each check: ✅ pass (seen live) · ❌ fail · ⚠️ partial · ➖ not relevant · 🧪 emerging (bonus only). Score each area by the share of relevant checks passed, weighting the **bold** ones double.

## A. AI search discoverability
- **AI search and user-triggered bots are allowed** in robots.txt and not blocked by the firewall/CDN (OAI-SearchBot, ChatGPT-User, Claude-User, PerplexityBot). Blocking training bots (GPTBot, ClaudeBot, Google-Extended) is a separate business choice.
- **The pages that matter show up in Google** (AI Overviews mostly cite Google's top 10; Ahrefs reports 76%). Classic SEO is the base layer.
- A complete sitemap.xml with recent `lastmod` dates, submitted in Google Search Console and Bing Webmaster Tools (Bing feeds ChatGPT search).
- **The brand is mentioned off-site**: reviews, "best X" listicles, comparisons, Reddit/forums, podcasts, YouTube. Ahrefs found branded web mentions correlate with AI visibility more than backlinks do.
- Consistent identity: the same one-sentence description on the site, LinkedIn, Crunchbase, app stores, podcast directories; a correct Wikidata entry (and Wikipedia if notable).
- Comparison and "alternatives to" pages exist and are honest.
- Pages people ask AI about exist at obvious URLs: /pricing, /docs, /about, /contact, /faq.
- URLs are stable; AI-hallucinated or old URLs that get traffic redirect instead of 404 (Ahrefs: AI sends visitors to 404s 2.87× more than Google).
- YouTube: evergreen videos answering buyer questions, with the keyword in title, description and speech, and chapters (YouTube is among the most-cited domains in AI answers, per Ahrefs).
- llms.txt at /llms.txt, short, linking key pages: **optional**. Useful for coding agents and docs; Google says Search doesn't use it, and log studies show AI search crawlers rarely fetch it. A 10-minute hedge, never a ranking lever.
- 🧪 Content-Signals line in robots.txt (search / ai-input / ai-train preferences).

## B. Content & structured data
- **Answer first (BLUF):** each key page states the answer in the first 1–2 sentences.
- **Self-contained passages:** sections that make sense quoted alone and name the brand rather than "we".
- **Nothing left to infer:** price, specs, who it's for, eligibility, limitations and next step written out as text.
- Specific facts: numbers, named sources, expert quotes, dates. Lists, tables, comparisons, step-by-steps and FAQs (Ahrefs: lists and comparisons are ~44% of cited formats).
- Freshness: visible "updated" dates; key pages refreshed in the last 90 days (Ahrefs: 76% of ChatGPT's top-cited pages were updated within 30 days).
- Named authors with credentials on expert content.
- Topic coverage: a pillar page plus pages answering the follow-up questions (AI "fans out" one prompt into many searches). Coverage matters, not word count.
- Facts live in HTML, not only in PDFs, images or videos (transcripts on the page).
- **Organization schema** (name, logo, contact, `sameAs` links to official profiles). Product/Offer schema for stores and pricing, LocalBusiness for local, FAQPage where there's a real FAQ. Everything in schema is also visible on the page. Validate it.
- What AI currently says about the brand is accurate (price, features, founders). Fix the source pages if not.
- 🧪 NLWeb `/ask` endpoint.

## C. Browser-agent usability
- **The main content and navigation are in the first HTML response** (works with JavaScript off). Several AI crawlers don't render JS.
- **Good accessibility = agent-readiness:** agents read the accessibility tree. Buttons and links have real labels, forms have labels, one H1, logical headings, image alt text, page language set.
- No hover-only menus, no CAPTCHA on simple read pages, no pop-ups blocking content.
- Fast, stable pages (low layout shift); slow pages get dropped from real-time retrieval.
- Specific calls to action ("Book a 15-min demo", "Start free") rather than "Contact us".
- Correct HTTP codes: real 404s, 429 with Retry-After when rate limiting.
- A markdown version of key pages (linked `.md` pages or served on request); AgentReady measured agents requesting markdown in ~65% of fetches.
- Run Chrome Lighthouse's "Agentic browsing" audit (Chrome 150+) and report X of N checks passed.
- 🧪 WebMCP: forms and actions exposed as tools to browser agents (Chrome origin trial; little support elsewhere). Only relevant for sites with forms, search or checkout.

## D. Actions & API
- **Agents can do the core jobs without the UI:** a public API, an MCP server or a CLI.
- Public OpenAPI 3.x spec: every operation has an ID, description, typed parameters, auth scheme, shared error format and pagination.
- Structured JSON errors that say what went wrong and what to do next.
- Rate limits documented, with headers and 429 + Retry-After.
- Idempotency keys for create/pay actions; signed webhooks; long jobs return 202 + a status URL.
- Self-serve signup and API keys, a sandbox or free tier, no "talk to sales" gate.
- Quickstart docs with copy-paste examples; SDKs on npm/PyPI.
- Clean, complete catalogue/product data (stores): title, price + currency, availability, brand, shipping, returns, reviews.
- A changelog and a status page.
- Agents treated as "just another partner": reuse an existing partner or affiliate API and feed rather than building from zero. Wayfair says it put its 30M-product catalogue on agents this way in under a quarter (Google Cloud Next '26).

## E. Connectors, MCP & auth
- **A remote MCP server** (Streamable HTTP) that initialises, with every tool described and typed. Tools named by intent and prefixed with the brand; about 10 or fewer per server; flat parameters; pagination.
- Read-only vs destructive tools are marked; consequential actions ask the human to confirm.
- OAuth so users connect their own account (authorization-server metadata at `/.well-known/`, PKCE, scoped permissions like `orders:read`); a 401 that points to the auth metadata.
- Listed in the official MCP Registry and the Claude / ChatGPT connector directories (plus Smithery or similar).
- The same brand name and one-line value on the site, llms.txt, MCP server name and tool descriptions.
- An end-to-end test: a real agent finds it, signs in, completes a task and recovers from an error.
- Private data protected by login, not by robots.txt.
- 🧪 MCP Apps (an in-chat screen), MCP server card, A2A agent card.

## F. Pricing & payments for agents
- **Pricing is plain text on /pricing**, not an image, a PDF or a sales form.
- Prices in structured data (Product/Offer) and consistent everywhere AI might read them.
- A usage-based option (per task, call or result) an agent can reason about.
- Each resource classified free / paid / blocked for bots.
- Stores: product feed in Google Merchant Center; checkout that works without forced account creation.
- 🧪 HTTP 402 / x402 or Cloudflare pay-per-crawl for paid content and APIs.
- 🧪 Agentic checkout: ACP (OpenAI + Stripe) or UCP (Google), usually via the store's platform or payment provider. Under UCP, the retailer stays the seller of record.
- 🧪 Agent payment trust: only verified agents, limited spending permissions, signed purchase approvals (AP2 mandates), audit trails, and fraud checks on the agent's decisions as well as the card (Fiserv, Google Cloud Next '26).
