# QA Code Review — Hood Heating Air Plumbing & Electric
**File:** `projects/website-building-agency/clients/hood-heating-electric/index.html`
**Reviewer:** Code Reviewer Agent
**Date:** 2026-04-10

---

## Hard Requirements

### 1. `<html lang="en">` present
PASS ✓ — Line 1: `<html lang="en">`

### 2. Skip-to-content link present
PASS ✓ — Line 1372: `<a href="#main" class="skip-link">Skip to main content</a>`. CSS positions it off-screen at `top: -60px` and brings it into view on `:focus`. Correct implementation.

### 3. `<title>` contains business name
PASS ✓ — Line 5: `<title>Hood Heating Air Plumbing &amp; Electric | Concordia, KS</title>`

### 4. `meta description` present and non-empty
PASS ✓ — Line 6: present, 158 characters, includes business name, location, year, and a CTA hook.

### 5. `og:image` is an absolute URL
PASS ✓ — Line 12: `https://hood-heating-electric.nule.io/assets/scraped-02-reviews.jpg` — fully qualified. Width/height meta tags also present.

### 6. Canonical URL set
PASS ✓ — Line 7: `<link rel="canonical" href="https://hood-heating-electric.nule.io" />`

### 7. Schema.org LocalBusiness JSON-LD — name, telephone, address, aggregateRating
PASS ✓ — All four required fields present (lines 29, 32, 33–40, 47–51).

WARNING ⚠ — Line 46: `"openingSpec"` is not a valid Schema.org property. The correct key is `"openingHoursSpecification"` (structured) or `"openingHours"` (text string). This field will be silently ignored by all validators and search engines. Low impact but should be fixed.

### 8. All `<img>` tags have non-empty, descriptive alt text
PASS ✓ — All images checked:
- Logo (nav): `"Hood Heating Air Plumbing &amp; Electric logo"` ✓
- Hero bg: handled via `role="img"` with `aria-label` on the div ✓
- Team photo: descriptive alt with headcount and context ✓
- 6 service card images: each has specific alt describing content ✓
- Footer logo: `"Hood Heating Air Plumbing and Electric logo"` ✓

No blank or "image" alt values found.

### 9. All phone links use `href="tel:+17852431489"`
PASS ✓ — All six phone link occurrences use the correct `tel:+17852431489` format (lines 1382, 1400, 1430, 1580, 1809, 1881, 1896, 1932).

### 10. No `href="#"` on any visible link
PASS ✓ — No `href="#"` found anywhere in the document.

### 11. No fake/dead Privacy Policy or Accessibility links
PASS ✓ — The footer legal area (lines 1919–1922) contains only plain `<span>` elements ("Licensed & Insured", "Est. 1946"), not hyperlinks. No dead policy links present.

### 12. "Built by nule.io" in footer as a working hyperlink
PASS ✓ — Line 1917: `Built by <a href="https://nule.io" target="_blank" rel="noopener noreferrer">nule.io</a>.` — correct URL, opens in new tab, noopener present.

### 13. Google Maps iframe present with valid embed URL
PASS ✓ — Lines 1781–1788: iframe present, `src` uses `https://www.google.com/maps/embed?pb=...`, has `title` attribute, `allowfullscreen`, and `loading="lazy"`.

WARNING ⚠ — The embed URL uses `!1s0x0%3A0x0` as the place ID, which is a null/placeholder place ID. The map will render a generic pin at the lat/long coordinates rather than resolving to the verified business listing. Replace with the real Google Maps place embed URL (get it from Google Maps > Share > Embed a map with the business selected).

### 14. Form has `<label>` elements associated with every input
PASS ✓ — All four form fields (name, phone, service, message) have explicit `<label for="...">` matched to the corresponding `id` on each input. Correct for/id pairing throughout.

### 15. Mobile sticky bottom CTA bar — present, hidden on desktop
PASS ✓ — `#sticky-call` is declared `display: none` in base styles (line 1159), then `display: block` is applied inside `@media (max-width: 768px)` (line 1322). Correct approach — desktop never sees it.

---

## Accessibility

### Form inputs have associated labels (for/id pairing)
PASS ✓ — All four inputs: `form-name`, `form-phone`, `form-service`, `form-message` — each has a matching `<label for="...">`.

