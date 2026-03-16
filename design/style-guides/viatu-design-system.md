# Viatu Design System Reference

> **Source of truth**: Extracted from `viatu-complete-css.css`, cross-referenced with live site analysis (viatu.com homepage, destinations, destination detail, blog).
> **Last updated**: February 2026

---

## 1. Brand Identity

| Attribute | Value |
|-----------|-------|
| Brand | Viatu — "The Trip Builder for Conscious Travellers" |
| Focus | Sustainable, tailor-made travel in Africa & beyond |
| Values | Sustainability · Local community support · Authentic experiences |
| Certifications | B Corp · 1% for the Planet · Future of Tourism · UN Global Compact |
| Social proof | Reviews.io 5.0 (153 reviews) · Featured in Skift, Fortune, Quartz, Sifted |

---

## 2. Color System

### 2.1 Brand Palette (Official)

| Token | Name | Hex | Role |
|-------|------|-----|------|
| `--sangria-red` | Sangria | `#541736` | **Primary** — CTAs, logos, nav, key brand moments, tagline text |
| `--pthalo-green` | Pthalo | `#1C4447` | **Secondary** — Supporting actions, focus rings, footer, balance color |
| `--platinum-grey` | Platinum | `#C4C4C4` | **Neutral** — Borders, dividers, subtle UI elements |
| `--black` | Black | `#000000` | **Supporting** — Body text, strong contrast |
| `--white` | White | `#FFFFFF` | **Supporting** — Backgrounds, negative space |
| `--cream` | Cream | `#F3FFB9` | **Supporting** — Accent highlights (⚠️ lime-yellow, not beige) |

### 2.2 Extended Neutrals

| Token | Hex | Usage |
|-------|-----|-------|
| `--grey-light` | `#F8F9FA` | Light backgrounds, badge fills |
| `--grey-medium` | `#6C757D` | Secondary text, metadata, placeholders |
| `--grey-dark` | `#343A40` | Dark UI text, icon fills |
| `--grey-300` | `#DEE2E6` | Input borders, subtle dividers |

### 2.3 Semantic / Feedback Colors

| Token | Hex | Role |
|-------|-----|------|
| `--color-success` | `#22c55e` | Success states, confirmations |
| `--color-danger` | `#ef4444` | Errors, destructive actions |
| `--color-warning` | `#f59e0b` | Warnings, caution states |

> These are utility colors only — not part of the brand palette. Use sparingly and never as decorative elements.

### 2.4 Color Hierarchy (Proportions)

1. **Dominant**: Sangria `#541736` — most prominent brand color
2. **Secondary**: Pthalo `#1C4447` — balance and depth
3. **Supporting**: Platinum, Black, White, Cream — neutral scaffolding

### 2.5 Contextual Usage

| Context | Color |
|---------|-------|
| Primary CTA buttons | Sangria background, white text |
| Secondary CTA buttons | Pthalo background, white text |
| Outline buttons | Transparent bg, sangria or pthalo border + text |
| Button hover | `#47142e` (sangria hover) + `opacity 0.9` + `translateY(-1px)` |
| Button active | `#3b1026` (sangria active) |
| Focus ring (inputs) | Pthalo `rgba(28, 68, 71, 0.1)` 3px spread |
| Section taglines | Sangria text on Caveat font |
| Card borders | Platinum `#C4C4C4` or `rgba(196,196,196,0.3)` |
| Card accent | 4px left border in Sangria |
| Dark icon grid cells | Sangria background |

---

## 3. Typography System

### 3.1 Font Families

| Token | Stack | Role |
|-------|-------|------|
| `--font-primary` | **Krona One**, -apple-system, BlinkMacSystemFont, Segoe UI, Roboto, sans-serif | Display / H1 headers |
| `--font-secondary` | **Hanken Grotesk**, Satoshi, -apple-system, BlinkMacSystemFont, sans-serif | Body, H2–H5, UI elements |
| `--font-supporting` | **Caveat**, cursive | Taglines, handwritten accents |
| `--font-mono` | Source Code Pro, Monaco, monospace | Code (if needed) |

> ⚠️ **Correction**: The uploaded markdown/PDF incorrectly listed Inter and Playfair Display. The actual fonts are **Krona One** (display) and **Hanken Grotesk** (body).

### 3.2 Font Weights

| Token | Value | Available in |
|-------|-------|-------------|
| `--font-light` | 300 | Hanken Grotesk |
| `--font-regular` | 400 | Krona One, Hanken Grotesk |
| `--font-medium` | 500 | Hanken Grotesk |
| `--font-semibold` | 600 | Hanken Grotesk |
| `--font-bold` | 700 | Hanken Grotesk, Caveat |
| `--font-black` | 900 | Hanken Grotesk |

> Note: **Krona One** only comes in Regular (400). It is inherently bold-looking and does not need weight variation.

