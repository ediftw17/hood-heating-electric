# Visual Review — Hood Heating Air Plumbing & Electric — 2026-04-10

---

## Desktop Review

### Critical Issues

- **Hero background is wrong photo:** `assets/scraped-02-reviews.jpg` is a stock photo of a woman adjusting a thermostat — not the scraped reviews screenshot the filename implies. The image itself is fine (warm, on-brand), but the file is named `scraped-02-reviews.jpg`, implying it was intended to be a reviews page screenshot used as hero background. This is confusing but renders acceptably. **More critically: the about section uses `scraped-01-team.jpg` (the actual Hood team photo) in the correct place, but the hero is a generic stock photo, not a Hood-specific asset.** For a pitch site this is acceptable, but should be noted — the client may recognize it's not their business. This is the single most critical fix if the intent was to use a scraped real photo as the hero. Fix: if no better asset exists, keep it. If the intent was to use the team van shot as hero, swap `assets/scraped-02-reviews.jpg` in the hero-bg CSS with `assets/scraped-01-team.jpg` and adjust `background-position`.

### High Severity

- **Services grid shows only 3 cards above fold (screenshot-services.png):** The section-services.png is cropped at the first row, showing only Heating, AC, and Plumbing. The bottom row (Electrical, Commercial Refrigeration, New Construction) is cut off and not visible in the section screenshot. This is a screenshot framing issue, not a layout bug — but in the desktop-1440-full.png you can see all 6 cards. However, there is a real issue: the Plumbing card image (`photo-1504328345606-18bbc8c9d7d1`) shows a close-up of a man welding/cutting metal with sparks, which reads more like fabrication or construction than plumbing. This is a wrong-image-for-service issue. Fix: Replace the plumbing card Unsplash image with a photo of a plumber at pipes/fixtures. Suggested URL swap: `https://images.unsplash.com/photo-1585771724684-38269d6639fd?w=800&q=80` (plumber working under sink) or any plumbing-specific photo.

- **Hero headline is not using mixed weight/italic treatment:** The H1 "One Call Covers It All" is all-bold, all white, same weight. There is no italic word, no accent-color word, no weight contrast between lines. For a serif Playfair Display headline this is a missed opportunity — the headline looks flat compared to what the font can do. Fix: Wrap "Covers" or "It All" in a `<em>` tag, or color "One Call" in `var(--amber)` to create visual hierarchy within the headline.

- **Hero content is center-aligned while CTA rule requires left-alignment under left-aligned text — but here it's consistently centered, which is fine as a design choice. However, there are two equal-weight CTAs:** "Call (785) 243-1489" (amber/primary) and "Schedule Service" (outline/white). They are close enough in visual weight that the primary action is not dominant. The call button is slightly more prominent due to the filled amber color, but the outline button at the same size competes. Fix: Reduce "Schedule Service" to a smaller ghost button (`font-size: 0.875rem`, reduced padding) to subordinate it visually.

### Medium Severity

- **About section: 50/50 grid split (section-about.png):** The about grid uses `1fr 1fr` — a perfectly symmetric split. The image side and text side get equal width. For a "trust and credibility" section, a 60/40 split favoring the text would give the copy more breathing room and feel more intentional. Fix: Change `.about-grid` to `grid-template-columns: 1fr 1.15fr` or `55fr 45fr`.

- **Testimonials: 5 cards in a 3-col grid leaves an orphaned row (section-testimonials.png):** 5 cards = 3 on row 1, 2 on row 2. The bottom-left card (Lacey) and bottom-center card (Suzie) leave the bottom-right cell empty. This is visible and slightly awkward. Fix: Either add a 6th review card to fill the grid, or switch to a 2+3 staggered layout, or reduce to 4 cards (2x2). Easiest fix: add one more review from their Google/Facebook corpus.

- **Trust strip between testimonials and contact is amber background with white text — this is a large amber section:** The trust strip spanning the full viewport in amber is a lot of orange. Per color usage guidelines, accent color should not be used as a background for large sections. At desktop it's about 80px tall so it's contained, but it draws very strong attention. Flag as polish: if you want to pull it back, use a light cream or navy background with amber accents instead.

