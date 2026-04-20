# YieldRadar Landing Page — E2E Test Plan

**Version:** 1.1  
**Last Updated:** 2026-04-20 (session 2)  
**Scope:** https://yieldradar.io (all pages)  
**Environment:** Production (Hetzner) + Local dev (`npm run dev`) + Tailscale for remote access

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
| 1.5 | **Logo assets exist** | Check `public/` | `logo.svg` (nav logo), `favicon.svg`, `favicon.ico` (16/32/64px) all present |
| 1.6 | Production site is accessible | `curl -sI https://yieldradar.io` | HTTP 200, proper content-type |

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

## 5. Responsive Design & Layout

| # | Test Case | Steps | Expected Result |
|---|-----------|-------|-----------------|
| 5.1 | Mobile (< 640px) | DevTools → iPhone SE viewport | Single column, nav collapses to hamburger, text readable, no horizontal scroll |
| 5.2 | Tablet (768px - 1024px) | DevTools → iPad viewport | 2-column pricing, 2-col stats grid, proper spacing, no overflow |
| 5.3 | Desktop (1280px+) | Full-width browser | Full layout, all sections visible, proper whitespace |
| 5.4 | Large desktop (1920px+) | Full-width on large monitor | Content doesn't stretch too wide, max-width container respected |
| 5.5 | Touch targets (mobile) | Check all buttons/links on mobile | Minimum 44x44px tap targets |
| 5.6 | Font scaling | Set browser zoom to 200% | Layout doesn't break, text still readable |
| 5.7 | **Stats grid layout** | View "By the numbers" section | 4 cards top row + 4 cards bottom row, evenly aligned |
| 5.8 | **Stats grid — mobile** | Resize to <768px | Stats grid collapses to 2 columns |
| 5.9 | **Pipeline boxes equal height** | View "How it works" section | All 4 pipeline boxes are same height (tallest wins), arrows vertically centered |
| 5.10 | **Pipeline — mobile vertical** | Resize to <768px | Pipeline stacks vertically, arrows hidden |
| 5.11 | **FAQ full-width left-aligned** | View FAQ section | FAQ items span full content width, left-aligned (no centering) |
| 5.12 | **Docs architecture pipeline** | Navigate to /docs → Architecture | All 5 steps in single horizontal row, no wrapping |

---

## 6. Content Accuracy

| # | Test Case | Steps | Expected Result |
|---|-----------|-------|-----------------|
| 6.1 | Pricing tiers match bot | Compare site Free/Pro/Power tiers with bot subscription logic | Features, prices, limits are consistent |
| 6.2 | Supported chains listed correctly | Check chain list against DeFiLlama data | All 10 chains listed: Ethereum, Base, Solana, Arbitrum, BSC, Polygon, Optimism, Avalanche, Hyperliquid L1, Sui |
| 6.3 | FAQ answers are accurate | Read each FAQ item | Answers reflect actual bot behavior (verify against source code) |
| 6.4 | No placeholder/stale text | Search for "TODO", "placeholder", "coming soon" outside blog | No stale placeholder text on live pages |
| 6.5 | Changelog is current | Check changelog entries | Matches actual released features, latest version is v1.2 |
| 6.6 | Docs page formulas correct | Check risk scoring formula against bot source code | Formula in docs matches `risk-scoring/scorer/` implementation |
| 6.7 | Blog placeholder handled | Navigate to /blog | Shows "Coming soon" or similar, no 404 |
| 6.8 | Telegram bot link correct | Click "Open in Telegram" | Opens `https://t.me/YieldRadar_io_bot` |
| 6.9 | **Nav logo renders** | View top-left of any page | Radar + yield arrow SVG logo visible, links to / |
| 6.10 | **Favicon loads** | Check browser tab icon | Radar logo favicon visible (not default Astro icon) |

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
| 7.10 | **Decorative SVGs hidden** | Inspect all `<svg>` elements in index.astro | All 12 decorative SVGs have `aria-hidden="true"` (4 pipeline + 4 security + 4 moat icons) |
| 7.11 | **Nav logo accessible** | Inspect nav logo `<a>` tag | Has `aria-label="YieldRadar home"` |
| 7.12 | **Methodology links labeled** | Check all 3 "See the full methodology →" links | Each has `aria-label="Read the full risk scoring methodology"` |
| 7.13 | **No empty anchors/headings** | Run Lighthouse a11y audit on / | Zero "Headings and anchors must have accessible name" violations |

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

- [x] ~~Pricing section clarity~~ — restructured with Free/Pro cards
- [ ] Hero section value proposition clarity
- [ ] Mobile navigation UX
- [x] ~~FAQ coverage completeness~~ — 11 FAQ items covering all major topics
- [ ] Social proof / trust signals

## Changes Since v1.0 (Session 2)

- **Logo:** Replaced generic crosshair SVG with custom radar + yield arrow logo (`public/logo.svg`)
- **Favicon:** Updated `favicon.svg` and `favicon.ico` (16/32/64px) to match new logo
- **A11y:** Added `aria-hidden="true"` to 12 decorative SVGs, `aria-label` to nav logo and 3 methodology links
- **Stats grid:** Changed from `auto-fit` (5+3 layout) to fixed `repeat(4, 1fr)` (4+4 layout), 2-col on mobile
- **Pipeline boxes:** Equal height via `align-items: stretch`, arrows vertically centered
- **FAQ alignment:** Removed max-width, now full-width left-aligned
- **Docs pipeline:** Scoped override forces single-row horizontal layout on /docs Architecture section

---

## Issues & Notes

*Log test results here as you execute:*

| Date | Test | Result | Notes |
|------|------|--------|-------|
| | | | |
