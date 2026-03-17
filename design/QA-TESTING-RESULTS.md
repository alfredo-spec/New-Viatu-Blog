# QA Testing Results — Viatu Blog Mockups

Last run: 2026-02-26 · Browser: Chromium (macOS) · Tested by: Antigravity automated QA

---

## Summary

| Mockup | Overall | Fails | Notes |
|---|---|---|---|
| `blog-v10-master.html` | ⚠️ PARTIAL | 2 | Mobile nav + mobile pills |
| `blog-v10-master-staging.html` | ✅ PASS | 0 | Clean across all checks |
| `blog-v10-peek-fold.html` | ⚠️ PARTIAL | 1 | Mobile nav only |
| `blog-v10-scroll-indicator.html` | ⚠️ PARTIAL | 3 | Indicator fade timing, mobile tap, mobile nav |
| `blog-v10-destinations-editorial.html` | ⚠️ PARTIAL | 2 | Expert stats missing, mobile nav crowding |

---

## Logged Failures

---

### [FAIL] 3A-3 — Mobile navigation does not collapse (master)
- **File:** blog-v10-master.html
- **Browser:** Chromium
- **Viewport:** 390 x 844
- **Expected:** Navigation collapses into a mobile-friendly menu (e.g., hamburger menu) or elements resize to fit the narrower screen.
- **Actual:** Navigation items remain at desktop scale. The "Back to homepage" button is too wide, causing the header to appear crowded with potential horizontal overflow.
- **Severity:** Medium
- **Fix:** Implement responsive nav — hide text links and "Back to homepage" label on `< 768px`; show a hamburger icon or abbreviate the CTA.

---

### [FAIL] 3D-2 — Mobile category pills not reliably horizontally scrollable (master)
- **File:** blog-v10-master.html
- **Browser:** Chromium
- **Viewport:** 390 x 844
- **Expected:** All category pills accessible via horizontal swipe.
- **Actual:** Pills are cut off at the right edge of the viewport; horizontal drag did not reliably reveal hidden pills.
- **Severity:** Medium
- **Fix:** Confirm `overflow-x: auto` and `white-space: nowrap` on the browse bar; `-webkit-overflow-scrolling: touch` may also be needed.

---

### [FAIL] 3A-3 — Mobile navigation does not collapse (peek-fold)
- **File:** blog-v10-peek-fold.html
- **Browser:** Chromium
- **Viewport:** 390 x 844
- **Expected:** Navigation collapses or hides gracefully on mobile.
- **Actual:** All desktop navigation elements (Logo, Search, Language, "Back to homepage" button) remain fully expanded, leading to a cluttered header.
- **Severity:** Low
- **Fix:** Same as master — responsive nav breakpoint.

---

### [FAIL] 3C-10 — Scroll indicator does not fade at 120px threshold (scroll-indicator)
- **File:** blog-v10-scroll-indicator.html
- **Browser:** Chromium
- **Viewport:** 1440 x 900
- **Expected:** Scroll indicator fades/disappears after scrolling ~120px.
- **Actual:** Indicator remains visible at 120px; it had faded by ~486px scroll depth.
- **Severity:** Low
- **Fix:** Check the scroll event listener threshold — the fade-out `scrollY` condition appears to be set too high. Adjust to `scrollY > 120`.

---

### [FAIL] 4B-8 — Scroll indicator click does not trigger scroll on mobile (scroll-indicator)
- **File:** blog-v10-scroll-indicator.html
- **Browser:** Chromium
- **Viewport:** 390 x 844
- **Expected:** Tapping the scroll indicator circle smooth-scrolls to the browse bar.
- **Actual:** Click/tap on the indicator produced no scroll action.
- **Severity:** Medium
- **Fix:** Verify the click handler is attached and targets the correct element. Check touch event support; may need `pointer-events: all` or an explicit `addEventListener('click', ...)`.

---

