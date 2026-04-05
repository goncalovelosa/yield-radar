# Persona 3: The Security-First Whale

**Name:** Viktor (41, fund manager, Zurich)
**Capital:** $800K+ across DeFi, predominantly blue-chip protocols (Aave, Lido, MakerDAO)
**Experience:** 4 years DeFi, reads audit reports, understands governance, multisig, smart contract risk
**Risk Tolerance:** Low-Moderate — capital preservation first, yield optimization second
**Telegram:** Moderate — uses it for alerts but prefers comprehensive dashboards
**Current spend:** Nansen $69/mo, Token Terminal $350/mo, DeBank Pro

---

## Journey Simulation

### Hero Section
**Sees:** "18,632 yield pools on DeFiLlama. Most of them will lose you money."
**Thinks:** "Hyperbolic but not wrong. However, 'most' is vague — what percentage? And 'lose you money' conflates IL with actual loss. A professional tool should be more precise."
**Verdict:** ⚠️ Too marketing-heavy. Viktor respects data, not hyperbole.

### The Problem Section
**Sees:** "DeFi has thousands of yield opportunities across dozens of chains."
**Thinks:** "I know. I already spend time on this. What's your actual differentiator beyond 'we push to Telegram'?"
**Verdict:** ⚠️ Problem statement is generic. Every yield tool says this. Needs more specific differentiation.

### How It Works
**Sees:** 6-factor scoring model
**Thinks:** "6 factors is a start. But what about: audit recency, admin key risk, timelock status, governance participation, TVL concentration, oracle dependency, bridge risk? 6 factors is surface-level for someone managing $800K."
**Verdict:** ❌ The scoring model is too simplistic for whale-tier users. Missing critical risk dimensions.

### Risk Scoring Section
**Sees:** 4 tiers with score ranges
**Thinks:** "A single 0-100 score for a pool is a reductionist approach. I need multi-dimensional risk assessment. A pool could score 80 overall but have a critical governance risk that gets masked."
**Verdict:** ❌ Single composite score hides important nuance. Viktor needs to see individual factor breakdowns.

### GoPlus Integration
**Sees:** "Every token is scanned for honeypot patterns, malicious contracts, and high-tax mechanisms."
**Thinks:** "GoPlus is a good start but it's an automated scanner with known blind spots. It misses sophisticated exploits. What about SpookySwap, where GoPlus gave passing grades before the exploit? What's the supplementary analysis?"
**Verdict:** ⚠️ Over-reliance on GoPlus without acknowledging its limitations. Should mention it as one layer, not the whole security story.

### Protocol-Level Intelligence
**Sees:** "TVL, audit status, protocol age"
**Thinks:** "What audits? By whom? Trail of Bits? OpenZeppelin? Certora? An 'audited' badge means nothing without knowing the auditor and scope. Protocol age is also not a reliable safety signal — many exploited protocols were 1+ years old."
**Verdict:** ❌ "Audit status" is dangerously vague. An exploited protocol could have an "audited" badge from a no-name auditor.

### Pricing
**Sees:** Pro $9.99/mo, Power $29.99/mo
**Thinks:** "$9.99 is suspiciously cheap. Nansen charges $69/mo and provides a fraction of what I need. At this price point, the depth of analysis can't be meaningful. The Power tier at $29.99 with 'yield collapse prediction' — using what model? Trained on what data? What's the precision/recall?"
**Verdict:** ❌ Pricing signals low-quality product to whale users. Too cheap to trust with $800K decisions. No mention of methodology validation.

### Security Section
**Sees:** Non-custodial, GoPlus, Open source, Self-hostable
**Thinks:** "Open source is the strongest signal here. I can audit the code myself. Self-hosting means I can run it with my own API keys. That's genuinely valuable."
**Verdict:** ✅ Open source + self-hostable are the only things that earn Viktor's trust.

### Roadmap
**Sees:** REKT database integration, social sentiment, API access
**Thinks:** "REKT database is useful — that's actual exploit history. API access is essential for my workflow — I'd pull this into my own dashboard. Social sentiment is noise for my use case."
**Verdict:** ✅ REKT database and API access are the right features for this persona. ⚠️ No timeline.

---

## Key Findings

### Critical Issues
1. **Scoring too simplistic for whale users** — single 0-100 score masks critical risk dimensions
2. **Pricing too cheap = perceived low quality** — $9.99 signals "toy" not "tool"
3. **"Audit status" dangerously vague** — doesn't specify auditor, scope, or recency
4. **Missing critical risk factors** — admin keys, timelock, oracle risk, bridge risk, governance

### Moderate Issues
5. **GoPlus presented as definitive** — should acknowledge limitations
6. **No methodology validation** — no backtesting data, no historical accuracy stats
7. **No API access at launch** — whales need to integrate into their own systems
8. **No enterprise/whale tier** — no volume-based pricing or custom features

### Minor Issues
9. **"Moat" section is unconvincing** — "months of APY snapshots" isn't a moat
10. **No mention of data freshness** — how stale can data be before alerts are suppressed?
11. **Blog empty** — no thought leadership content to establish credibility

### What Works Well
- Open source (genuinely the strongest signal for this persona)
- Self-hostable (Viktor could run his own instance)
- Non-custodial (mandatory for whale trust)
- REKT database on roadmap (right direction)

---

## Viktor's Unanswered Questions
- "What's the scoring formula? Can I see individual factor scores, not just a composite?"
- "Which auditors do you check? Trail of Bits? OpenZeppelin? How do you verify audit scope?"
- "What's the false positive/negative rate on GoPlus security scans?"
- "Do you track admin key changes, timelock modifications, or governance proposals?"
- "How do you handle bridge risk for cross-chain pools?"
- "When will API access be available? What's the rate limit?"
- "Can I self-host and use my own GoPlus/API keys?"
- "What's the precision/recall of your 'yield collapse prediction' model?"
- "Why is this $9.99/mo when inferior tools charge $50+?"

## Recommendation
This persona is NOT the target market for v1 — and that's fine. But the landing page should still not alienate them. Consider: adding a methodology section, specifying auditor verification, and acknowledging GoPlus limitations. The Power tier at $29.99 is still too cheap for whale trust — consider adding an "Institutional" tier or positioning Power as "Advanced" with proper methodology documentation.
