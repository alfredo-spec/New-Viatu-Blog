# QA Testing Schedule — Viatu Blog Mockups & Components

Last updated: 2026-02-26

---

## Scope

| Category | Items |
|---|---|
| **Active mockups** | `blog-v10-master.html`, `blog-v10-master-staging.html`, `blog-v10-destinations-editorial.html`, `blog-v10-peek-fold.html`, `blog-v10-scroll-indicator.html` |
| **Vue components** | `BlogNav.vue`, `LangToggle.vue`, `PlaceholderImage.vue` |
| **Archived mockups** | 19 files in `design/mockups/archive/` (spot-check only) |

---

## 1. Browser Matrix

Test every active mockup and component in the following browsers. Mark each cell Pass / Fail / Partial.

| Browser | Version | Engine | Priority |
|---|---|---|---|
| Chrome (macOS) | Latest stable | Blink | P0 |
| Safari (macOS) | Latest stable | WebKit | P0 |
| Firefox (macOS) | Latest stable | Gecko | P1 |
| Edge (Windows) | Latest stable | Blink | P1 |
| Chrome (Android) | Latest stable | Blink | P0 |
| Safari (iOS) | Latest stable | WebKit | P0 |
| Samsung Internet | Latest stable | Blink | P2 |

### Browser-specific checks

| Check | Why | Browsers |
|---|---|---|
| `svh` / `dvh` units | Hero height uses `100svh` | Safari iOS, Chrome Android |
| `backdrop-filter: blur()` | Nav bar, scroll indicator | Firefox (verify support) |
| CSS `aspect-ratio` | PlaceholderImage component | All |
| Sticky positioning (`position: sticky`) | Browse bar, nav | Safari (known quirks) |
| `translate` property (non-transform) | Scroll indicator bounce | Firefox, Safari |
| SVG `stroke` rendering | All icons throughout | All |
| Font rendering / antialiasing | Lora + sans-serif stack | Safari vs Chrome |
| Smooth scroll (`scroll-behavior`) | Anchor links | Safari (partial support) |

---

## 2. Viewport & Device Format Matrix

Test at these exact dimensions. Use browser DevTools device mode + real devices where available.

### Desktop

| Viewport | Represents | Priority |
|---|---|---|
| 1920 x 1080 | Full HD monitor | P0 |
| 1440 x 900 | MacBook Pro 15" | P0 |
| 1280 x 800 | MacBook Air 13" | P1 |
| 2560 x 1440 | QHD / large external | P2 |

### Tablet

| Viewport | Represents | Priority |
|---|---|---|
| 1024 x 768 | iPad (landscape) | P0 |
| 768 x 1024 | iPad (portrait) | P0 |
| 820 x 1180 | iPad Air (portrait) | P1 |
| 1194 x 834 | iPad Pro 11" (landscape) | P1 |

### Mobile

| Viewport | Represents | Priority |
|---|---|---|
| 390 x 844 | iPhone 14 | P0 |
| 375 x 667 | iPhone SE / small phones | P0 |
| 412 x 915 | Pixel 7 / large Android | P1 |
| 360 x 780 | Galaxy S21 | P1 |
| 320 x 568 | iPhone SE 1st gen (minimum) | P2 |

---

## 3. Section-by-Section Visual Checks

For each mockup, verify every section passes at desktop, tablet, and mobile widths.

### 3A. Navigation

| # | Check | Breakpoints | Pass/Fail |
|---|---|---|---|
| 3A-1 | Logo renders and is correctly sized | All | |
| 3A-2 | Nav links are visible and properly spaced on desktop | >= 1024px | |
| 3A-3 | Nav collapses / hides gracefully on mobile | < 768px | |
| 3A-4 | "Back to homepage" CTA button visible and clickable | All | |
| 3A-5 | Search icon present and tappable (44px minimum target) | All | |
| 3A-6 | Nav becomes opaque/blurred on scroll (`scrolled` class) | All | |
| 3A-7 | Nav z-index sits above all content when scrolled | All | |

### 3B. Language Toggle

| # | Check | Breakpoints | Pass/Fail |
|---|---|---|---|
| 3B-1 | Globe icon + "EN" label visible | All | |
| 3B-2 | Dropdown opens on click, closes on outside click | All | |
| 3B-3 | Dropdown closes on Escape key | Desktop | |
| 3B-4 | Active language shows checkmark | All | |
| 3B-5 | Switching language updates the label text | All | |
| 3B-6 | Dropdown doesn't overflow viewport on mobile | < 480px | |
| 3B-7 | `aria-expanded` toggles correctly | All | |