### [FAIL] 3A-3 — Mobile navigation does not collapse (scroll-indicator)
- **File:** blog-v10-scroll-indicator.html
- **Browser:** Chromium
- **Viewport:** 390 x 844
- **Expected:** Navigation collapses or hides gracefully on mobile.
- **Actual:** "Back to homepage" button remains full-sized, making the header crowded.
- **Severity:** Low
- **Fix:** Same responsive nav breakpoint fix as master.

---

### [FAIL] 3G — Expert section stats row missing (destinations-editorial)
- **File:** blog-v10-destinations-editorial.html
- **Browser:** Chromium
- **Viewport:** 1440 x 900
- **Expected:** Expert section contains portrait, stats row (Safaris, Countries, Articles), and pull quote.
- **Actual:** Portrait photo and pull quote present, but the stats row is not visible.
- **Severity:** Medium
- **Fix:** Confirm the stats HTML block is present in the file and not hidden via CSS (`display: none` or conditional class).

---

### [FAIL] 3A-3 — Mobile navigation crowding (destinations-editorial)
- **File:** blog-v10-destinations-editorial.html
- **Browser:** Chromium
- **Viewport:** 390 x 844
- **Expected:** Navigation collapses gracefully; no overlap or horizontal overflow.
- **Actual:** All desktop nav elements in one row; significant crowding and element overlap on the narrow viewport.
- **Severity:** High
- **Fix:** Highest priority — apply responsive header layout at `< 768px` across all mockups.

---

## Passes (Selected Highlights)

| Check | Mockups | Notes |
|---|---|---|
| 3A Desktop Nav (logo, CTA, search, opaque on scroll) | All 5 | ✅ Consistent |
| 3B Language Toggle (open/close/active state) | All 5 | ✅ Consistent |
| 3C Hero (full-width image, text over gradient, meta) | All 5 | ✅ Consistent |
| **3C-8 Peek-fold peek** | peek-fold | ✅ Browse bar peeking correctly on load |
| **3C-9 Scroll indicator circle** | scroll-indicator | ✅ Subtle circle visible in hero |
| 3D Sticky Browse Bar (sticks, pill smooth-scroll) | All 5 | ✅ Consistent |
| 3E Content sections (3-col desktop, section headings) | master-staging, destinations | ✅ |
| 3E-5 Destination cards (gradient overlay, name) | destinations-editorial | ✅ |
| 3E-7 Editorial split image-left/text-right | destinations-editorial | ✅ |
| 3E-8 Editorial split stacks on mobile | destinations-editorial | ✅ |
| 3G Expert section (portrait + stats + quote) | master-staging | ✅ |
| 3H Footer (4-col, social icons, B Corp, copyright) | master-staging | ✅ |
| 4A Scrolling (no glitches, scroll back to top) | All 5 | ✅ Consistent |
| 3D-2 Mobile category pills scrollable | peek-fold, master-staging, destinations | ✅ |
| 3E-2 Cards 1-col on mobile | master-staging | ✅ |

---

## Priority Fixes

1. **[HIGH] Mobile nav responsive breakpoint** — applies to all 5 mockups. `3A-3` fails everywhere. Shared CSS change.
2. **[MEDIUM] Mobile browse bar horizontal scroll** — `blog-v10-master.html` `3D-2`. Verify `overflow-x`.
3. **[MEDIUM] Scroll indicator click handler** — `blog-v10-scroll-indicator.html` `4B-8`.
4. **[MEDIUM] Expert stats row** — `blog-v10-destinations-editorial.html` `3G`.
5. **[LOW] Scroll indicator fade threshold** — `blog-v10-scroll-indicator.html` `3C-10`. Adjust JS threshold to 120px.

---

## Next Steps

- [ ] Run **Firefox** and **Safari** browser matrix (P0/P1).
- [ ] Run **iPad** viewport checks (768x1024, 1024x768).
- [ ] Run **Accessibility audit** (Section 6) with axe.
- [ ] Run **Performance checks** (Section 5) with Lighthouse.
- [ ] Apply mobile nav fix and re-test all 5 mockups.
- [ ] Spot-check 2–3 archived mockups for navigation/footer regressions.
