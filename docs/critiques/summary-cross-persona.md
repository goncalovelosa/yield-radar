# YieldRadar Landing Page — Cross-Persona Critique Summary

**Date:** 2026-04-05
**Personas:** 5 (Beginner, Farmer, Whale, Degen, Builder)

---

## Issue Aggregation by Severity

### 🔴 CRITICAL (Fix before launch)

| # | Issue | Personas Affected | Impact |
|---|-------|-------------------|--------|
| C1 | **GitHub link points to wrong repo** — links to yield-radar (website) not defi-yield-bot (bot) | Builder | Self-hosting is impossible, creates immediate distrust |
| C2 | **Self-hosting claim is false** — bot repo is private, but page says "audit it, self-host it, fork it" | Builder | Misleading claim, legal/trust issue |
| C3 | **Docs self-hosting instructions clone wrong repo** — `git clone yield-radar` gives Astro site, not bot | Builder | Anyone following docs gets the wrong project |
| C4 | **Blog page is empty** — "Coming soon" with no content | All | Undermines credibility, suggests inactive project |

### 🟠 HIGH (Fix soon after launch)

| # | Issue | Personas Affected | Impact |
|---|-------|-------------------|--------|
| H1 | **No FAQ section** — beginners have 20+ unanswered questions | Beginner, Degen | High bounce rate from confused visitors |
| H2 | **No plain-English intro** — "DeFi", "yield pool", "TVL", "IL" never defined | Beginner | Alientates largest potential user segment |
| H3 | **Hero is fear-based** — "Most of them will lose you money" as opening line | Beginner | Creates anxiety instead of curiosity |
| H4 | **Scoring methodology not transparent** — no weights, no formula, no link to docs | Farmer, Whale | Users who understand scoring can't trust it |
| H5 | **"Priority discovery" undefined** — Pro tier feature with no explanation | Farmer, Degen | Users can't evaluate if Pro is worth paying for |
| H6 | **No social proof** — no user count, no testimonials, no community size | All | No evidence anyone uses this |
| H7 | **Free tier too restrictive** — 3 alerts/day may not show enough value to convert | Degen, Farmer | Users hit limit before experiencing value, churn |
| H8 | **No Telegram Stars payment explanation** — users may not know how to pay | Beginner, Degen | Conversion friction at payment step |

### 🟡 MEDIUM (Fix in v1.2)

| # | Issue | Personas Affected | Impact |
|---|-------|-------------------|--------|
| M1 | **No link from landing page to docs** — scoring table exists but isn't linked | Farmer | Interested users can't find technical details |
| M2 | **Mockup data is static** — not labeled with dates, could be outdated | Farmer, Whale | Undermines "real-time" claim |
| M3 | **No Ethereum pool in mockups** — largest chain by TVL unrepresented | Farmer, Whale | Seems like an oversight |
| M4 | **No roadmap timelines** — "Next up" and "Planned" have no dates | Farmer, Whale | Hard to evaluate if project is actively maintained |
| M5 | **Chain coverage missing hot chains** — no Optimism, Avalanche, Hyperliquid, Sui | Degen | Users on those chains feel excluded |
| M6 | **"Audit status" dangerously vague** — doesn't specify auditor or scope | Whale | Could lead to false trust in unaudited protocols |
| M7 | **GoPlus presented as definitive** — no mention of limitations | Whale, Builder | Overstates security coverage |
| M8 | **Self-hostable description uses jargon** — "Docker on a $5 VPS" | Beginner | Irrelevant and confusing to non-developers |
| M9 | **No onboarding preview** — users don't know what /start asks them | Farmer, Beginner | Uncertainty about commitment |
| M10 | **No Twitter/X link** — missing major social channel | Degen, All | No social proof from crypto community |

### 🟢 LOW (Polish / Nice-to-have)

| # | Issue | Personas Affected |
|---|-------|-------------------|
| L1 | Footer says "MIT License" without link to license file | Builder |
| L2 | No favicon (minor) | All |
| L3 | No mobile-responsive roadmap breakpoint between 2-col and 1-col | All (small screens) |
| L4 | "Alt-us" column in comparison table could use highlight background | All |
| L5 | No contributing guide or issue templates on GitHub | Builder |
| L6 | No CI/CD badges on repo | Builder |
| L7 | Roadmap "Future" column uses technical jargon (ERC-4337) | Beginner, Degen |
| L8 | Pricing card Free tier CTA could be more prominent | Beginner |
| L9 | No breadcrumb navigation | All |
| L10 | No cookie/privacy policy page | All (legal) |

---

## Quick Wins (Fixed Tonight)

These are issues I can fix directly in code right now:

### Fix 1: Blog page — remove or redirect
**Problem:** Empty "Coming soon" page undermines credibility.
**Fix:** Redirect /blog to / or remove the link from nav.

### Fix 2: Add FAQ section to landing page
**Problem:** No FAQ for common questions.
**Fix:** Add FAQ section based on cross-persona unanswered questions.

### Fix 3: Add Twitter/X link to footer and nav
**Problem:** No social media presence link.
**Fix:** Add X/Twitter placeholder link.

### Fix 4: Add docs link to landing page
**Problem:** Scoring details exist on /docs but aren't linked from main page.
**Fix:** Add "See how scoring works" link in the risk scoring section.

### Fix 5: Fix GitHub link to point to correct repo
**Problem:** Links to yield-radar (website) instead of defi-yield-bot (bot).
**Fix:** Update all GitHub links. Note: since bot repo is private, we need to either make it public or adjust the messaging.
**DECISION NEEDED FROM GONÇALO:** Make defi-yield-bot public or remove self-hosting claims?

### Fix 6: Add an Ethereum pool to mockups
**Problem:** No Ethereum example in preview section.
**Fix:** Replace or add an Ethereum pool (e.g., Aave USDC or Curve 3pool).

### Fix 7: Remove or soften "self-hostable" claims
**Problem:** Self-hosting is claimed but bot repo is private.
**Fix:** Temporarily adjust wording until bot repo is made public.

### Fix 8: Add "New to DeFi?" link or explainer
**Problem:** No onboarding for beginners.
**Fix:** Add a brief explainer or link to an external resource.

### Fix 9: Clarify "Priority discovery" in Pro tier
**Problem:** Undefined feature.
**Fix:** Either define it or remove it from the pricing card.

### Fix 10: Add dates to roadmap items
**Problem:** No timelines.
**Fix:** Add approximate quarters or "Q2 2026" to Next Up items.

---

## Persona Conversion Probability (Before Fixes)

| Persona | Likelihood to Try Free | Likely to Convert to Pro | Blocker |
|---------|----------------------|-------------------------|---------|
| Cautious Beginner | 30% | 10% | Jargon, no FAQ, fear-based hero |
| Active Yield Farmer | 70% | 60% | Scoring transparency, undefined features |
| Security Whale | 20% | 5% | Too simplistic, too cheap = low trust |
| Telegram Degen | 80% | 40% | 3 alerts/day too restrictive, slow speed |
| Technical Builder | 60% | 20% | Wrong repo link, can't self-host |

**Primary target for v1:** Active Yield Farmer + Telegram Degen (highest conversion potential)
**Secondary:** Cautious Beginner (largest market, needs more hand-holding)
**Not targeting yet:** Security Whale (needs v2 features)