- **Contact section: abundant blank space below the form (section-contact.png):** There's a large white/cream gap between the bottom of the map info card and the footer. The contact section has substantial padding at the bottom that leaves the section feeling unfinished. Fix: reduce `#contact .section` bottom padding, or add a brief "Emergency? Call us now" amber CTA strip before the footer to fill the space.

- **Footer copyright says "2025" — should be 2026** (section-footer.png, bottom bar reads "© 2025 Hood Heating Air Plumbing & Electric"). Fix: update to 2026 in the footer-bottom span.

### Passing

- Logo: ✓ White/inverted logo in nav reads clearly against dark nav background
- Nav: ✓ Business name, phone number, and CTA all visible at desktop
- Hero overlay: ✓ Linear gradient (80% top, 60% mid, 78% bottom) provides adequate text legibility — headline is clearly readable
- Hero text contrast: ✓ White text with 80%+ overlay at top where text sits — no legibility issue
- Trust bar: ✓ 4.3 Google, 80 Years, 24/7, A+ BBB — all visible below CTA
- About section photo: ✓ Real Hood team photo with branded vans — strong credibility signal
- About badge: ✓ "80 Years Serving Kansas" amber badge bottom-right of team photo — well placed
- Stats row in about: ✓ 4 stats (80 Years, 4th Gen, 24/7, 2 Locations) — clear and legible
- Testimonials: ✓ Dark navy background creates strong visual contrast from surrounding sections; amber stars, italic quote text, source badges all render well
- Service card images: ✓ Heating (technician with furnace), AC (outdoor unit), Electrical (panel work), Commercial Refrigeration (restaurant kitchen), Construction (framing site) — all appropriate
- Contact form: ✓ Full Name, Phone, Service dropdown, Message, Send Request button — complete and functional-looking
- Google Maps embed: ✓ Shows correct Concordia, KS location
- Footer: ✓ 4-col layout (brand, services, quick links, contact) — clean and well-organized
- Typography: ✓ Two fonts only — Playfair Display (serif, headings) and system sans-serif/Inter (body). No font sprawl.
- Animations: ✓ fade-up uses `opacity` + `transform` only — no `filter:blur` transitions. All transitions 0.55s or under. Safe for Safari.
- Service card hover: ✓ `translateY(-6px)` — subtle, not jarring. No scale transform used.
- Section breathing room: ✓ 96px section padding throughout — sections are well-spaced and do not run together

---

## Mobile Review (390px)

### Critical Issues

- **Services grid is single-column on mobile (mobile-services.png):** At 768px breakpoint the grid drops to `1fr` — single column. For 6 service cards this means a very long vertical scroll through the services section on mobile. Per checklist, minimum 2-col on mobile is expected. The single-column layout makes the section feel like a wall of content. Fix: Change the 768px breakpoint services-grid rule from `grid-template-columns: 1fr` to `grid-template-columns: repeat(2, 1fr)`. The card images at 200px height will still fit at 390px in 2 columns.

### High Severity

- **Footer logo appears duplicated on mobile (mobile-footer.png):** The sticky nav bar (pinned to top) shows the Hood logo, and immediately below it — because the footer section starts right there in the scroll position — the footer brand column also shows the Hood logo at the same size. On a 390px screen they stack within ~10px of each other and look like a copy-paste error. This is a visual artifact of the sticky nav + footer logo proximity. Fix: In the footer brand column, either reduce the footer logo height to 38px on mobile (`@media (max-width: 768px) { .footer-brand img { height: 38px; } }`) or visually separate by adding more padding-top to the footer, making it clear they are different elements.

