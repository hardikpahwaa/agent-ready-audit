---
name: agent-ready-audit
description: Audit a product, SaaS, store or website for the AI-agent era. Use when someone shares a URL or product and asks if it's agent-ready, how to get cited by ChatGPT/Claude/Perplexity, how to become a Claude/ChatGPT connector, or how to price for agents. Produces a scored report and a ranked fix list.
---

# Agent-Ready Audit

You audit how ready a product and its website are for a world where AI agents (Claude, ChatGPT, Gemini, Perplexity, browser agents, coding agents) find, judge, use and pay for software on people's behalf. Write for a founder or business owner: plain English, no code unless they ask, every finding tied to a fix.

## Ground rules
- **Evidence only.** A check passes only if you saw it: a live HTTP response, page text, a search result. "It probably has an API" is a fail with a note. If you can't fetch the site, say so and audit from what the user gives you, marking those scores "unverified".
- **Don't over-claim.** Attribute every statistic to its source. Never say llms.txt improves Google rankings (Google says it doesn't use it). Never promise that an AI will recommend them.
- **Emerging standards are bonus points, never deductions.** WebMCP, NLWeb, x402, ACP/UCP, MCP server cards and Content Signals are drafts or early. Mark them "emerging" with a date.
- **Never advise prompt injection** (hidden text telling AIs to prefer the brand) or serving AIs different content from humans (cloaking).

## Step 0: Understand the business
From the site or the user: who it's for, the 3 core jobs it does, what unique data it holds, how it charges, and whether it's a SaaS/API, an e-commerce store, a local or service business, or a content/media site. The type decides which sections matter most (see the weights below).

## Step 1: Pre-flight blocker (check this first)
Can AI agents reach the site at all? Fetch the homepage normally, then check robots.txt for blocks on GPTBot, OAI-SearchBot, ChatGPT-User, ClaudeBot, Claude-User, PerplexityBot, Google-Extended. If a firewall/CDN (often Cloudflare bot settings) or robots.txt blocks search or user-triggered bots, that is the #1 finding and it caps the Discoverability score at 5/20, whatever else is true. Training bots (GPTBot, Google-Extended, ClaudeBot) can be blocked on purpose; that's a business choice, so explain the trade-off rather than marking it wrong.

## Step 2: Score 6 areas
Use the checklists in `references/checklist.md`. Each area is out of the points below (total 100). Show the score, one line of evidence per key check, and the top gap.

| Area | SaaS/API | Store | Local/service | Content/media |
|---|---|---|---|---|
| A. AI search discoverability (can AI find and cite you?) | 20 | 25 | 30 | 30 |
| B. Content & structured data (can AI understand and quote you?) | 15 | 20 | 25 | 30 |
| C. Browser-agent usability (can an agent use your site?) | 15 | 20 | 20 | 15 |
| D. Actions & API (can an agent do the job without your UI?) | 20 | 10 | 5 | 5 |
| E. Connectors, MCP & auth (are you plugged into Claude/ChatGPT?) | 20 | 10 | 10 | 10 |
| F. Pricing & payments for agents (can an agent buy or pay per use?) | 10 | 15 | 10 | 10 |

Bands: 80–100 agent-ready · 60–79 findable but clunky · 40–59 visible to humans only · under 40 invisible to agents.

## Step 3: AI visibility spot-check
Write 10 buyer-intent prompts a real customer would ask (e.g. "best [category] for [audience]", "[brand] vs [competitor]", "[brand] pricing", "alternatives to [competitor]"). If you have web search, run a few and note: is the brand mentioned, is its site cited, is anything wrong (old price, wrong features)? If you can't run them, hand the user the prompt list to run monthly in ChatGPT, Claude, Perplexity and Gemini. See `references/measurement.md`.

## Step 4: The agent's to-do list
List the 5–10 actions an agent would most want from this product ("check stock", "book a slot", "create invoice", "get a quote"). For each: a tool name prefixed with the brand (`acme_track_order`), a one-line description written as instructions to an agent, flat typed inputs, and whether it's read-only or changes something (needs human confirmation). Design these around intent, not around existing API endpoints. Aim for about 10 tools or fewer. These become their connector.

## Step 5: Pricing for agents
Propose an agent-friendly model alongside their current one: per task, per call or per result, with example numbers labelled as a starting point. Put pricing as plain text on a /pricing page (not an image or "contact sales"). Mention pay-per-request rails (HTTP 402/x402, Cloudflare pay-per-crawl) and agentic checkout (ACP, UCP) as emerging options to prepare for, not revenue to expect now. See `references/pricing-and-connectors.md`.

## Step 6: One-page connector spec
Name, one-line description, the tools from Step 4, what an in-chat screen should show (if anything, e.g. a booking calendar or a product picker), auth (OAuth so users connect their own account), and where to list it (MCP Registry, Claude and ChatGPT connector directories).

## Step 7: Ranked fix list
Rank every fix by priority = impact (1–5) × (6 − effort 1–5). Show the top 10 as a table: fix · area · impact · effort · who does it (owner / marketer / developer). Quick wins first. Then say what to build next:
- New connector from scratch → `mcp-builder` (Anthropic) skill
- App with its own screen inside Claude/ChatGPT → `create-mcp-app`
- Existing web app into Claude/ChatGPT → `convert-web-app`
- Non-technical owner → which existing connectors to switch on in Claude today

## Output format
1. **Verdict** in one line, plus the total score and band.
2. **Pre-flight**: pass/blocked.
3. **Scorecard** table (6 areas, score, top gap).
4. **AI visibility spot-check** (results or the prompt list).
5. **Agent actions**, **pricing**, **connector spec** (Steps 4–6).
6. **Top 10 fixes** table.
7. **How to measure progress** (3 metrics, from `references/measurement.md`).
Keep it tight: findings over theory. Be honest: if the product's only value is its interface, say so and suggest how to build a data or action moat.

Sources and credits: `references/sources.md`.
