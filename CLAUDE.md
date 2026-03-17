# CLAUDE.md — Website Design Project

## Project Overview

A SaaS web application built with Vue 3, Nuxt, and Tailwind CSS. Design direction is professional and inspirational. All UI work must respect the style guides and reference images stored in `/design/`.

---

## Tech Stack

- **Framework:** Nuxt 3
- **UI Library:** Vue 3 (Composition API)
- **Styling:** Tailwind CSS
- **Language:** TypeScript preferred

---

## Project Structure

```
/
├── design/                          # Design source files (never served publicly)
│   ├── style-guides/                # ← DROP typography, spacing, color guides here
│   ├── reference-images/            # ← DROP inspiration screenshots here
│   ├── brand/
│   │   ├── logos/                   # ← DROP logo SVGs/PNGs here
│   │   └── icons/                   # ← DROP favicon, app icons here
│   └── mockups/                     # ← DROP wireframes and page mockups here
│
├── public/                          # Statically served assets
│   ├── images/
│   │   ├── brand/
│   │   │   ├── logos/               # ← DROP production logo files here
│   │   │   └── icons/               # ← DROP favicon/OG icons here
│   │   ├── photos/                  # ← DROP photography and hero images here
│   │   └── og/                      # Open Graph images
│   └── fonts/                       # ← DROP self-hosted font files here
│
├── assets/
│   ├── css/                         # Global CSS (fonts, resets, tokens)
│   └── images/                      # Build-processed images
│
├── components/
│   ├── ui/                          # Base UI components (buttons, inputs, cards…)
│   │   └── PlaceholderImage.vue     # Clean image placeholder — use until real assets arrive
│   ├── layout/                      # Header, footer, nav, sidebar
│   └── sections/                    # Page sections (Hero, Pricing, Features…)
│
├── composables/                     # Vue composables (useX.ts)
├── layouts/                         # Nuxt layouts
├── pages/                           # File-based routing
├── server/api/                      # Nuxt server routes
└── types/                           # Shared TypeScript types
```

---

## Design Workflow — Required Before Any UI Work

Every time a component, page, or layout is created or modified:

1. **Read all files in `/design/style-guides/`** — follow typography, spacing, and color rules precisely
2. **Review images in `/design/reference-images/`** — absorb layout patterns and spatial rhythm
3. **Study live reference sites** — check `/design/reference-images/inspiration-links.md` for URLs relevant to the current task. Use WebFetch to study 2–3 of the most relevant sites, noting layout structure, typography hierarchy, image-text rhythm, whitespace, and navigation patterns to adapt. Do not copy — extract principles only.
4. **Check `/design/brand/logos/`** — use real logo if present; otherwise use `PlaceholderImage`
5. **Check `/design/mockups/`** — if a mockup exists for the page/section, follow it
6. **Adapt, never copy** — reference images and live sites are inspiration only; all output must be this project's own
7. **Use the `frontend-design` skill** for all substantial UI implementation

---

## Image Placeholder Convention

When real images, logos, or photos are not yet available, **always use `<PlaceholderImage>`** — never use broken `<img>` tags, external placeholder services, or lorem picsum URLs.

```vue
<!-- Basic usage -->
<PlaceholderImage label="Hero image" ratio="16/9" />

<!-- Logo slot -->
<PlaceholderImage label="Logo" ratio="3/1" width="160px" theme="neutral" />

<!-- Team photo -->
<PlaceholderImage label="Team member" ratio="1/1" width="80px" />

<!-- Hero with size hint -->
<PlaceholderImage
  label="Hero background"
  ratio="21/9"
  hint="2400 × 1000"
  :show-size="true"
  theme="cool"
/>
```

Props:

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `label` | string | `'Image placeholder'` | Descriptive text shown inside |
| `ratio` | string | `'16/9'` | CSS aspect-ratio value |
| `width` | string | `'100%'` | Explicit width override |
| `hint` | string | — | Size hint shown below label |
| `showSize` | boolean | `false` | Show size hint |
| `theme` | `neutral \| warm \| cool` | `neutral` | Color tone |

Replace `<PlaceholderImage>` with a real `<img>` or `<NuxtImg>` tag once the asset is dropped into its folder.

---

## Design Standards

### Typography
- Follow the type scale defined in `/design/style-guides/`
- Respect font weight hierarchy — headings, subheadings, body, captions each have defined roles
- Line height and letter spacing are part of the design — do not override without cause

### Spacing
- Use the spacing scale from style guides consistently — no arbitrary gaps
- Whitespace is intentional; generous breathing room is preferred over cramped layouts
- Section padding, component padding, and element margins each have separate rules

### Visual Quality Bar
- **Professional:** Clean structure, consistent rhythm, no visual noise
- **Inspirational:** Bold ideas executed with restraint, purposeful detail
- **Accessible:** WCAG AA minimum contrast, semantic HTML, keyboard navigable
- Production-grade output only — no generic or placeholder aesthetics in finished work

---

## Code Conventions

- Use `<script setup lang="ts">` in all Vue SFCs
- Use `defineProps` and `defineEmits` with TypeScript generics
- Composables go in `/composables/` and are named `use[Feature].ts`
- Components are PascalCase; pages and composables are kebab-case or camelCase
- Prefer `v-bind` shorthand (`:`) and `v-on` shorthand (`@`)
- Do not use Options API — Composition API only

---

## Styling Rules

- Tailwind utility classes directly in templates — no inline styles
- Design tokens (colors, spacing, fonts) defined in `tailwind.config.ts`; no arbitrary Tailwind values unless unavoidable
- `<style scoped>` only when Tailwind is genuinely insufficient
- Mobile-first responsive design (`sm:`, `md:`, `lg:` breakpoints)

---

## Commands

```bash
npm install       # Install dependencies
npm run dev       # Start dev server
npm run build     # Build for production
npm run preview   # Preview production build
npm run typecheck # Type check
```

---

## Standing Rules for Claude

- Read style guides in `/design/style-guides/` before writing any UI
- Use `/design/reference-images/` as creative input — always adapt to this project's style
- Use `<PlaceholderImage>` whenever a real image asset is not yet available
- Do not use external image placeholder URLs (no picsum, placehold.co, etc.)
- Do not introduce new dependencies without user confirmation
- Do not auto-commit changes unless explicitly asked
- Prefer editing existing files over creating new ones
- Keep components focused and single-purpose
- When a design decision is ambiguous, ask rather than assume
