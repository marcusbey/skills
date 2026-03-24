# Pre-Delivery Checklists — Reference

Pre-delivery checklist. Read this before calling any build complete.

---

## NON-NEGOTIABLES — What separates premium from polished-generic

These 10 principles are synthesized from live analysis of award-winning sites.
They are not patterns to apply — they are standards to judge against.
**If a build violates any of these, it cannot read as premium regardless of other quality.**

### 1. The first 300ms is a sensory event, not a message
Premium sites use the load/entry as an **authored moment** — a flash of brand color,
a logo building itself, an illustration fading in. Nothing happens before something
has already happened. The visitor is inside the brand before they've read a word.

> Bad: white flash -> content appears
> Good: full-screen brand color -> logo animates -> content reveals

### 2. Type does structural work, not label work
Headlines are sized and positioned like architectural elements, not text containers.
A heading at 87px with -3px letter-spacing sitting next to a canvas is a column.
A heading at 32px centered above a card grid is a label.

> Bad: h2 centered above a card grid, 36px, weight 700, bottom margin 24px
> Good: h1 at 87px overflowing the viewport, positioned to cross a split boundary

### 3. Every cursor state is designed
The single biggest tell between premium and not. Nothing is static under the cursor.
Every interactive zone has a **geometric** response — not just color change.

> Bad: `color: var(--primary)` on link hover
> Good: text scrambles, splits, swaps, grows, or reveals a second element

### 4. Color temperature is one decision, not a palette
One atmospheric choice applied consistently. Never pure `#000` or pure `#fff`.
All surfaces shifted toward the same warmth or coolness.

> Bad: `#141414` dark sections, `#ffffff` light sections
> Good: `#141314` (warm dark) and `#eee` (warm white) — identical temperature

### 5. Scroll is authored, not navigated
Every scroll unit spent on a designed reveal. If you can scroll through a section
without anything changing except position, that section is not earned.

> Bad: sections fade in with IntersectionObserver opacity 0 to 1
> Good: active process step tracks scroll position, photo panel swaps, sticky portrait

### 6. Sections are moods, not containers
Each section has a distinct emotional temperature that shifts the visitor's state
before they read a word. The shift should feel like entering a different room.

> Bad: all sections same light grey background, content swaps
> Good: warm editorial -> near-black studio -> silhouette against gradient

### 7. The detail nobody asked for
At least one element exists purely because it's delightful, not because it converts.
Keyboard shortcuts, ASCII art, tab title changes, ghost wordmarks, selection colors.
This is the most reliable signal that the site was made by people who love what they do.

> Bad: every element has a conversion purpose
> Good: `C` key reshuffles the ASCII art; tab says "Don't be shy, Fella." on hover

### 8. Font loading is a brand decision, not a default
Premium sites never use a widely-used free font as the display face.
The font is a budget line item. The cost makes the distinctiveness possible.

> Bad: Inter + Playfair Display (Google Fonts, seen on 200,000 sites)
> Good: aktiv-grotesk (Adobe Fonts, $), BerlingskeSerif (paid), custom variable font

### 9. White space is held under pressure
The ability to hold empty space without discomfort is the clearest indicator of
design confidence. Amateurs fill space. Premium designers hold it.

> Bad: every viewport has something in every quadrant
> Good: couple's names separated by 900px of intentional nothing

### 10. Motion has one vocabulary per site
2-3 named easing curves maximum, applied to every animation. Inconsistent easings
are the motion equivalent of using 8 different font weights.

> Bad: `ease`, `ease-in-out`, `0.3s`, `cubic-bezier(0.4,0,0.2,1)`, all mixed
> Good: `--ease-out-quint: cubic-bezier(0.22,1,0.36,1)` used everywhere, 700ms

---

## PHASE 9 — EDGE CASES & STATES (where cheap sites leak)

Design ALL of these before calling it done:

| State | What cheap sites do | What premium does |
|---|---|---|
| Loading | Browser spinner | Skeleton that matches the layout |
| Empty | Blank div | Illustration + helpful copy + action |
| Error | Default alert | Warm copy + icon + recovery path |
| Success | Green "Success!" | Brand-colored confirmation + icon + next step |
| 404 | Default browser page | Brand statement + personality (P28) |
| Focus | Browser default ring | Custom visible ring — accessibility = trust |
| Mobile nav | Instant show/hide | Slides/scales in with animation |
| Touch target | Whatever size | Min 44x44px |
| Overscroll | Wrong background | First/last section color matches browser chrome |

---

## PHASE 10 — ANTI-PATTERNS (never break these)

### Color and gradient:
- NEVER `linear-gradient(#000, #fff)` or any high-contrast pair in <300px height
- NEVER pure `#000000` or `#ffffff` — always temperature-adjusted variants
- NEVER introduce a new color after Phase 4 lock
- NEVER more than 2 accent colors on one page
- NEVER full-bleed gradient scrim on images — top 30% OR bottom 30% only
- NEVER adjacent sections with their own gradients — they'll fight each other

### Layout and composition:
- NEVER centered text + centered button on plain white bg (looks like a template)
- NEVER hero image carousel
- NEVER equal-height card grids — use masonry or intentional asymmetry
- NEVER "Trusted by X companies" logo rows
- NEVER stock photography with office workers
- NEVER more than one primary focal point per viewport

### Typography:
- NEVER Font Awesome or any icon font — use SVG
- NEVER default system font on a premium site
- NEVER all-caps on body text
- NEVER `font-weight: 400` on display headings

### Motion:
- NEVER `transition: all` — always specify the property
- NEVER `animation: bounce` or `animation: pulse`
- NEVER identical easing on every element (creates mechanical feeling)
- NEVER hover states that change ONLY color (geometry must change too)
- NEVER scroll reveal on every element — selective use = premium (50% max)
- NEVER animation that serves no purpose (motion must mean something)

### Code quality:
- NEVER `box-shadow` as primary depth — use z-layering, bg color change
- NEVER inline styles on repeating elements
- NEVER `!important` except to override third-party styles

---

## PHASE 11 — THE 10 PREMIUM SIGNALS CHECKLIST

Before delivering, verify all 10:

1. **Preloader is a statement** — brand color fullscreen, not a spinner or logo fade
2. **Typography IS the hero somewhere** — one section where type alone is the art
3. **Cursor is alive** — lag, zone-specific states (view/drag/play), labels on key zones
4. **Sections bleed** — no hard cuts. Every boundary has a visual bridge
5. **First scroll surprises** — something unexpected happens at y:200. Visitor is rewarded
6. **Color creates atmosphere** — not just section theming. Ambient light, gradients, depth
7. **One signature interaction** — the thing they tell someone else about (only one)
8. **Footer is a destination** — strong copy, CTA with surprise hover, not a sitemap
9. **Nav reads anywhere** — `mix-blend-mode: exclusion` on nav, always visible
10. **Motion has a language** — same easing vars, same duration scale, nothing random
