# Pricing for agents and connector design

## Why per-seat breaks
An agent isn't a seat. One person's agent may call a tool 500 times a day, or once a month. Price what the agent consumes: a task done, a call made, a result delivered.

## Models to suggest (label example numbers as a starting point)
- **Per task/result:** e.g. per report generated, per lead enriched, per booking made.
- **Per call with a free allowance:** e.g. first 1,000 calls free, then a small fee per 1,000.
- **Credits:** a prepaid balance agents draw down; easy to cap.
- **Hybrid:** keep the human plan; add an "agent/API" plan priced by usage.
Always keep a free tier or sandbox so an agent can try it before a human approves spend.

## Payment rails (emerging; prepare, don't expect revenue yet)
- **HTTP 402 / x402:** the server answers "402 Payment Required" with a price; the agent pays and retries with proof. Cloudflare offers pay-per-crawl and payment rules at the edge.
- **ACP (OpenAI + Stripe)** and **UCP (Google):** let an AI assistant complete checkout. Most stores get these through their platform or payment provider, not by building them. Reports in 2026 say OpenAI scaled back in-chat checkout, so treat this as early.
- **Free / paid / blocked:** classify every resource (public pages free, premium data paid, private data blocked).

## Connector (MCP) design rules
- Start from the 5–10 jobs a user would ask an agent to do, not from your API endpoints.
- Name tools by intent and prefix with the brand: `acme_search_products`, `acme_track_order`.
- Descriptions are instructions to the agent: say when to use the tool, what it returns, and what to do next.
- Flat, typed inputs; mark required fields; paginate long results.
- Errors say what went wrong and how to fix it.
- Mark read-only vs destructive tools; ask the human to confirm payments, deletes and sends.
- One product per server; about 10 tools or fewer; remove tools nobody uses.
- Auth with OAuth so each user connects their own account, with narrow scopes.
- Test two ways: normal tests for each tool, and real agent runs checking it picks the right tool with the right inputs.
- Only build an MCP server if the product has real data or actions to offer; otherwise fix the website first.

## Where to point builders
- New connector: Anthropic's `mcp-builder` skill.
- Connector with its own in-chat screen: `create-mcp-app`.
- Existing web app into Claude/ChatGPT: `convert-web-app`; existing connector + screen: `add-app-to-server`; ChatGPT app → also Claude: `migrate-oai-app`.
- Agent-friendly API descriptions: LAP.