### 3C. Hero Section

| # | Check | Breakpoints | Pass/Fail |
|---|---|---|---|
| 3C-1 | Hero image loads and covers full width | All | |
| 3C-2 | Gradient overlay is visible (text readable over image) | All | |
| 3C-3 | Category tag ("GUIDE") visible | All | |
| 3C-4 | Title renders in display font, no overflow/clipping | All | |
| 3C-5 | Subtitle / deck text wraps cleanly | All | |
| 3C-6 | Author avatar + byline visible | All | |
| 3C-7 | Read time shown with correct formatting | All | |
| 3C-8 | Hero height allows content peek below fold (peek-fold variant) | All | |
| 3C-9 | Scroll indicator renders as subtle round circle (scroll-indicator variant) | All | |
| 3C-10 | Scroll indicator fades out after 120px scroll | All | |
| 3C-11 | Scroll indicator bounces gently (not distracting) | All | |

### 3D. Sticky Browse Bar

| # | Check | Breakpoints | Pass/Fail |
|---|---|---|---|
| 3D-1 | Browse bar sticks below nav on scroll | All | |
| 3D-2 | Category pills are horizontally scrollable on mobile | < 768px | |
| 3D-3 | Active pill highlights on scroll (correct section tracked) | All | |
| 3D-4 | Clicking a pill smooth-scrolls to the correct section | All | |
| 3D-5 | Offset accounts for stacked sticky heights (nav + browse bar) | All | |
| 3D-6 | No visual gap between nav and browse bar when both sticky | All | |

### 3E. Content Sections (Featured, Destinations, Experiences, Guides, Travel Styles, Comparisons)

| # | Check | Breakpoints | Pass/Fail |
|---|---|---|---|
| 3E-1 | Section heading + "All [category]" link layout | All | |
| 3E-2 | Card grid: 3 columns desktop, 2 tablet, 1 mobile | All | |
| 3E-3 | Card images load, maintain aspect ratio, no distortion | All | |
| 3E-4 | Card text doesn't overflow card boundaries | All | |
| 3E-5 | Destination cards: gradient overlay, name + description visible | All | |
| 3E-6 | Experience tiles: 4-column grid collapses to 2 on mobile | All | |
| 3E-7 | Editorial split (Guides): image left, text right on desktop | >= 768px | |
| 3E-8 | Editorial split stacks vertically on mobile | < 768px | |
| 3E-9 | Comparison triptych: 3 panels side-by-side on desktop | >= 768px | |
| 3E-10 | Comparison triptych stacks or scrolls on mobile | < 768px | |
| 3E-11 | Reveal-on-scroll animations fire for each section | All | |

### 3F. Spread / Full-width Breaks

| # | Check | Breakpoints | Pass/Fail |
|---|---|---|---|
| 3F-1 | Background image covers full viewport width | All | |
| 3F-2 | Text content is readable over gradient | All | |
| 3F-3 | CTA link is visible and clickable | All | |
| 3F-4 | Parallax / scale effect (if present) runs smoothly | Desktop | |

### 3G. Expert Section

| # | Check | Breakpoints | Pass/Fail |
|---|---|---|---|
| 3G-1 | Portrait photo renders in circle/rounded container | All | |
| 3G-2 | Stats row (Safari count, Countries, Articles) lays out evenly | >= 768px | |
| 3G-3 | Stats stack or wrap on mobile | < 768px | |
| 3G-4 | Pull quote renders with decorative quotation mark | All | |
| 3G-5 | "Read articles" link is clickable | All | |

### 3H. Footer

| # | Check | Breakpoints | Pass/Fail |
|---|---|---|---|
| 3H-1 | Footer columns: 4 across on desktop, stacked on mobile | All | |
| 3H-2 | Social icons render (SVG strokes visible) | All | |
| 3H-3 | B Corp badge visible and properly styled | All | |
| 3H-4 | Bottom bar: logo + copyright on single line | All | |
| 3H-5 | Footer links are clickable (44px touch targets on mobile) | < 768px | |

---

## 4. Interaction & Usability Scenarios

### 4A. Scrolling Behaviour