- **Mobile sticky "Call" bar obscures bottom of the page at all times (mobile-hero.png, mobile-contact.png):** The amber sticky bar with "Call (785) 243-1489" is fixed to the bottom. On mobile-contact.png, the bottom of the form area (`Send Request` button) is very close to the sticky bar — the button appears just above it. The 56px body padding-bottom is meant to prevent this, but the sticky bar eats into the visible viewport. On mobile-contact.png the Google Maps "Open in Maps" button is partially obscured at the bottom. This is a z-index/overlap issue on the contact section's map area. Fix: Verify the contact section has sufficient `padding-bottom` on mobile (currently 72px section padding + 56px body padding = 128px total — should be enough, but the map panel clips at bottom). Ensure `#contact .section` has `padding-bottom: 80px` on mobile to keep map controls above the sticky bar.

### Medium Severity

- **Trust bar items stack vertically on 390px (mobile-hero.png):** At 480px breakpoint, `.trust-bar` changes to `flex-direction: column`. On the mobile hero this renders as a vertical list of 4 items (4.3 Google, 80 Years, 24/7, A+ BBB) stacked with thin dividers. It is readable but takes up significant vertical space below the CTA buttons. It pushes the first trust signal further from the headline. The items stack cleanly but could be tighter. Fix: Keep 2-per-row in a 2x2 grid instead of full column stack: `display: grid; grid-template-columns: 1fr 1fr; gap: 4px` at 480px. This maintains the same total height but groups trust items visually.

- **Mobile about section: stats row is 4-column at 768px but switches to 2-column at 480px (mobile-about.png shows partial view):** The `@media (max-width: 480px)` rule changes stats-row to `repeat(2, 1fr)`. At 390px the stats read fine in 2x2 grid. No critical issue but the `@media (max-width: 768px)` rule sets it to `repeat(4, 1fr)` — four stat boxes at 390px width means each box is about 80px wide which is very cramped. The 480px rule overrides this correctly. Verify at 390px it's showing 2x2 (it should be). This appears correct in code.

- **Mobile testimonials: single-column card list is long (mobile-testimonials.png):** 5 review cards stacked vertically — fine for readability but creates very long section. Consider limiting to 3 cards on mobile and showing a "See all 61 reviews" link. Not critical, but improves scrolling experience.

### Passing

- Hero headline: ✓ "One Call Covers It All" breaks cleanly across 3 lines at 390px — no mid-word breaks
- Hero CTA: ✓ Both CTA buttons visible above fold on mobile, full-width, well above the sticky call bar
- Mobile CTA sizing: ✓ Primary amber "Call" button is full-width-ish and well above 44px height (56px sticky bar + hero buttons ~48px)
- Sticky call bar: ✓ Amber, high-contrast, phone icon + number — excellent tap target (min-height: 56px)
- Nav mobile: ✓ Phone number hidden on mobile, replaced by hamburger menu — correct pattern (no full phone number text in nav)
- Text contrast mobile: ✓ Overlay sufficient on hero — headline readable
- No text overflow: ✓ No clipping or mid-word breaks on 390px observed
- About team photo: ✓ Stacks above text on mobile — image loads correctly, badge positioned bottom-right
- Services section header: ✓ Title wraps cleanly at 390px
- Contact form: ✓ Full-width inputs, full-width Send Request button, all touch targets adequate
- Footer nav links: ✓ Clean vertical list, adequate line height for tap targets

---

## Summary

- **Total issues: 10** (Critical: 1, High: 4, Medium: 5)

**Critical (1):**
- Hero background is a stock thermostat photo, not a Hood-branded asset — file naming is misleading

**High (4):**
- Plumbing card has wrong/off-topic image (welding/sparks instead of plumbing)
- Hero headline is flat all-bold, no mixed weight/italic treatment
- Two equal-weight CTAs in hero — primary action not dominant
- Mobile services grid is single-column (should be 2-col minimum)

**Medium (5):**
- Footer logo duplication effect on mobile
- About section is 50/50 grid (should be asymmetric)
- Testimonials has an orphaned card in bottom row (5 cards in 3-col grid)
- Trust bar stacks vertically on 390px instead of 2x2
- Footer copyright year says 2025 (should be 2026)

**Recommendation: FIX FIRST**

The plumbing image and mobile single-column services grid are the two fixes that most affect how polished this looks. The headline treatment and CTA hierarchy affect conversion. Fix those four before sending to the client.