> ⚠️ **Numbers Rule**: All numeric content — prices, statistics, counts, dates, percentages, phone numbers — must **always** use **Hanken Grotesk** (`--font-secondary`). Never set numbers in Krona One (`--font-primary`) or Caveat (`--font-supporting`). This applies even when a number appears inside a headline or tagline; wrap the numeric portion in a span styled with `font-family: var(--font-secondary)`.

### 3.3 Desktop Type Scale

| Class | Font | Size | Weight | Line Height | Letter Spacing | Notes |
|-------|------|------|--------|-------------|----------------|-------|
| `.h1` | Krona One | 70px | 400 (regular) | 1.34 | -0.06em | Hero headlines |
| `.h2` | Hanken Grotesk | 58px | 700 (bold) | 1.2 | -0.03em | Section titles |
| `.h3` | Hanken Grotesk | 48px | 700 (bold) | 1.2 | — | Sub-sections |
| `.h4` | Hanken Grotesk | 40px | 700 (bold) | 1.2 | — | Card group titles |
| `.h5` | Hanken Grotesk | 32px | 700 (bold) | 1.2 | — | Card titles |
| `.body-xl` | Hanken Grotesk | 24px | 400 | 1.5 | — | Lead paragraphs |
| `.body-l` | Hanken Grotesk | 20px | 400 | 1.5 | — | Large body |
| `.body-m` | Hanken Grotesk | 18px | 400 | 1.5 | — | Default body |
| `.body-s` | Hanken Grotesk | 16px | 400 | 1.5 | — | Standard body |
| `.body-xs` | Hanken Grotesk | 14px | 400 | 1.5 | — | Metadata, labels |
| `.tagline-l` | Caveat | 24px | 700 (bold) | 1.2 | — | Sangria color |
| `.tagline-m` | Caveat | 20px | 700 (bold) | 1.2 | — | Sangria color |
| `.tagline-s` | Caveat | 18px | 700 (bold) | 1.2 | — | Sangria color |

### 3.4 Mobile Type Scale

| Element | Desktop | Mobile |
|---------|---------|--------|
| H1 | 70px | 35px |
| H2 (section header) | 58px | 40px |

### 3.5 Line Heights

| Token | Value | Usage |
|-------|-------|-------|
| `--leading-tight` | 1.2 | Headers (H2–H5), taglines |
| `--leading-normal` | 1.34 | H1 specifically |
| `--leading-relaxed` | 1.5 | All body text |
| `--leading-loose` | 1.625 | Relaxed reading (optional) |

---

## 4. Spacing System (8px Grid)

| Token | rem | px | Common Usage |
|-------|-----|-----|-------------|
| `--space-1` | 0.25 | 4 | Micro gaps |
| `--space-2` | 0.5 | 8 | Icon gaps, tagline margin-bottom |
| `--space-3` | 0.75 | 12 | Button padding (vertical), input padding, carousel nav gap |
| `--space-4` | 1 | 16 | Container padding, card content padding, meta gaps |
| `--space-5` | 1.25 | 20 | — |
| `--space-6` | 1.5 | 24 | Button padding (horizontal), card padding, grid gaps |
| `--space-8` | 2 | 32 | CTA horizontal padding, carousel margin-top, icon grid padding |
| `--space-10` | 2.5 | 40 | — |
| `--space-12` | 3 | 48 | Section header margin-bottom, grid bottom margin |
| `--space-16` | 4 | 64 | — |
| `--space-20` | 5 | 80 | — |
| `--space-24` | 6 | 96 | — |
| `--space-32` | 8 | 128 | — |
| `--space-40` | 10 | 160 | — |
| `--space-48` | 12 | 192 | — |
| `--space-56` | 14 | 224 | — |
| `--space-64` | 16 | 256 | — |
| `--space-80` | 20 | 320 | — |
| `--space-96` | 24 | 384 | — |
| `--space-112` | 28 | 448 | — |

---

## 5. Border & Radius System

### 5.1 Border Radius

| Token | Value | px | Usage |
|-------|-------|-----|-------|
| `--radius-none` | 0 | 0 | Sharp edges |
| `--radius-sm` | 0.125rem | 2 | Icon grid items |
| `--radius-md` | 0.375rem | 6 | Buttons, inputs |
| `--radius-lg` | 0.5rem | 8 | Cards, travel cards, destination cards |
| `--radius-xl` | 0.75rem | 12 | — |
| `--radius-2xl` | 1rem | 16 | — |
| `--radius-full` | 9999px | ∞ | Badges, carousel dots, hover icons, avatar circles |

### 5.2 Border Widths

| Token | Value | Usage |
|-------|-------|-------|
| `--border-1` | 1px | Card borders, input borders, icon grid |
| `--border-2` | 2px | Outline buttons |
| `--border-4` | 4px | Card accent (left border) |

