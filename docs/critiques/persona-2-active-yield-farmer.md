# Persona 2: The Active Yield Farmer

**Name:** Marcus (28, software engineer, Berlin)
**Capital:** $65K split across Ethereum, Arbitrum, Base, and Solana
**Experience:** 2 years DeFi, farms on Aave, Curve, Aerodrome, Raydium. Understands IL, gas, bridging.
**Risk Tolerance:** Moderate — optimizes for risk-adjusted yield, won't touch unaudited contracts
**Telegram:** Heavy user — 8 crypto groups, uses Banana Gun, follows multiple alpha channels

---

## Journey Simulation

### Hero Section
**Sees:** "18,632 yield pools on DeFiLlama. Most of them will lose you money."
**Thinks:** "Fair point. I currently check DeFiLlama manually. If this pushes relevant pools to me, that's valuable."
**Verdict:** ✅ Hero resonates. Marcus knows DeFiLlama and the pain of manual checking.

### The Problem Section
**Sees:** Stats grid — 18,632 pools, ~3,800 pass filters, 6 chains, 5 min between scans
**Thinks:** "3,800 pools pass filters? That's still a lot. What are the quality filters? $500K TVL minimum is mentioned in the pipeline — that seems reasonable."
**Verdict:** ✅ Stats are meaningful and verifiable. ⚠️ "Pass our quality filters" is vague — what are the filters exactly?

### How It Works
**Sees:** Fetch → Filter → Score → Alert
**Thinks:** "Solid pipeline. GoPlus integration is good. But how does the scoring actually work? 'Multi-factor risk model' with 6 factors — can I see the weights?"
**Verdict:** ⚠️ Scoring methodology is described at a high level but lacks detail. Marcus would want to know the exact factors and weights to evaluate if the scoring is useful.

### Comparison Table
**Sees:** YieldRadar vs DeFiLlama manual vs Alpha Telegram groups
**Thinks:** "This is exactly the comparison I'd make. DeFiLlama is free but manual. Telegram groups are spam. If this actually does push personalized alerts, it fills the gap."
**Verdict:** ✅ Comparison table is strong and honest.

### Risk Scoring Section
**Sees:** 4 tiers (Safe/Watch/Speculative/Danger) with score ranges
**Thinks:** "OK, but how much weight does GoPlus get vs TVL? What's the formula? I want to understand if a 'Safe' pool with 15% APY on a new protocol actually deserves that label."
**Verdict:** ⚠️ Lacks transparency on scoring weights/formula. The docs page has a table of factors and weights — but the landing page doesn't link there.

### Preview / Mockups
**Sees:** Aerodrome USDC-AERO (Watch, 19.1%), Uniswap V4 WETH-EAT (Speculative, 17.9%), Raydium WSOL-RAY (Danger, 47.1%)
**Thinks:** "Good examples — covers different risk tiers. But I notice these are all Base and Solana. Where's the Ethereum example? Also, the Aerodrome pool shows 'Watch' at 19.1% — I currently farm there. Is the score telling me something I don't know?"
**Verdict:** ⚠️ No Ethereum pool example. ⚠️ Mockup data is static — it would be more compelling if it showed actual live data or noted "example from [date]."

### Getting Started
**Sees:** 3 steps
**Thinks:** "Simple enough. But I want to know: can I customize my filters before I start getting alerts? The /start command — what does it ask me?"
**Verdict:** ⚠️ Doesn't explain what the onboarding flow looks like. What preferences can you set?

### Chain Coverage
**Sees:** Ethereum, Base, Solana, Arbitrum, BSC, Polygon
**Thinks:** "These are the main ones. I use all of them. But I also farm on Optimism and Avalanche. The roadmap mentions those — when exactly?"
**Verdict:** ✅ Good core coverage. ⚠️ Roadmap says "Next up" for expanded chains but no timeline.

### Pricing
**Sees:** Free (3/day), Pro ($9.99 launch, grandfathered), Power ($29.99 coming soon)
**Thinks:** "3 alerts/day is nothing — I'd blow through that in an hour. Pro at $9.99 is reasonable. Grandfathered forever is a nice touch. But what does 'priority discovery' mean? And what's the difference between Pro alerts and Free alerts?"
**Verdict:** ⚠️ "Priority discovery" is undefined. ⚠️ No clear explanation of what changes between Free and Pro alerts (same pools? better scoring? more frequent?). ⚠️ No mention of how payment works (Telegram Stars vs other methods).

### Security Section
**Sees:** Non-custodial, GoPlus, Open source, Self-hostable
**Thinks:** "All good signals. Open source is important — I might actually audit the code. Self-hosting is a bonus."
**Verdict:** ✅ Strong for this persona.

### Moat Section
**Sees:** "I could build this in a weekend"
**Thinks:** "Honestly, I could build a basic DeFiLlama wrapper in a weekend. But the scoring model, historical data, and GoPlus integration — that's the real value."
**Verdict:** ✅ Honest framing. Addresses the "I could build this" objection head-on.

### Roadmap
**Sees:** Shipped, Next up, Planned, Future
**Thinks:** "OK, expanded chains are next. Yield collapse prediction would be amazing. But no timelines on anything."
**Verdict:** ⚠️ No dates or quarters on roadmap items. Hard to evaluate if this is actively maintained or a side project.

---

## Key Findings

### Critical Issues
1. **Scoring methodology not transparent enough** — Marcus needs weights/formula to trust the output
2. **No link from landing page to docs** — the docs page has the scoring table but there's no navigation link

### Moderate Issues
3. **"Priority discovery" undefined** — what does Pro actually give you that Free doesn't?
4. **No onboarding preview** — what does the /start flow look like? What can you configure?
5. **Static mockup data** — examples should be clearly labeled with dates or shown as live
6. **No Ethereum pool in mockups** — the largest chain by TVL should be represented
7. **No roadmap timelines** — "Next up" and "Planned" have no dates

### Minor Issues
8. **Blog is empty** — no content marketing for someone who'd read yield strategy posts
9. **No mention of digest vs alert frequency** — the Free tier says "daily digest" but it's unclear if Pro also gets digests
10. **Footer "MIT License"** — should link to the actual license file on GitHub

### What Works Well
- Hero resonates with DeFi natives
- Comparison table is honest and effective
- Moat section directly addresses the "I could build this" objection
- Non-custodial + open source signals
- Grandfathered pricing creates urgency

---

## Marcus's Unanswered Questions
- "What are the exact scoring weights? I want to understand the formula."
- "What does 'priority discovery' mean for Pro users?"
- "What can I configure in the onboarding flow?"
- "How many alerts does the average Pro user receive per day?"
- "Is the Free tier's 3-alert limit per pool or per day total?"
- "Can I set custom TVL minimums and risk thresholds on Free?"
- "When exactly are Optimism and Avalanche being added?"
- "What's the difference between a digest and an alert?"

## Recommendation
Link to docs from the landing page. Add a "How scoring works" expandable section or link. Clarify Pro vs Free differences beyond "unlimited." Add an Ethereum pool example to the mockups. Consider adding approximate timelines to roadmap items.