| # | Scenario | Expected | Pass/Fail |
|---|---|---|---|
| 4A-1 | Load page — hero visible, browse bar peeks below (peek-fold) | Browse bar pills partially visible at bottom of viewport | |
| 4A-2 | Scroll down slowly | Nav goes opaque, browse bar sticks, sections reveal in sequence | |
| 4A-3 | Scroll quickly to bottom | No visual glitches, all reveal animations still fire | |
| 4A-4 | Scroll back to top | Active pill returns to "All", nav returns to transparent | |
| 4A-5 | Click anchor pill in browse bar | Smooth scroll to section with correct offset | |
| 4A-6 | Rapid-click multiple pills | No scroll conflict, last click wins | |
| 4A-7 | iOS rubber-band overscroll at top | Hero image doesn't leave ugly gap | |
| 4A-8 | iOS rubber-band overscroll at bottom | Footer doesn't detach from page | |

### 4B. Touch & Gesture (Mobile / Tablet)

| # | Scenario | Expected | Pass/Fail |
|---|---|---|---|
| 4B-1 | Swipe horizontally on browse bar pills | Pills scroll, no page-level horizontal scroll | |
| 4B-2 | Tap card | Card hover state activates, navigates correctly | |
| 4B-3 | Tap language toggle | Dropdown opens cleanly above/below trigger | |
| 4B-4 | Tap outside language dropdown | Dropdown closes | |
| 4B-5 | Long-press on image | Native context menu, no broken preview | |
| 4B-6 | Pinch-to-zoom | Page zooms cleanly (no fixed-width breakage) | |
| 4B-7 | Orientation change (portrait to landscape) | Layout reflows without overlap or gaps | |
| 4B-8 | Tap scroll indicator circle | Smooth scrolls to browse bar | |

### 4C. Keyboard Navigation (Desktop)

| # | Scenario | Expected | Pass/Fail |
|---|---|---|---|
| 4C-1 | Tab through all interactive elements | Logical tab order: nav links, CTA, lang toggle, browse pills, cards, footer links | |
| 4C-2 | Focus visible on all focusable elements | Clear focus ring / outline visible | |
| 4C-3 | Enter / Space on card | Navigates (acts as link click) | |
| 4C-4 | Escape on language dropdown | Closes dropdown | |
| 4C-5 | Tab into and through browse pills | All pills focusable, active state visible | |

### 4D. Hover States (Desktop)

| # | Scenario | Expected | Pass/Fail |
|---|---|---|---|
| 4D-1 | Hover over article card | Image scales up slightly, subtle shadow transition | |
| 4D-2 | Hover over destination card | Overlay lightens, CTA becomes more prominent | |
| 4D-3 | Hover over experience tile | Gradient shifts, label more visible | |
| 4D-4 | Hover over "All articles" link | Arrow shifts right, underline or color change | |
| 4D-5 | Hover over scroll indicator circle | Background slightly more opaque, border brightens | |
| 4D-6 | Hover over browse pill | Pill background/border change | |
| 4D-7 | Hover over footer link | Color or underline change | |

---

## 5. Performance Checks

| # | Check | Target | Tool |
|---|---|---|---|
| 5-1 | Largest Contentful Paint (LCP) | < 2.5s | Lighthouse / Chrome DevTools |
| 5-2 | Cumulative Layout Shift (CLS) | < 0.1 | Lighthouse |
| 5-3 | Total page weight (images + HTML + CSS) | < 5 MB | DevTools Network tab |
| 5-4 | Image formats optimised (JPEG, WebP, or AVIF) | No uncompressed PNGs for photos | Manual check |
| 5-5 | No broken image requests (404s) | Zero | DevTools Console + Network |
| 5-6 | Smooth scroll performance (no jank) | 60 fps during scroll | DevTools Performance tab |
| 5-7 | IntersectionObserver reveal doesn't cause reflows | No layout thrashing | Performance profiler |
| 5-8 | Sticky positioning doesn't cause paint storms | Minimal repaint area | Layers panel |

---

## 6. Accessibility Audit