---

## 6. Shadow System

| Token | Value | Usage |
|-------|-------|-------|
| `--shadow-sm` | `0 1px 2px 0 rgba(0,0,0,0.05)` | Destination cards (default) |
| `--shadow-md` | `0 4px 6px -1px rgba(0,0,0,0.1), 0 2px 4px -1px rgba(0,0,0,0.06)` | Cards, travel cards, destination card hover |
| `--shadow-lg` | `0 10px 15px -3px rgba(0,0,0,0.1), 0 4px 6px -2px rgba(0,0,0,0.05)` | Elevated cards, travel card hover |
| `--shadow-xl` | `0 20px 25px -5px rgba(0,0,0,0.1), 0 10px 10px -5px rgba(0,0,0,0.04)` | Modals, popovers |
| `--shadow-2xl` | `0 25px 50px -12px rgba(0,0,0,0.25)` | Heavy emphasis |

---

## 7. Layout System

### 7.1 Breakpoints

| Token | Value | Label |
|-------|-------|-------|
| `--breakpoint-sm` | 640px | Small |
| `--breakpoint-md` | 768px | Medium |
| `--breakpoint-lg` | 1024px | Large |
| `--breakpoint-xl` | 1280px | Extra large |
| `--breakpoint-2xl` | 1536px | 2X large |

### 7.2 Containers

| Token | Max Width | Usage |
|-------|-----------|-------|
| `--container-sm` | 640px | Narrow content |
| `--container-md` | 768px | Medium content |
| `--container-lg` | 1024px | Standard content |
| `--container-xl` | 1280px | Wide content |
| `--container-2xl` | 1536px | Full-width content |
| `--content-narrow` | 65ch | Reading-optimized (blog) |
| `--content-wide` | 80ch | Wide reading |

Container base: `width: 100%; margin: 0 auto; padding: 0 var(--space-4);`

### 7.3 Grid System

| Layout | Columns | Gap | Responsive |
|--------|---------|-----|------------|
| Travel cards | `auto-fit, minmax(280px, 1fr)` | `--space-6` | 1 → 2 (640px) → 4 (1024px) |
| Destination cards | `auto-fit, minmax(300px, 1fr)` | `--space-6` | 1 → 2 (768px) → 3 (1024px) |
| Icon grid | 9 columns | `--space-4` | 3 (mobile) → 6 (tablet) → 9 (desktop) |

---

## 8. Animation System

### 8.1 Durations

| Token | Value | Usage |
|-------|-------|-------|
| `--duration-75` | 75ms | — |
| `--duration-100` | 100ms | — |
| `--duration-150` | 150ms | — |
| `--duration-200` | 200ms | Buttons, inputs, icons, carousel dots |
| `--duration-300` | 300ms | Cards, destination cards, hover overlays |
| `--duration-500` | 500ms | — |
| `--duration-700` | 700ms | — |
| `--duration-1000` | 1000ms | — |

### 8.2 Easing Functions

| Token | Value | Usage |
|-------|-------|-------|
| `--ease-linear` | `linear` | — |
| `--ease-in` | `cubic-bezier(0.4, 0, 1, 1)` | Exit animations |
| `--ease-out` | `cubic-bezier(0, 0, 0.2, 1)` | Enter animations |
| `--ease-in-out` | `cubic-bezier(0.4, 0, 0.2, 1)` | **Default** — buttons, cards, all interactions |

---

## 9. Component Patterns

### 9.1 Buttons

| Variant | Background | Text | Border | Padding | Radius |
|---------|-----------|------|--------|---------|--------|
| Primary | `--sangria-red` | White | none | `--space-3` / `--space-6` | `--radius-md` (6px) |
| Secondary | `--pthalo-green` | White | none | `--space-3` / `--space-6` | `--radius-md` |
| Outline Primary | transparent | `--sangria-red` | 2px sangria | `--space-3` / `--space-6` | `--radius-md` |
| Outline Secondary | transparent | `--pthalo-green` | 2px pthalo | `--space-3` / `--space-6` | `--radius-md` |
| CTA | `--sangria-red` | White | none | `--space-4` / `--space-8` | `--radius-md` |

All buttons: `font-family: var(--font-secondary)` · `font-weight: 500` · `font-size: 16px` · `min-height: 44px` · `transition: all 200ms ease-in-out`

Hover: `opacity 0.9` + `translateY(-1px)` · Outline hover: fills with brand color, text goes white

### 9.2 Cards

**Travel Card** — used for trip listings:
- `border-radius: var(--radius-lg)` (8px)
- `box-shadow: var(--shadow-md)` → hover: `var(--shadow-lg)` + `translateY(-4px)`
- Image: 100% width, 240px height, `object-fit: cover`
- Content padding: `var(--space-6)` (24px)
- Title: Hanken Grotesk 32px bold
- Meta: 14px, grey-medium
- Carousel dots: 6px circles (20px when active), absolute bottom

