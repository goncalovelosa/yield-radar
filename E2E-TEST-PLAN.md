# YieldRadar Landing Page — E2E Test Plan

**Version:** 1.0  
**Last Updated:** 2026-04-20  
**Scope:** https://yieldradar.io (all pages)  
**Environment:** Production (Hetzner) + Local dev (`npm run dev`)

---

## Test Infrastructure Setup

No test runner exists yet. Before executing, install:

```bash
# Link checker
npm install -D linkinator

# Lighthouse CI (performance + a11y + SEO)
npm install -D @lhci/cli

# HTML validator
npm install -D html-validate

# Accessibility
npm install -D axe-core @axe-core/playwright

# E2E browser tests
npm install -D @playwright/test
npx playwright install
```

---

## 1. Build & Deploy Validation

| # | Test Case | Steps | Expected Result |
|---|-----------|-------|-----------------|
| 1.1 | Clean build succeeds | `rm -rf dist && npm run build` | Exit code 0, no warnings |
| 1.2 | Build output is complete | `ls dist/` and check pages | `index.html`, `docs/index.html`, `learn/index.html`, `changelog/index.html`, `sitemap-index.xml` exist |
| 1.3 | No build errors or orphan assets | Review build output | Zero "orphan" or "missing" asset warnings |
| 1.4 | Static files are self-contained | Check dist/ has no server-side dependencies | All HTML/CSS/JS inline or referenced from dist/ |
| 1.5 | Production site is accessible | `curl -sI https://yieldradar.io` | HTTP 200, proper content-type |

---

## 2. Navigation & Link Integrity

| # | Test Case | Steps | Expected Result |
|---|-----------|-------|-----------------|
| 2.1 | All internal links resolve | `npx linkinator https://yieldradar.io --recurse --skip "^(?!https://yieldradar.io)"` | 0 broken links |
| 2.2 | External links are valid | Manual spot-check: Telegram bot link, DeFiLlama, any external refs | No 404s |
| 2.3 | Navigation menu links work | Click each nav item (Home, Docs, Learn, Changelog) | Correct page loads, active state shown |
| 2.4 | CTA buttons link correctly | Click "Open in Telegram" / pricing CTAs | Opens @YieldRadar_io_bot or correct destination |
| 2.5 | Sitemap is valid XML | Fetch `/sitemap-index.xml` | Valid XML, lists all 4 pages |
| 2.6 | robots.txt allows crawling | Fetch `/robots.txt` | Contains `Sitemap:` pointing to sitemap, no disallow for content pages |

---

## 3. SEO & Metadata

| # | Test Case | Steps | Expected Result |
|---|-----------|-------|-----------------|
| 3.1 | Title tags are present and unique | Check `<title>` on each page | Each page has unique, descriptive title containing "YieldRadar" |
| 3.2 | Meta descriptions exist | Check `<meta name="description">` on each page | 150-160 char descriptions, unique per page |
| 3.3 | Open Graph tags present | Check `<meta property="og:*">` | `og:title`, `og:description`, `og:image`, `og:url` on every page |
| 3.4 | OG image loads | Fetch the og:image URL | Returns 200, is a valid image (1200x630 recommended) |
| 3.5 | JSON-LD structured data | Check `<script type="application/ld+json">` | Valid JSON-LD with Organization/WebSite schema |
| 3.6 | Canonical URLs | Check `<link rel="canonical">` | Self-referencing canonical on each page |
| 3.7 | H1 heading per page | Each page has exactly one `<h1>` | Unique H1 describing page content |
| 3.8 | Heading hierarchy | Check h1→h2→h3 nesting | No skipped levels (e.g., h1→h3) |
| 3.9 | Lighthouse SEO score | `npx lhci collect --url=https://yieldradar.io` | Score ≥ 90 |

---

## 4. Theme Toggle (Light/Dark)

| # | Test Case | Steps | Expected Result |
|---|-----------|-------|-----------------|
| 4.1 | Default theme loads | Load page with no localStorage | Theme matches system preference (prefers-color-scheme) |
| 4.2 | Toggle switches theme | Click theme toggle button | All elements switch colors (bg, text, cards, borders) |
| 4.3 | Theme persists on reload | Toggle to dark → refresh page | Page loads in dark mode |
| 4.4 | Theme persists across pages | Set dark on home → navigate to docs | Docs page loads in dark mode |
| 4.5 | No FOUC (Flash of Unstyled Content) | Hard-refresh with throttled network | Theme applied before content renders (no white flash) |
| 4.6 | All elements themed | Check cards, buttons, links, code blocks, FAQ | No elements remain in wrong theme after toggle |

---

## 5. Responsive Design

| # | Test Case | Steps | Expected Result |
|---|-----------|-------|-----------------|
| 5.1 | Mobile (< 640px) | DevTools → iPhone SE viewport | Single column, nav collapses to hamburger, text readable, no horizontal scroll |
| 5.2 | Tablet (768px - 1024px) | DevTools → iPad viewport | 2-column pricing, proper spacing, no overflow |
| 5.3 | Desktop (1280px+) | Full-width browser | Full layout, all sections visible, proper whitespace |
| 5.4 | Large desktop (1920px+) | Full-width on large monitor | Content doesn't stretch too wide, max-width container respected |
| 5.5 | Touch targets (mobile) | Check all buttons/links on mobile | Minimum 44x44px tap targets |
| 5.6 | Font scaling | Set browser zoom to 200% | Layout doesn't break, text still readable |

---

## 6. Content Accuracy