### Navigation has `<nav>` with aria-label
WARNING ⚠ — The desktop nav is wrapped in `<header id="navbar" role="banner">` (line 1391) but there is no `<nav>` element inside it. The desktop navigation links are not wrapped in a `<nav>` landmark at all. The mobile overlay has a `<nav class="mobile-menu-links">` (line 1376) but it lacks an `aria-label`. Screen readers expect a `<nav aria-label="Primary">` for the main navigation.

Fix: Wrap the desktop nav links area in `<nav aria-label="Primary">`, and add `aria-label="Primary"` to the mobile `<nav>`.

### Main content wrapped in `<main id="main">`
PASS ✓ — Line 1419: `<main id="main">`. The skip-link target matches.

### Headings in logical order
PASS ✓ — One `<h1>` (hero, line 1427). H2s for each section (services, about, testimonials, contact — lines 1454, 1558, 1593, 1711). H3s used for service card titles and nothing deeper. No heading levels skipped.

### Icon-only buttons have aria-label
PASS ✓ — The hamburger button (line 1408) has `aria-label="Open navigation menu"`, `aria-expanded="false"`, and `aria-controls="mobile-menu"`. The JS updates `aria-label` and `aria-expanded` on toggle.

### Color contrast — amber #E8881A on white/cream backgrounds
WARNING ⚠ — The `.eyebrow` class (lines 148–151) applies `color: var(--amber)` (`#E8881A`) on `var(--cream)` (`#F7F3EE`) in the services and about sections. Computed contrast ratio for #E8881A on #F7F3EE is approximately 3.0:1, which fails WCAG AA (requires 4.5:1 for normal text). The eyebrow text is 0.75rem/12px, which makes this a normal-text contrast requirement, not the relaxed large-text threshold.

This is body/label-level text used repeatedly as section labels. It fails AA for normal text. Switch amber eyebrow text in cream-background sections to a darker tone — `#C96F0A` (`--amber-dark`) achieves approximately 4.6:1 on cream and passes AA.

### Touch targets — mobile CTA bar and hamburger
PASS ✓ — Hamburger button: `width: 44px; height: 44px` (line 296). Sticky call bar link: `min-height: 56px; width: 100%` (line 1178–1179). Both meet the 44x44px minimum.

---

## Mobile-Specific

### Hamburger menu JS — literal hex color in overlay code?
PASS ✓ — The mobile menu overlay uses `background: #0D2240` in CSS (line 327), not injected via JavaScript. The JS only toggles classes; it never sets inline styles or hardcodes colors. No hex literals in the script block.

### `display:none` / media query to hide sticky bar on desktop
PASS ✓ — `display: none` in base styles, activated only inside `@media (max-width: 768px)`. Desktop never renders the bar.

### Hero height: `100svh` or `100vh`
PASS ✓ — Line 382: `min-height: 100svh`. Uses the modern `svh` unit which accounts for mobile browser chrome (address bar). Correct.

---

## Copyright Year

FAIL ✗ — Line 1916: `&copy; 2025 Hood Heating Air Plumbing &amp; Electric.`

The year reads **2025**. Should be **2026**. Clients and their customers will notice this immediately as a signal that the site is outdated.

---

## Summary of Findings

**Total: 1 FAIL, 4 WARNINGs, all other items PASS**

### Top 3 fixes by priority

**1. FAIL — Copyright year is 2025 (line 1916)**
Change `&copy; 2025` to `&copy; 2026`. This is the most visible issue — any user who scrolls to the footer sees a site that appears to be from last year. One-character fix.

**2. WARNING — Amber eyebrow text on cream background fails WCAG AA contrast (lines 148–151 and all eyebrow usages in cream sections)**
`#E8881A` on `#F7F3EE` is approximately 3.0:1. Fails for normal text. Change the CSS variable or override for sections with cream backgrounds to use `--amber-dark` (`#C96F0A`), which passes at ~4.6:1. Affects every eyebrow label on the services and about sections. Real accessibility impact.

**3. WARNING — Google Maps embed uses null place ID (`0x0:0x0`) (line 1783)**
The map renders by lat/long only, not linked to the verified business listing. This means the pin will not show the business name, reviews, or "Get Directions" link inside the embed. Replace with the real embed URL from Google Maps (share > embed, with the actual listing selected). Minor UX impact but undermines the trust signal the map is intended to provide.

**Lower priority (non-blocking):**
- Desktop nav links not wrapped in a `<nav>` landmark (accessibility, screen reader navigation)
- Schema `"openingSpec"` is not a valid property — should be `"openingHours"` (SEO, no user-visible impact)
