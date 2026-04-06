# YieldRadar — Persona Critique Round 2: Synthesis & Action Plan

**Date:** 2026-04-06
**Personas:** 5 (Priya, James, Lena, Chen Wei, Aisha)
**Scope:** yieldradar.io landing page + @yieldradar_bot Telegram experience
**Verified against:** `yield-radar/src/pages/index.astro`, `defi-yield-bot/src/` source code

---

## Personas

| # | Name | Title | Profile | DeFi XP | Portfolio |
|---|------|-------|---------|---------|-----------|
| 1 | **Priya** | Cross-Chain Yield Optimizer | 32F, SWE Bangalore, $150K multi-chain | Advanced | $150K |
| 2 | **James** | Skeptical Crypto Podcaster | 38M, Austin, 15K listeners, credibility-first | Intermediate | $50K |
| 3 | **Lena** | Part-Time Stablecoin Saver | 45F, Munich accountant, €30K idle on Coinbase | Beginner | €30K |
| 4 | **Chen Wei** | Algorithmic Finance Student | 24M, Tsinghua CS+Finance, builds yield scripts | Advanced (academic) | $2-8K |
| 5 | **Aisha** | African Remittance Optimizer | 29F, Lagos fintech PM, $5-20K working capital, honeypot trauma | Low-Medium | $5-20K |

---

## 1. Issue Aggregation

### 🔴 CRITICAL — Fix Before Any Marketing Push

| # | Issue | Verified | Personas |
|---|-------|----------|----------|
| C1 | **False transparency claim** — Landing page says "Transparent codebase" + GitHub link, but bot repo is PRIVATE. Only the Astro landing page is public. | ✅ `index.astro:373-374` | Priya, James, Chen Wei, Aisha |
| C2 | **Brand mismatch** — Bot welcome says "DeFi Yield Chaser" (`bot.ts:74`), invoice title says "DeFi Yield Chaser Pro" (`payments.ts:35`), but landing page says "YieldRadar". Looks like a phishing clone. | ✅ 3 files in bot | James, Lena, Chen Wei, Aisha |
| C3 | **"Invest" button links to wrong page** — Both `format-alert.ts:37` and `format-deep-dive.ts:22` construct `defillama.com/protocol/{project}` (protocol page) instead of the specific pool URL. Users ready to invest land on a generic page. | ✅ 2 formatters + 3 test files | Priya, James, Lena, Chen Wei, Aisha |

### 🟠 HIGH — Fix Within 1 Week

| # | Issue | Verified | Personas |
|---|-------|----------|----------|
| H1 | **Alert count inconsistency** — Landing page says "3 alerts per day" (`index.astro:317,495`) but bot code has `FREE_TIER_DAILY_LIMIT = 10` (`quota-manager.ts:43`) and `/status` message says "10 alerts/day" (`payments.ts:121`). | ✅ Landing page vs bot code | Priya, James, Chen Wei |
| H2 | **Risk mental model mismatch** — Onboarding offers 3 levels (Conservative/Moderate/Aggressive → mapped to scores ≥75/≥50/≥25) but scoring has 4 tiers (Safe/Watch/Speculative/Danger at 75/50/25/0). "Speculative" (25-49) has no onboarding analog. | ✅ `pool-filter.ts:22-30` | Priya, Lena, Chen Wei, Aisha |
| H3 | **Zero social proof** — No team identity, user count, testimonials, or audit badges anywhere. Anonymous product = scam signal for trust-anxious users. | ✅ No social proof in codebase | James, Lena, Aisha |
| H4 | **Digest has no inline navigation** — `format-digest.ts` outputs plain text pool list with only Settings/ViewAll buttons. No per-pool deep-dive buttons. | ✅ `format-digest.ts` | Priya, Chen Wei |

### 🟡 MEDIUM — Fix in v1.2

| # | Issue | Personas |
|---|-------|----------|
| M1 | No minimum APY threshold in onboarding or settings | Priya, Lena, Chen Wei |
| M2 | "View All" shows only top 10 pools regardless of tier (`settings.ts` → `getTopPools(100).slice(0,10)`) | Priya, Chen Wei |
| M3 | No reward token emission schedule / incentive decay in alerts | Priya, Chen Wei |
| M4 | Deep dive shows TVL multiplier but not raw TVL number | Priya, Chen Wei, James |
| M5 | Asset type filter (stablecoin/mixed/defi_native) has no explanation of what it filters | Lena, Aisha |
| M6 | No public methodology documentation (sigma window, multiplier weights) | Chen Wei, Priya |
| M7 | No API or data export for technical users | Chen Wei, Priya |

### 🟢 LOW — Polish

| # | Issue | Personas |
|---|-------|----------|
| L1 | Jargon without definitions (IL, sigma, TVL) | Lena, Aisha |
| L2 | No mobile-optimized for slow connections | Aisha |
| L3 | No stablecoin-specific filter in onboarding | Aisha, Lena |
| L4 | No beginner onboarding branch | Lena |
| L5 | Types.ts comment says conservative = ">100 score" but code says ≥75 | Chen Wei |

---

## 2. Conversion Analysis