| # | Check | Standard | Tool |
|---|---|---|---|
| 6-1 | Color contrast (text over images, gradients) | WCAG AA (4.5:1 normal, 3:1 large) | axe / Lighthouse |
| 6-2 | Color contrast (UI elements: pills, tags, meta text) | WCAG AA | axe |
| 6-3 | All images have descriptive `alt` text | WCAG 1.1.1 | Manual |
| 6-4 | Decorative images marked `alt=""` or `role="presentation"` | WCAG 1.1.1 | Manual |
| 6-5 | Heading hierarchy (`h1` > `h2` > `h3`, no skips) | WCAG 1.3.1 | axe / HeadingsMap |
| 6-6 | Interactive elements have accessible names | WCAG 4.1.2 | axe |
| 6-7 | Touch targets >= 44x44px | WCAG 2.5.8 | Manual measurement |
| 6-8 | No horizontal scroll at any breakpoint | WCAG 1.4.10 | Manual resize |
| 6-9 | Content reflows at 400% zoom | WCAG 1.4.10 | Browser zoom |
| 6-10 | Animations respect `prefers-reduced-motion` | WCAG 2.3.3 | Toggle in DevTools |
| 6-11 | Language dropdown keyboard-operable | WCAG 2.1.1 | Manual |
| 6-12 | Skip-to-content link present | WCAG 2.4.1 | Tab from top of page |
| 6-13 | Landmark roles present (`<nav>`, `<main>`, `<footer>`) | WCAG 1.3.1 | axe |

---

## 7. Visual Regression / Design Fidelity

| # | Check | Method |
|---|---|---|
| 7-1 | Typography matches style guide (Lora for headings, system sans for body) | Compare to `/design/style-guides/` |
| 7-2 | Spacing scale consistent (no arbitrary gaps) | Measure with DevTools |
| 7-3 | Color palette matches design tokens | Compare hex values to `tailwind.config.ts` |
| 7-4 | Border radius values consistent across components | DevTools inspection |
| 7-5 | Logo renders at correct size and position | Compare to `/design/brand/logos/` |
| 7-6 | All five active mockups are visually consistent with each other | Side-by-side comparison |
| 7-7 | Peek-fold variant: browse bar visible below hero on load | Screenshot at 1440x900 |
| 7-8 | Scroll-indicator variant: circle is subtle, not distracting | Screenshot at 1440x900 |
| 7-9 | Mobile: no content is cut off or hidden unintentionally | Screenshots at 390x844 |

---

## 8. Edge Cases & Stress Tests

| # | Scenario | Expected |
|---|---|---|
| 8-1 | Very long article title (80+ characters) | Title wraps cleanly, no overflow |
| 8-2 | Missing hero image (broken path) | Graceful fallback, no layout collapse |
| 8-3 | Slow network (3G throttle) | Images lazy-load, layout stable before images arrive |
| 8-4 | JavaScript disabled | Page content still visible, links work (progressive enhancement) |
| 8-5 | Dark mode (if `prefers-color-scheme: dark`) | No unreadable text or invisible elements (or intentionally no dark mode) |
| 8-6 | Print stylesheet | Content prints readably, no wasted pages on nav/images |
| 8-7 | Browser font size set to "Very Large" (20px base) | Layout adapts, nothing overflows |
| 8-8 | Ad blocker active | No assets blocked (all self-hosted) |
| 8-9 | Multiple rapid orientation changes on tablet | No layout thrashing or stuck states |

---

## Testing Priority Order

Complete in this order to catch high-impact issues first:

1. **P0 Browsers + Desktop 1440px** — baseline visual correctness
2. **P0 Mobile (iPhone 14 + iPhone SE)** — responsive layout
3. **Interaction scenarios (Section 4)** — nothing broken functionally
4. **Accessibility audit (Section 6)** — compliance
5. **P0 Tablet (iPad portrait + landscape)** — intermediate breakpoints
6. **Performance (Section 5)** — load times
7. **P1 Browsers** — Firefox, Edge
8. **Edge cases (Section 8)** — resilience
9. **P2 Browsers + viewports** — Samsung Internet, 2560px, 320px
10. **Archived mockups** — spot-check navigation and footer variants

---

## Issue Tracking Template

When a check fails, log it in this format:

```
### [FAIL] 3C-8 — Hero peek not visible on iPad portrait
- **File:** blog-v10-peek-fold.html
- **Browser:** Safari 18 (iPad)
- **Viewport:** 768 x 1024
- **Expected:** Browse bar pills visible below hero fold
- **Actual:** Hero fills full viewport, no peek visible
- **Screenshot:** [attach]
- **Severity:** Medium
- **Fix:** Adjust calc() value at 768px breakpoint
```
