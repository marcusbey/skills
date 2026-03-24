## COMPOSITION PATTERN LIBRARY

When analyzing, identify which of these **premium composition patterns** are used:

### PATTERN A: The Pinned Portrait
A large person/product image is `position: sticky` or GSAP-pinned. Multiple text panels scroll past alongside it. The image may scale, fade, or shift position as different panels come into view.
- **Detection:** `position: sticky` on image container + multiple sibling text blocks
- **Example:** Dental site in screenshots — doctor portrait stays while sections scroll

### PATTERN B: The Gravity Cross
A large typographic element (headline) is split — half its letters live in Section A, the other half in Section B. As you scroll, the full word assembles.
- **Detection:** Overflow visible on parent + `translateY` or `clip-path` animations on text spans

### PATTERN C: The Ghost Reveal
Text appears as transparent/faded at the bottom of the current section. On scroll, it comes fully into view in the next section. Creates forward-pulling tension.
- **Detection:** `opacity: 0.2–0.5` on elements near section bottom + ScrollTrigger that increases opacity
- **Example:** Dental site — "aesthetic care / through advanced" appears faded, then fills the next viewport

### PATTERN D: The Background Mood Shift
Instead of a hard section border, a gradient or blurred transition converts a light section to a dark one (or vice versa). The content transition happens WITHIN the gradient zone.
- **Detection:** Overlapping sections with `mix-blend-mode`, or a dedicated transition div with gradient BG between sections
- **Example:** Dental site — the light grey section bleeds into the near-black section with a soft gradient divider

### PATTERN E: The Breaking Type
A large display typeface headline is placed BEHIND a photograph, with the photo's subject visually "breaking through" the text. The text reads around the image.
- **Detection:** `z-index` hierarchy where photo > text, + large font-size on headline
- **Example:** Dental site "Team of Experts" — faces overlap the text

### PATTERN F: The Continuous Persona
A single photo of a person appears in multiple sections — first as a small portrait, then full-bleed, then as a detail. The same face creates visual thread across 3–4 sections.
- **Detection:** Same `src` image used multiple times at different scales, or one very large image with scroll-parallax crop changing

### PATTERN G: The Scroll-Assembled Scene
Decorative elements (icons, lines, shapes) start scattered and appear to assemble into a composition as you scroll. Each element has a different scroll start time creating stagger.
- **Detection:** Multiple elements with ScrollTrigger, each with slight offset in `start` value

### PATTERN H: The Viewport-Sized Typography
Text is sized to viewport width (`font-size: Xvw`) so words become architectural elements, not just content. They structure space like columns or walls.
- **Detection:** `font-size` values in `vw` units on H1/H2, typically > 8vw

### PATTERN I: The Logo-Building Transition
The page transition doesn't just fade between pages — it animates the brand logo being
constructed during the transition itself. The result: every navigation is a brand moment.
The logo either draws itself (SVG stroke animation), builds from components (blocks
assembling into letterforms), or is revealed by a wipe. The full-screen transition color
IS the brand color.
- **Detection:** Full-screen colored overlay `z-index: 9999+` during navigation. Logo element appears and animates within that overlay. Color = brand primary.
- **Example:** good-fella.com — 4 dark squares animate into the pixelated GOOD wordmark on full-screen orange (`#fb460d`) on every SPA navigation.

### PATTERN J: The Sticky-Scrolled Thumbnail Navigator
In a portfolio/work section, a left panel sticks and shows 3–5 small project thumbnails.
Clicking a thumbnail instantly swaps the right panel to that project. Scrolling changes
which thumbnail is active. This solves the problem of showing multiple projects without
pagination — it's a gallery inside a section.
- **Detection:** Left column with `position: sticky`, 3+ small images with click handlers, right column with conditionally displayed large images.
- **Active state:** Orange/brand ■ dot next to active thumbnail. Inactive thumbnails at lower opacity.
- **Hover on right panel:** "VIEW PROJECT" badge appears centered — not a button, a label that materializes.

---

## PREMIUM QUALITY SIGNALS CHECKLIST

When evaluating a site, score these:

**Composition (0-5)**
- [ ] Cross-viewport element continuity (any of patterns A–J above)
- [ ] Deliberate negative space / breathing room
- [ ] Each viewport has a clear focal point
- [ ] Typography used as architectural structure (not just labels)
- [ ] Colour/light as a narrative tool (dark = authority, light = approachability)

**Motion (0-5)**
- [ ] Consistent easing language (same ease curve family throughout)
- [ ] Scroll-scrubbed (not just snap-in) animations
- [ ] Micro-interactions on hover/focus states
- [ ] Page transitions (if multi-page)
- [ ] Motion that reinforces hierarchy (larger elements move slower)

**Typography (0-5)**
- [ ] Maximum 2 typefaces
- [ ] Display face has genuine character (custom or rare)
- [ ] Type scale is geometric/mathematical
- [ ] Line length controlled (`max-width: 60–75ch` on body)
- [ ] Optical kerning and tracking tuned manually

**Interaction (0-5)**
- [ ] Hover states on all clickable elements — GEOMETRY, not just color
- [ ] Focus styles that match brand (not default browser blue)
- [ ] Loading/skeleton states
- [ ] Form feedback states (success, error, validating)
- [ ] Touch-friendly targets (≥44px) on mobile

**Personality (0-5)** ← new dimension from good-fella analysis
- [ ] Tab title changes on interaction (P69) — hover, idle, or return states
- [ ] Text selection `::selection` matches brand, not browser blue
- [ ] Keyboard easter eggs exist and are discoverable (P70)
- [ ] At least ONE element exists purely for delight, not conversion
- [ ] Footer has depth (ghost wordmark, ASCII art, or personality copy)

**Performance Signals (0-5)**
- [ ] WebP/AVIF image formats
- [ ] Lazy loading on below-fold images
- [ ] Fonts subset or display:swap
- [ ] No render-blocking scripts in `<head>`
- [ ] Smooth 60fps scroll (no jank)
