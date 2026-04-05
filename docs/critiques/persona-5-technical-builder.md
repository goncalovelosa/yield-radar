# Persona 5: The Technical Builder

**Name:** Alex (34, backend developer, Austin)
**Capital:** $30K (but evaluates products primarily on technical merit)
**Experience:** 5 years DeFi, runs his own nodes, contributes to open-source protocols
**Risk Tolerance:** Low for personal funds, but evaluates products on architecture quality
**Telegram:** Moderate — uses bots, but more interested in the product behind them
**Motivation:** Evaluate YieldRadar as a product to self-host, contribute to, or build on top of

---

## Journey Simulation

### Hero Section
**Sees:** "18,632 yield pools on DeFiLlama. Most of them will lose you money."
**Thinks:** "OK, a DeFiLlama wrapper with risk scoring. Let me see the architecture."
**Verdict:** ✅ Clear value prop. Alex immediately wants to evaluate the technical implementation.

### How It Works
**Sees:** Pipeline: Fetch → Filter → Score → Alert
**Thinks:** "Simple pipeline. Good. But what's the data freshness? How is state managed? Is there a database? How do you handle DeFiLlama rate limits?"
**Verdict:** ⚠️ High-level pipeline doesn't address architectural questions a developer would have.

### Risk Scoring Section
**Sees:** "Multi-factor risk model: APY/volatility, TVL quality, trend, impermanent loss, maturity, GoPlus security audit."
**Thinks:** "6 factors. How are they weighted? Is the scoring model configurable? Can I add my own factors if I self-host?"
**Verdict:** ⚠️ No indication that scoring is configurable or pluggable.

### Docs Page
**Navigates to:** /docs
**Sees:** Tech stack, architecture diagram, risk scoring table, self-hosting instructions, changelog
**Thinks:** "OK, this is useful. Node.js 24, TypeScript, SQLite, Grammy, Docker. Clean stack. Architecture is straightforward: DeFiLlama → Fetcher → Filter → SQLite → Scorer → Alert. But..."

**Issues found:**
1. **Scoring table shows factors but not weights** — the table has columns for "Factor", "Weight", "Source" but weights say "Base formula" and "Multiplier" — not actual numbers
2. **Self-hosting instructions are minimal** — `docker compose up -d` but no mention of required env vars, no config documentation
3. **No API documentation** — the bot is Telegram-only, no REST/HTTP API
4. **No contributing guide** — MIT license but no CONTRIBUTING.md, no issue templates
5. **No architecture decision records (ADRs)** — why SQLite over PostgreSQL? Why Grammy over Telegraf?
6. **Changelog is thin** — just v1.0 and v1.1, no detailed release notes

**Verdict:** ⚠️ Docs exist but are surface-level. Alex would want to understand the architecture deeply before self-hosting or contributing.

### GitHub Repository
**Navigates to:** github.com/goncalovelosa/yield-radar
**Thinks:** (would check: README quality, test coverage, CI/CD, issue templates, PR templates, code structure)
**Sees:** Public repo, linked from landing page
**Verdict:** ✅ Repository is accessible. ⚠️ But the landing page links to the public repo (yield-radar) while the actual bot code is in a separate private repo (defi-yield-bot) — this could cause confusion if someone tries to self-host from the landing page repo.

### Security Section
**Sees:** "Code is public on GitHub. Audit it, self-host it, fork it."
**Thinks:** "Wait, which repo? The landing page repo or the actual bot repo? If I clone yield-radar, I get an Astro site, not a bot."
**Verdict:** ❌ CRITICAL: The GitHub link points to the landing page repo, not the bot repo. Self-hosting instructions on the docs page say `git clone https://github.com/goncalovelosa/yield-radar.git` — but that's the website, not the bot.

### Self-Hosting Claim
**Sees:** "Run your own instance with Docker on a $5 VPS"
**Thinks:** "The bot repo is private (defi-yield-bot). The public repo is just the website. So I can't actually self-host. This claim is misleading."
**Verdict:** ❌ CRITICAL: Self-hosting is claimed but the bot repo is private. Either make it public or remove the self-hosting claim.

### Pricing
**Sees:** Pro $9.99/mo, Power $29.99 with API access
**Thinks:** "API access is 'coming soon' — that's what I actually need. I want to pull this data into my own dashboard. No API at launch is a gap."
**Verdict:** ⚠️ No API at launch limits the builder persona's utility.

### Roadmap
**Sees:** REST API access (Power tier)
**Thinks:** "Good, API is planned. But 'Power tier' means I'd need to pay $29.99/mo for API access? For a self-hosted instance, I shouldn't need to pay. Or is the API only for the hosted version?"
**Verdict:** ⚠️ Unclear if API access applies to self-hosted instances or only the SaaS.

---

## Key Findings

### Critical Issues (Will cause immediate distrust)
1. **GitHub link points to wrong repo** — landing page links to yield-radar (website) not defi-yield-bot (actual bot)
2. **Self-hosting is impossible** — bot repo is private, but the page claims you can self-host
3. **Self-hosting instructions are for the wrong repo** — docs say `git clone yield-radar` which gives you an Astro site, not a bot

### Moderate Issues
4. **No API documentation** — REST API is "coming soon" but no spec, no preview
5. **Scoring weights not documented** — docs table shows "Base formula" and "Multiplier" not actual values
6. **No contributing guide** — MIT license invites contributions but there's no CONTRIBUTING.md
7. **No env var documentation** — self-hosting section doesn't list required env vars
8. **Two separate repos not explained** — yield-radar (public, website) vs defi-yield-bot (private, bot) — confusing architecture

### Minor Issues
9. **No ADRs** — architectural decisions aren't documented
10. **No CI/CD badges** — no build status, no test coverage badge on the repo
11. **No issue/PR templates** — low-friction contribution is not set up
12. **Blog empty** — no technical blog posts about architecture decisions

### What Works Well
- MIT license (correct for open source)
- Docker mentioned (developer-friendly deployment)
- Clean tech stack (Node.js, TypeScript, SQLite, Grammy)
- Architecture diagram on docs page (basic but useful)
- Non-custodial (no private key handling = simpler security model)

---

## Alex's Unanswered Questions
- "Which repo is the actual bot? The GitHub link goes to an Astro website."
- "Can I actually self-host? The bot repo seems private."
- "What env vars do I need to configure for self-hosting?"
- "Are the scoring weights configurable?"
- "Can I add custom scoring factors?"
- "When will the REST API be available? What endpoints?"
- "Why SQLite over PostgreSQL for a data-heavy application?"
- "How do you handle DeFiLlama rate limits with 5-minute polling?"
- "Is there a webhook/callback system for alerts instead of just Telegram?"
- "Can I run this without Telegram (just the data pipeline)?"

## Recommendation
**CRITICAL FIX:** Either make defi-yield-bot public or remove all self-hosting claims. The current state is misleading — the GitHub link, docs, and security section all imply you can self-host, but you can't because the bot repo is private.

If keeping the bot private: remove self-hosting claims, change "Open source" to "Open source (website)" or similar. If making it public: update all links to point to the correct repo, add proper self-hosting docs, and add env var documentation.
