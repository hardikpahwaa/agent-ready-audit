# Agent-Ready Audit

**Is your product ready for AI agents?** This Claude skill checks how easily ChatGPT, Claude, Perplexity, Gemini and browser agents can **find**, **understand**, **use** and **pay for** your product. You get a score out of 100 and a ranked list of fixes.

Give it a URL and ask *"Is this agent-ready?"*

## What you get

1. **Verdict:** a total score and a band (agent-ready · findable but clunky · visible to humans only · invisible to agents)
2. **Pre-flight check:** are AI bots blocked by your robots.txt or firewall?
3. **Scorecard** across 6 areas, weighted by business type (SaaS, store, local business, content site):

   | Area | The question it answers |
   |---|---|
   | A. AI search discoverability | Can AI find and cite you? |
   | B. Content & structured data | Can AI understand and quote you? |
   | C. Browser-agent usability | Can an agent use your site? |
   | D. Actions & API | Can an agent do the job without your UI? |
   | E. Connectors, MCP & auth | Are you plugged into Claude / ChatGPT? |
   | F. Pricing & payments | Can an agent buy or pay per use? |

4. **AI visibility spot-check:** 10 buyer questions to test in ChatGPT, Claude, Perplexity and Gemini
5. **Your agent's to-do list:** the 5–10 actions an agent would want from you, written as connector tools
6. **Pricing for agents:** a usage-based model alongside your current one
7. **One-page connector spec:** ready to hand to a developer
8. **Top 10 fixes:** ranked by impact × effort, quick wins first, with who should do each one
9. **How to measure progress:** 3 metrics to track monthly

It only gives a check a pass when it has seen the evidence, it attributes every statistic to its source, and it never recommends tricks like hidden prompts or showing AI different content.

## Install

**Claude Code**
```
/plugin marketplace add hardikpahwaa/agent-ready-audit
/plugin install agent-ready-audit@agent-ready-audit
```

**Claude.ai / Claude desktop app**
1. Download `agent-ready-audit.zip` from the [latest release](https://github.com/hardikpahwaa/agent-ready-audit/releases/latest)
2. Go to **Settings → Capabilities → Skills** and upload the zip

**Manual (Claude Code)**
```
git clone https://github.com/hardikpahwaa/agent-ready-audit
cp -R agent-ready-audit/skills/agent-ready-audit ~/.claude/skills/
```

## Use it

> Audit https://example.com. Is it agent-ready?

> How do I get my store cited by ChatGPT and Perplexity?

> We're a SaaS. Should we build a Claude connector, and how should we price for agents?

Works best when Claude can browse the web. Without it, the skill audits from what you give it and marks those scores "unverified".

## What's inside

```
skills/agent-ready-audit/
├── SKILL.md                         # the audit method
└── references/
    ├── checklist.md                 # every check, by area
    ├── measurement.md               # how to track AI visibility and agent usage
    ├── pricing-and-connectors.md    # pricing models + MCP connector design rules
    └── sources.md                   # credits and sources
```

## Credits

Written by **Hardik Pahwa** ([@hardikpahwa.ai](https://www.instagram.com/hardikpahwa.ai/)). Built on methods from open-source work by Forter, AgriciDaniel, AgentReady, zubair-trabzada, Corey Haines and Anthropic, plus 2026 talks and videos from Ahrefs, Chrome for Developers, Google Cloud and others. Full list in [sources.md](skills/agent-ready-audit/references/sources.md).

## License

MIT. See [LICENSE](LICENSE).