**Destination Card** — used for destination listings:
- `border-radius: var(--radius-lg)` (8px)
- `box-shadow: var(--shadow-sm)` → hover: `var(--shadow-md)` + `translateY(-2px)`
- `border: 1px solid rgba(196,196,196,0.3)`
- Image: 100% width, 200px height
- Content padding: `var(--space-4)` (16px)
- Title: Hanken Grotesk 20px bold
- Badges: `--radius-full` pills, `--grey-light` bg, `--grey-dark` text, platinum border

### 9.3 Section Headers

```
.section-header
  ├── .section-header-tagline  → Caveat 24px bold, sangria color, mb: 8px
  └── .section-header-title    → Krona One 58px regular, black, tracking: -0.03em
```
`margin-bottom: var(--space-12)` (48px) · `text-align: left`

### 9.4 Form Inputs

- Padding: `12px 16px`
- Border: `1px solid #DEE2E6`
- Radius: `var(--radius-md)` (6px)
- Font: Hanken Grotesk, 16px
- Min height: 44px (touch target)
- Focus: `border-color: var(--pthalo-green)` + `box-shadow: 0 0 0 3px rgba(28,68,71,0.1)`

### 9.5 Carousel Navigation

- Button: 44×44px, `--radius-full`, white bg, platinum border
- Icon: 20×20px, `--grey-dark`
- Gap: `var(--space-3)` (12px)
- Disabled: `opacity: 0.5`

### 9.6 Icon System

**Sizes**: xs (10px) · sm (16px) · md (24px) · lg (60px)

**Color variants**: `--light` (black on white) · `--dark` (white on dark) · `--sangria` (brand accent)

**Icon categories** (SVG, stroke-based):
- Location types: national-park, nature-reserve, town, destination, region, city, private-concession, province, island
- UI: star, verified, avatar, chevron, sort, filters, pause
- Social: Facebook, Instagram, LinkedIn

All icons: `stroke-width: 1.5; fill: none; stroke: currentColor`

---

## 10. Image Specifications

| Context | Dimensions | Aspect Ratio | Notes |
|---------|-----------|--------------|-------|
| Hero images | 2000 × 1340px | ~3:2 | Full-width, text overlay |
| Destination cards (square) | 700 × 700px | 1:1 | Grid listings |
| Travel card images | 100% × 240px | Fluid | `object-fit: cover` |
| Destination detail images | 540–800px | 1:1 | Gallery |
| Partner logos | Various | — | White on transparent |

All images: CloudFront CDN · `quality=80` · `format=auto`

---

## 11. Accessibility

| Requirement | Implementation |
|-------------|---------------|
| Touch targets | Minimum 44px (`min-height: 44px` on buttons, inputs) |
| Focus states | Visible ring: `0 0 0 3px` in brand color at 10% opacity |
| Color contrast | Sangria on white: ~10:1 ✓ · Pthalo on white: ~8.5:1 ✓ |
| Keyboard nav | All interactive elements focusable |
| Disabled state | `opacity: 0.5; cursor: not-allowed` |

---

## 12. Email / Cross-Platform Notes

When adapting this system for email:

| Token | Web | Email Equivalent |
|-------|-----|-----------------|
| Krona One | Google Fonts | Web font with Arial fallback |
| Hanken Grotesk | Google Fonts | Web font with Helvetica/Arial fallback |
| Caveat | Google Fonts | Web font with Georgia fallback |
| `--radius-md` (6px) | CSS | Supported in most clients |
| `--shadow-md` | CSS | Not supported — use borders instead |
| Grid | CSS Grid | Table-based layout |
| Cream `#F3FFB9` | Background | Use sparingly — high-energy accent |
| Min 44px touch targets | CSS | Maintain for mobile email |

---

## 13. Corrections Log

| Item | Incorrect (from MD/PDF) | Correct (from CSS) |
|------|------------------------|---------------------|
| Primary font | Inter | **Krona One** |
| Secondary font | Playfair Display | **Hanken Grotesk** (+ Satoshi fallback) |
| Supporting font | (missing) | **Caveat** (cursive) |
| Cream hex | `#F5F5DC` (beige) | **`#F3FFB9`** (lime-yellow) |
| H1 size | rem-based scale | **70px** desktop / **35px** mobile |
| H2 size | rem-based scale | **58px** desktop / **40px** mobile |
| H1 font | Secondary font | **Primary font** (Krona One) |
| H1 line-height | 1.25 | **1.34** |
| Body line-height | 1.5 | **1.5** ✓ (confirmed) |
| Leading-tight | 1.25 | **1.2** |
| Input focus color | `rgba(45,90,61,0.1)` | **`rgba(28,68,71,0.1)`** (pthalo-based) |