| # | Test Case | Steps | Expected Result |
|---|-----------|-------|-----------------|
| 6.1 | Pricing tiers match bot | Compare site Free/Pro/Power tiers with bot subscription logic | Features, prices, limits are consistent |
| 6.2 | Supported chains listed correctly | Check chain list against DeFiLlama data | All 6 chains (Ethereum, BSC, Arbitrum, Polygon, Avalanche, Optimism) listed |
| 6.3 | FAQ answers are accurate | Read each FAQ item | Answers reflect actual bot behavior (verify against source code) |
| 6.4 | No placeholder/stale text | Search for "TODO", "placeholder", "coming soon" outside blog | No stale placeholder text on live pages |
| 6.5 | Changelog is current | Check changelog entries | Matches actual released features, latest version is v1.2 |
| 6.6 | Docs page formulas correct | Check risk scoring formula against bot source code | Formula in docs matches `risk-scoring/scorer/` implementation |
| 6.7 | Blog placeholder handled | Navigate to /blog | Shows "Coming soon" or similar, no 404 |
| 6.8 | Telegram bot link correct | Click "Open in Telegram" | Opens `https://t.me/YieldRadar_io_bot` |

---

## 7. Accessibility (a11y)

| # | Test Case | Steps | Expected Result |
|---|-----------|-------|-----------------|
| 7.1 | Lighthouse a11y score | `npx lhci collect` | Score ≥ 85 |
| 7.2 | axe-core automated audit | Run axe-core on each page | Zero critical/serious violations |
| 7.3 | All images have alt text | Check all `<img>` tags | Descriptive alt attribute on every image |
| 7.4 | Color contrast (light theme) | Check text on backgrounds | WCAG AA: 4.5:1 for normal text, 3:1 for large text |
| 7.5 | Color contrast (dark theme) | Check text on backgrounds | Same AA ratios met in dark mode |
| 7.6 | Keyboard navigation | Tab through entire page | Logical focus order, all interactive elements reachable |
| 7.7 | Skip to content link | Tab once on page load | Skip link appears and jumps to main content |
| 7.8 | Form elements labeled | If any forms exist (newsletter, etc.) | All inputs have associated labels |
| 7.9 | Focus indicators visible | Tab to buttons/links | Visible focus ring/outline on all interactive elements |

---

## 8. Performance

| # | Test Case | Steps | Expected Result |
|---|-----------|-------|-----------------|
| 8.1 | Lighthouse Performance | `npx lhci collect` | Score ≥ 90 |
| 8.2 | First Contentful Paint | Lighthouse audit | < 1.8s |
| 8.3 | Largest Contentful Paint | Lighthouse audit | < 2.5s |
| 8.4 | Cumulative Layout Shift | Lighthouse audit | < 0.1 |
| 8.5 | Total Blocking Time | Lighthouse audit | < 200ms |
| 8.6 | No render-blocking resources | Check network waterfall | CSS loaded without blocking, fonts use `display=swap` |
| 8.7 | Image optimization | Check all images | SVGs for icons, proper sizing, no oversized assets |
| 8.8 | Gzip/Brotli compression | `curl -sI -H "Accept-Encoding: br"` | `content-encoding: br` or `gzip` |

---

## 9. Cross-Browser Compatibility

| # | Test Case | Steps | Expected Result |
|---|-----------|-------|-----------------|
| 9.1 | Chrome (latest) | Load all pages | Full functionality, no console errors |
| 9.2 | Firefox (latest) | Load all pages | Full functionality, no console errors |
| 9.3 | Safari (latest) | Load all pages | Full functionality, no console errors |
| 9.4 | Edge (latest) | Load all pages | Full functionality, no console errors |
| 9.5 | Mobile Safari (iOS) | Load on iPhone | Responsive layout, theme toggle works |
| 9.6 | Chrome Android | Load on Android | Responsive layout, theme toggle works |

---

## 10. Security

| # | Test Case | Steps | Expected Result |
|---|-----------|-------|-----------------|
| 10.1 | No mixed content | Check all resources | Everything loads over HTTPS |
| 10.2 | Security headers present | `curl -sI https://yieldradar.io` | X-Frame-Options, X-Content-Type-Options, Referrer-Policy present |
| 10.3 | No sensitive data in HTML | View page source | No API keys, tokens, or internal URLs exposed |
| 10.4 | CSP headers | Check Content-Security-Policy | Restrictive CSP with appropriate allow-lists |

---

## Execution Checklist

```
Phase 1 — Smoke (5 min)
  [ ] 1.1 Clean build
  [ ] 1.5 Production accessible
  [ ] 2.1 Internal links

Phase 2 — Content & SEO (15 min)
  [ ] 3.1-3.9 All SEO checks
  [ ] 6.1-6.8 Content accuracy

Phase 3 — Visual & Interactive (15 min)
  [ ] 4.1-4.6 Theme toggle
  [ ] 5.1-5.6 Responsive design
  [ ] 7.1-7.9 Accessibility

Phase 4 — Performance & Security (10 min)
  [ ] 8.1-8.8 Performance
  [ ] 10.1-10.4 Security

Phase 5 — Cross-Browser (15 min)
  [ ] 9.1-9.6 Browser testing
```

**Estimated Total Time:** ~60 minutes

---

## Known Issues from Persona Critiques

These were identified in `docs/critiques/` — verify if resolved:

- [ ] Pricing section clarity (cross-persona issue)
- [ ] Hero section value proposition clarity
- [ ] Mobile navigation UX
- [ ] FAQ coverage completeness
- [ ] Social proof / trust signals

---

## Issues & Notes

*Log test results here as you execute:*

| Date | Test | Result | Notes |
|------|------|--------|-------|
| | | | |