| Persona | Try Free | Convert Pro | Main Blocker |
|---------|----------|-------------|--------------|
| **Priya** ($150K) | 75% | 55% | Needs to verify scoring quality; no API export |
| **James** (15K listeners) | 60% | 25% | Can't recommend without trust fixes (C1, C2, H3) |
| **Lena** (€30K) | 35% | 5% | Jargon + no social proof + no beginner path |
| **Chen Wei** (student) | 80% | 40% | Black-box scoring; will reverse-engineer and leave |
| **Aisha** ($5-20K) | 25% | 10% | Honeypot trauma × brand mismatch × no trust signals |

**Aggregate: 55% try free → 27% convert to Pro**

The funnel leaks at the TRUST layer, not the utility layer. Every persona agreed the concept is valuable — the blockers are credibility and consistency.

---

## 3. Priority Action Plan

### P0 — This Week (Code Changes)

**1. Fix "Transparent codebase" claim** [C1]
- **Files:** `yield-radar/src/pages/index.astro` lines 373-374
- **Change:** Replace "Transparent codebase" + GitHub link with "Methodology-transparent scoring" linking to `/docs`. Remove "no black boxes" language. Do NOT claim open source for the bot.
- **Effort:** Small (content change)

**2. Fix brand mismatch** [C2]
- **Files:** `defi-yield-bot/src/telegram-bot/bot.ts:74`, `payments.ts:35`, `payments.test.ts:118`
- **Change:** Replace all "DeFi Yield Chaser" with "YieldRadar". Update invoice title and welcome message.
- **Effort:** Small (3 string replacements)

**3. Fix "Invest" button URL** [C3]
- **Files:** `format-alert.ts:36-37`, `format-deep-dive.ts:21-22`, `format-alert.test.ts`, `format-deep-dive.test.ts`
- **Change:** Check if DeFiLlama pool URL format exists (e.g., `defillama.com/pool/{poolId}`). If pool data has a DeFiLlama pool ID, use it. Otherwise, construct the best possible URL. Update tests.
- **Effort:** Medium (requires checking DeFiLlama URL schema + test updates)

**4. Align alert count** [H1]
- **Files:** `yield-radar/src/pages/index.astro` lines 317, 495
- **Change:** "3 alerts per day" → "10 alerts per day"
- **Effort:** Small (2 string replacements)

### P1 — Next Sprint

**5. Unify risk model** [H2]
- **Files:** `onboarding.ts:37-39`, `settings.ts:141-143`, `pool-filter.ts`, `types.ts`
- **Change:** Change onboarding to 4 options: "Safe Only / Safe+Watch / All Except Danger / Everything". Map to score thresholds ≥75/≥50/≥25/≥0. Update types, filter logic, and settings.
- **Effort:** Medium (cross-cutting: types, onboarding, settings, filter, tests)
- **Justifies GSD spec** ✅

**6. Add digest inline buttons** [H4]
- **Files:** `format-digest.ts`, `format-digest.test.ts`
- **Change:** Add inline keyboard buttons per pool in digest (📊 Deep Dive, 🔗 Invest, 🔕 Mute). Reuse existing callback patterns from `format-alert.ts`.
- **Effort:** Small-Medium
- **Justifies GSD spec** ✅

**7. Add social proof section** [H3]
- **Files:** `yield-radar/src/pages/index.astro` (new section)
- **Change:** Add "Built by" section with developer identity, early adopter count, and optional beta quotes. This is a content/marketing task — needs Gonçalo input on what to reveal.
- **Effort:** Medium (content creation)

### P2 — v1.2

**8. Add minimum APY threshold** [M1] — Medium effort
**9. Increase "View All" cap for Pro** [M2] — Small effort
**10. Show raw TVL in deep dive** [M4] — Small effort (data already available)
**11. Explain asset type filter** [M5] — Small effort (tooltip text)
**12. Create `/methodology` page** [M6] — Large effort (content + new page)
**13. Add API endpoint** [M7] — Large effort (new route + auth + docs)

---

## 4. GSD Spec Recommendations

These fixes are substantial enough for Claude Code + GSD autonomous execution:

| # | Spec Title | Covers | Effort |
|---|-----------|--------|--------|
| 1 | **"Fix Trust & Brand Inconsistencies"** | C1 + C2 + H1 (transparency claim, brand name, alert count) | Small-Medium |
| 2 | **"Fix Invest Button + Add Digest Navigation"** | C3 + H4 (pool URL, digest buttons) | Medium |
| 3 | **"Unify Risk Model 3→4 Levels"** | H2 (onboarding, settings, filter, types) | Medium |

---

## 5. What's Already Good (DO NOT CHANGE)

Strengths acknowledged by 4+ personas:

- **Scoring concept** — Composite risk-adjusted yield score via Telegram is genuinely useful
- **Telegram-native format** — Push alerts in Telegram preferred over separate apps by ALL personas
- **Multi-chain coverage** — 6 chains covering 75%+ DeFi TVL is a differentiator
- **GoPlus security integration** — Security as a weighted score factor (not just pass/fail) reduces cognitive load
- **Free tier generosity** — 10 alerts/day is genuinely generous for evaluation
- **Digest format** — Consolidated daily report praised as non-spammy and scannable
- **0-100 normalized score** — Intuitive scale, well-received tier labels
- **Non-custodial positioning** — "No wallet needed" resonates with every risk-conscious persona
