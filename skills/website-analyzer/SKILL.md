# SKILL: Deep Website Analyzer

## TRIGGER
Use this skill when the user asks to:
- "analyze this website"
- "explore this URL"
- "create a spec for [url]"
- "deconstruct this site"
- "recreate this website"
- "what animations/effects does [url] use"
- "how is [url] built"

---

## CORE PHILOSOPHY: THE PAINTING METAPHOR

**Premium sites are NOT a stack of independent viewport-height sections.**
They are a **continuous composition** — like a large painting — where:

1. **Elements begin in one section and complete in another** (a photo that starts small in section A becomes full-bleed in section B)
2. **Typography overlaps section boundaries** (text introduced as ghost/faded in one fold becomes solid as you scroll into the next)
3. **Sticky/pinned elements act as anchors** that other content scrolls past (a portrait stays fixed while text panels scroll alongside it)
4. **Background transitions aren't section changes** — they're mood shifts in a continuous narrative
5. **Cross-section elements create visual "threads"** that pull the eye forward through the page

This is the key distinction between a $500 template and a $50,000 build.

---

## EXECUTION PROCEDURE

### PHASE 0 — SETUP

```javascript
// Always start with these steps:
// 1. Get tab ID
// 2. Navigate to URL
// 3. Set viewport to 1440×900 (standard desktop)
// 4. Wait 4 seconds for all assets and animations to load
// 5. Take initial screenshot
```

```javascript
// Disable Lenis/smooth scroll so native scrollTo works:
if (window.lenis) window.lenis.stop();
if (window.locomotive) window.locomotive.stop();
// Override scroll libraries that block native scroll
document.documentElement.style.overflow = 'auto';
```

---

### PHASE 1 — STRUCTURAL RECONNAISSANCE

Run these JS probes to build the site map before any scrolling:

```javascript
// 1. Get total page height and all named sections
JSON.stringify(Array.from(document.body.children).map((el,i) => ({
  i,
  tag: el.tagName,
  id: el.id || null,
  cls: (el.className||'').toString().substring(0,80),
  top: el.offsetTop,
  h: el.offsetHeight
})).filter(el => el.h > 50))
```

```javascript
// 2. Detect animation libraries
({
  gsap: typeof gsap !== 'undefined',
  lenis: typeof Lenis !== 'undefined' || !!window.lenis,
  locomotive: typeof LocomotiveScroll !== 'undefined',
  framerMotion: typeof window.__framer_importFromPackage !== 'undefined',
  aos: typeof AOS !== 'undefined',
  swiper: typeof Swiper !== 'undefined',
  three: typeof THREE !== 'undefined',
  scripts: Array.from(document.scripts).map(s => s.src).filter(s => s && !s.includes('chrome'))
})
```

```javascript
// 3. Extract full CSS design tokens
const root = document.documentElement;
const cs = window.getComputedStyle(root);
const tokenNames = ['--primary','--secondary','--accent','--bg','--text','--font-body',
  '--font-heading','--color-dark','--color-light','--white','--black','--radius'];
const tokens = {};
tokenNames.forEach(v => { const val = cs.getPropertyValue(v); if(val) tokens[v] = val; });
// Also get font faces
const fonts = Array.from(document.styleSheets).flatMap(s => {
  try { return Array.from(s.cssRules).filter(r => r instanceof CSSFontFaceRule).map(r => r.cssText); }
  catch(e) { return []; }
});
JSON.stringify({ tokens, fonts })
```

```javascript
// 4. Get ALL CSS rules (extract in chunks to avoid filter blocks)
const sheet = document.styleSheets[0];
let totalRules = 0;
try { totalRules = sheet.cssRules.length; } catch(e) {}
totalRules + ' rules in main stylesheet'
```

```javascript
// 5. Detect sticky/fixed/pinned elements — key for cross-viewport compositions
Array.from(document.querySelectorAll('*')).filter(el => {
  const cs = window.getComputedStyle(el);
  return cs.position === 'sticky' || cs.position === 'fixed';
}).map(el => ({
  tag: el.tagName,
  cls: (el.className||'').toString().substring(0,60),
  position: window.getComputedStyle(el).position,
  top: window.getComputedStyle(el).top,
  zIndex: window.getComputedStyle(el).zIndex
})).slice(0, 20)
```

---

### PHASE 2 — FULL SCROLL CAPTURE

**Strategy:** Scroll in increments of 40% of viewport height to catch all states.
Take a screenshot at EACH position. Do not skip increments.

```javascript
// Get scroll increment
Math.floor(window.innerHeight * 0.4)
```

For each scroll position:
1. `window.scrollTo(0, position)`
2. Wait 500ms for animations to settle
3. Take screenshot
4. Note what is visible and any elements crossing the fold boundary

**CRITICAL — At each screenshot, explicitly look for:**

#### A. CROSS-FOLD ELEMENTS (The Painting Technique)
- Is any element visible in BOTH the upper portion AND lower portion of the viewport?
- Is the same element that was visible in the PREVIOUS screenshot still visible here but in a different position/size/state?
- Are there elements that appear to "float" between sections (not clearly belonging to either)?

#### B. SECTION BOUNDARY CROSSINGS
- Does any photo, illustration, or graphic element bleed past the bottom of its parent section into the next?
- Is there text that begins faded/ghosted and becomes solid as you scroll?
- Are there elements that start partially off-screen and scroll INTO their final position?

#### C. BACKGROUND CONTINUITY
- Do sections share a continuous background or gradient that creates visual connection?
- Does a dark section transition feel like a lighting change rather than a block swap?
- Are there decorative elements (lines, curves, dots) that straddle the section border?

#### D. PINNED COMPOSITION LAYERS
- Is any large image (portrait, product, scene) staying fixed while text slides past it?
- Is there a multi-panel "slideshow" where the image is pinned and only the text changes?

---

### PHASE 3 — CROSS-VIEWPORT COMPOSITION DETECTION

This is the most important phase. Run these probes at different scroll positions:

```javascript
// Detect elements that span across the visible viewport fold (cross-boundary elements)
// Run this at multiple scroll positions
const vh = window.innerHeight;
const scrollY = window.scrollY;
const foldTop = scrollY;
const foldBottom = scrollY + vh;
const crossFold = Array.from(document.querySelectorAll('img, video, canvas, [class*="photo"], [class*="image"], [class*="portrait"], section, div'))
  .filter(el => {
    const rect = el.getBoundingClientRect();
    const elTop = rect.top + scrollY;
    const elBottom = rect.bottom + scrollY;
    // Element must START before current fold AND END after it (spanning at least 60% of viewport)
    return elTop < foldTop + (vh * 0.3) && elBottom > foldBottom - (vh * 0.3) && rect.height > vh * 0.5;
  })
  .map(el => ({
    tag: el.tagName,
    cls: (el.className||'').toString().substring(0,60),
    h: Math.round(el.getBoundingClientRect().height),
    top: Math.round(el.getBoundingClientRect().top),
    bottom: Math.round(el.getBoundingClientRect().bottom),
    position: window.getComputedStyle(el).position
  }));
JSON.stringify(crossFold.slice(0,10))
```

```javascript
// Detect scroll-driven transform animations (elements that change state on scroll)
// Look for GSAP ScrollTrigger instances
if (typeof ScrollTrigger !== 'undefined') {
  ScrollTrigger.getAll().map(st => ({
    trigger: st.trigger?.className?.substring(0,40),
    start: st.start,
    end: st.end,
    pin: !!st.pin,
    scrub: st.vars?.scrub,
    animation: st.animation ? st.animation.vars : null
  })).slice(0,20)
} else 'No ScrollTrigger detected'
```

```javascript
// Detect elements with scroll-driven opacity fades (ghost text entering from next section)
Array.from(document.querySelectorAll('*')).filter(el => {
  const cs = window.getComputedStyle(el);
  const opacity = parseFloat(cs.opacity);
  return opacity > 0 && opacity < 0.5 && el.offsetHeight > 20;
}).map(el => ({
  tag: el.tagName,
  cls: (el.className||'').toString().substring(0,50),
  text: (el.innerText||'').trim().substring(0,40),
  opacity: window.getComputedStyle(el).opacity,
  transform: window.getComputedStyle(el).transform
})).slice(0,10)
```

```javascript
// Detect clip-path animations (section reveal transitions)
Array.from(document.querySelectorAll('*')).filter(el => {
  const cs = window.getComputedStyle(el);
  return cs.clipPath !== 'none' && cs.clipPath !== '';
}).map(el => ({
  tag: el.tagName,
  cls: (el.className||'').toString().substring(0,60),
  clipPath: window.getComputedStyle(el).clipPath
})).slice(0,15)
```

---

### PHASE 4 — SECTION-BY-SECTION DEEP DIVE

For each major section detected in Phase 1:

```javascript
// Jump to section and fully characterize it
window.scrollTo(0, SECTION_TOP);

// Get section's full child structure
const el = document.querySelector('.SECTION_CLASS');
Array.from(el.querySelectorAll('*')).map(c => ({
  tag: c.tagName,
  cls: (c.className||'').toString().substring(0,60),
  text: (c.innerText||'').trim().substring(0,80),
  src: c.tagName === 'IMG' ? c.src.replace(window.location.origin,'') : null,
  href: c.tagName === 'A' ? c.getAttribute('href') : null,
  bg: window.getComputedStyle(c).backgroundImage.substring(0,80)
})).slice(0,40)
```

**For each section, document:**
- Background color / image
- All text content (headings, body, labels)
- All images (src paths)
- All interactive elements
- Entry animation (how does this section animate in?)
- Exit state (what is visible at the bottom of this section that bleeds into next?)
- **Cross-section relationship:** What element from this section appears in the NEXT section?

---

### PHASE 5 — INTERACTIVE STATE EXPLORATION

**Click every interactive element** and document state changes:

1. Navigation links / hamburger menus
2. CTA buttons (hover + click states)
3. Accordions / expandable sections
4. Tabs / filter controls
5. Carousels / sliders
6. Form inputs (focus states)
7. Any elements with `cursor: pointer`

```javascript
// Find all clickable elements
Array.from(document.querySelectorAll('button, a, [role="button"], [onclick], [data-popup], [data-modal]'))
  .map(el => ({
    tag: el.tagName,
    cls: (el.className||'').toString().substring(0,60),
    text: (el.innerText||'').trim().substring(0,40),
    href: el.getAttribute('href'),
    dataAttrs: Object.fromEntries([...el.attributes].filter(a => a.name.startsWith('data-')).map(a => [a.name, a.value]))
  })).slice(0,30)
```

For each interactive element:
- Screenshot before hover
- Screenshot during hover
- Screenshot after click / open state
- Document the animation (slide, fade, scale, clip-path expand?)

---

### PHASE 6 — MOBILE VIEWPORT

```javascript
// Resize to iPhone 14 Pro
// Width: 393, Height: 852
```

After resize:
1. Scroll full page again
2. Screenshot every major section
3. Note: What changes? What reflows? What disappears?
4. Document mobile navigation pattern
5. Check: Do cross-viewport compositions survive on mobile?

---

### PHASE 7 — CSS EXTRACTION

Extract all CSS in chunks (avoid security filters by splitting):

```javascript
const sheet = document.styleSheets[0];
const rules = [];
for (let i = 0; i < sheet.cssRules.length; i++) {
  rules.push(sheet.cssRules[i].cssText);
}
// Extract in batches of 50 rules at a time
rules.slice(0, 50).join('\n')
// Continue: rules.slice(50, 100).join('\n') etc.
```

**Always extract these specifically:**
- All `@keyframes` (complete code)
- All CSS custom properties (`:root { ... }`)
- All `@media` queries
- All `position: sticky` / `position: fixed` rules
- All `clip-path` rules
- All `transform` rules with `transition`

---

### PHASE 8 — ASSET INVENTORY

```javascript
// All images
Array.from(document.querySelectorAll('img, [style*="background-image"]')).map(el => ({
  tag: el.tagName,
  src: el.src ? el.src.replace(window.location.origin,'') : 
       (el.style.backgroundImage || window.getComputedStyle(el).backgroundImage)
})).filter(el => el.src && el.src !== 'none')
```

```javascript
// All video sources
Array.from(document.querySelectorAll('video, source')).map(el => ({
  tag: el.tagName,
  src: el.src || el.getAttribute('src'),
  type: el.type
}))
```

```javascript
// All fonts
performance.getEntriesByType('resource')
  .filter(r => r.initiatorType === 'css' || r.name.includes('.woff') || r.name.includes('.ttf') || r.name.includes('.otf'))
  .map(r => r.name.replace(window.location.origin,''))
```

---

## OUTPUT FORMAT

The analysis output must be organized as follows:

### 1. OVERVIEW
- URL, title, page height
- Tech stack (libraries, CMS if detectable)
- Color palette + typography system
- Emotional arc / brand character

### 2. THE PAINTING MAP
**This is the most important section.**
A narrative description of how the page flows as a continuous composition:

> "The page opens with [describe first impression]. As you scroll, [element X] transitions from [state A] to [state B], creating a thread into the next section. The [photo/type/element] that begins [ghosted/small/partial] at the bottom of Section 2 becomes the dominant hero of Section 3 — this is the core compositional technique repeated N times throughout."

For each cross-viewport transition:
```
TRANSITION: Section [A] → Section [B]
Element: [description]
Entry state: [size/opacity/position at bottom of A]
Exit state: [size/opacity/position at top of B]
Technique: [pin | parallax | clip-path | opacity-fade | scale | none]
```

### 3. SECTION MAP (table)
Same as our TTN format — section name, scroll range, height, background, pin duration

### 4. EACH SECTION — DETAILED
- Visual composition (not just "left photo right text" but HOW they relate)
- Typography with exact values
- All assets
- Entry animation
- Exit bleed into next section

### 5. INTERACTIONS
- All clickable states
- All hover states
- All open/close animations

### 6. ANIMATION CATALOG
- All @keyframes
- All GSAP timelines (if accessible)
- All scroll-scrubbed animations

### 7. MOBILE DIFFERENCES

### 8. COMPLETE ASSET INDEX

---

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

---

## COMPLETE EXAMPLE OUTPUT STRUCTURE

```markdown
# [SITE NAME] — Complete Website Analysis
## URL: [url] · Analyzed: [date] · Viewport: 1440×900

---

## THE PAINTING (Compositional Narrative)
[2–3 paragraph description of how the page reads as a continuous experience]

### Cross-Viewport Transitions Detected
| From Section | To Section | Element | Technique | Entry State | Exit State |
|---|---|---|---|---|---|
| ... | ... | ... | ... | ... | ... |

---

## TECH STACK
[Table: library, version, source, purpose]

## DESIGN TOKENS
[Colors, fonts, spacing scale]

## PAGE MAP
[Full section table with scroll positions]

---

## SECTION ANALYSIS (one per section)

### Section N: [Name]
**Scroll range:** Xpx–Ypx | **BG:** [color/image] | **Pin:** [duration or none]

**Viewport Composition:**
[Describe the visual composition of this viewport as if describing a painting]

**Cross-section relationship:**
- Bottom bleed INTO this section: [what arrives from previous section]
- Top bleed OUT OF this section: [what begins here and completes in next section]

**Assets:** [table]
**Text:** [all copy]
**Animations:** [entry, exit, hover, scroll-scrubbed]
**CSS:** [relevant rules]

---

## INTERACTION MAP
[Each interactive element with all states — GEOMETRY changes, not just color]

## ANIMATION CATALOG
[All keyframes + GSAP configs + easing curves used]

## MOBILE ANALYSIS
[All changes at ≤768px]

## ASSET INDEX
[Complete file list]

## PERSONALITY SIGNALS
[Results from Phase 4 probes — tab title, keyboard shortcuts, canvas, selection color, ghost wordmark]

## NON-NEGOTIABLES ASSESSMENT

| Principle | Grade | Evidence |
|---|---|---|
| 1. First 300ms is sensory event | A/B/C/F | |
| 2. Type does structural work | A/B/C/F | |
| 3. Every cursor state designed | A/B/C/F | |
| 4. Color temp is one decision | A/B/C/F | |
| 5. Scroll is authored | A/B/C/F | |
| 6. Sections are moods | A/B/C/F | |
| 7. Detail nobody asked for | A/B/C/F | |
| 8. Font is a brand decision | A/B/C/F | |
| 9. White space held under pressure | A/B/C/F | |
| 10. One motion vocabulary | A/B/C/F | |

**Overall premium grade:** [A/B/C/F]

## PREMIUM QUALITY SCORE
[Full scored checklist — Composition / Motion / Typography / Interaction / Personality / Performance]
```

---

## PHASE 4 — PERSONALITY SIGNAL DETECTION

These are the details that separate a site made by people who love what they do
from a site made by people who finished the brief. Run these probes explicitly.

### 4A — Page transition anatomy

When navigating between pages, immediately screenshot the transition state.
Premium transitions are often the most impressive animation on the site.

```javascript
// Detect page transition overlays and their trigger mechanism
Array.from(document.querySelectorAll('[class*="transition"],[class*="overlay"],[class*="curtain"],[class*="loader"],[class*="preloader"]'))
  .filter(el => el.offsetWidth > 100)
  .map(el => {
    const cs = window.getComputedStyle(el);
    return {
      cls: (el.className||'').toString().substring(0,80),
      position: cs.position,
      zIndex: cs.zIndex,
      bg: cs.backgroundColor,
      opacity: cs.opacity,
      display: cs.display,
      w: el.offsetWidth, h: el.offsetHeight
    };
  })
```

**Critical observation:** Does the transition build the brand logo? good-fella.com
uses its full-screen brand orange flash to animate the pixelated GOOD logo letter
by letter. This is a page transition AND a branding moment simultaneously.

**Capture checklist:**
- [ ] Color of the transition overlay (brand color or black?)
- [ ] Does it build a logo or mark during the transition?
- [ ] Duration: instant flash, or slow reveal?
- [ ] Does it fire on EVERY navigation, or just first load?
- [ ] Exit: does content fade in, or does overlay slide away?

---

### 4B — Tab title as brand voice (P69 detection)

Watch the browser tab title while interacting with the site. Premium studios often
program it to change on hover, idle, and return.

```javascript
// Capture the current title and listen for changes
const originalTitle = document.title;
const observer = new MutationObserver(muts => {
  muts.forEach(m => {
    if (m.type === 'childList') console.log('Title changed to:', document.title);
  });
});
observer.observe(document.querySelector('title'), { childList: true });

// Also check if there's a visibilitychange handler
const listeners = getEventListeners ? getEventListeners(document) : null;
JSON.stringify({ originalTitle, hasVisibilityHandler: !!document.onvisibilitychange });
```

**Manual test:** Hover over a button or CTA link, then look at the browser tab.
If the title changes → document P69. Record:
- What triggers the change (hover, idle, return)
- What the new title says
- Whether it uses emoji
- Duration before it resets

---

### 4C — Keyboard easter egg detection (P70)

```javascript
// Detect keydown handlers that might be easter eggs
// Can't enumerate all, but we can check for common patterns
const hasKeyHandler = typeof document.onkeydown === 'function' ||
  document.addEventListener.toString().includes('native');

// Check for grid overlay elements (common target)
const gridEl = document.querySelector('[class*="grid"],[class*="overlay"],[class*="dev-"]');
const shortcuts = document.querySelector('kbd, [class*="shortcut"],[class*="kbd"]');

// Check footer for keyboard hint UI
const footer = document.querySelector('footer');
const footerKbd = footer ? Array.from(footer.querySelectorAll('kbd')).map(el => el.innerText) : [];

JSON.stringify({ hasKeyHandler, gridEl: gridEl?.className?.toString()?.substring(0,60), footerKbd });
```

**Manual test:** Press `C`, `G`, `Cmd+G`, `Ctrl+G`, `D`, `T`, `M` on the keyboard
while on the page. Watch for visual changes — character reshuffles, color mode flips,
grid overlays, hidden panels.

---

### 4D — Canvas analysis (P68 detection)

```javascript
// Detect canvas elements and their context type
Array.from(document.querySelectorAll('canvas')).map(c => {
  const cs = window.getComputedStyle(c);
  const ctx2d = c.getContext('2d');
  const ctxWgl = c.getContext('webgl') || c.getContext('webgl2');
  return {
    w: c.width, h: c.height,
    cssW: cs.width, cssH: cs.height,
    position: cs.position,
    cls: (c.className||'').toString().substring(0,60),
    renderType: ctxWgl ? 'WebGL' : ctx2d ? '2D Canvas' : 'Unknown',
    parent: (c.parentElement?.className||'').toString().substring(0,60)
  };
})
```

**If 2D canvas found:** Move mouse slowly across it. Does the rendered content change
relative to cursor position? This is the P68 mouse spotlight pattern.

**If WebGL canvas found:** This is a Three.js / R3F scene. Note the size, position
(full-bleed? inset? overlapping content?), and whether it responds to mouse or scroll.

---

### 4E — Ghost wordmark detection (P71)

```javascript
// Find very large, very low opacity text elements
Array.from(document.querySelectorAll('*')).filter(el => {
  const cs = window.getComputedStyle(el);
  return parseFloat(cs.opacity) < 0.12 &&
         parseFloat(cs.opacity) > 0.01 &&
         parseInt(cs.fontSize) > 80 &&
         el.children.length < 3;
}).map(el => {
  const cs = window.getComputedStyle(el);
  return {
    tag: el.tagName,
    cls: (el.className||'').toString().substring(0,60),
    text: (el.innerText||'').trim().substring(0,40),
    opacity: cs.opacity,
    fontSize: cs.fontSize,
    fontWeight: cs.fontWeight,
    position: cs.position,
    parent: el.closest('footer,section,header')?.tagName
  };
}).slice(0,5)
```

---

### 4F — Text selection color

```javascript
// Check if ::selection is customized
const selectionStyles = [];
try {
  Array.from(document.styleSheets).forEach(sh => {
    try {
      Array.from(sh.cssRules).forEach(r => {
        if ((r.selectorText||'').includes('selection')) {
          selectionStyles.push(r.cssText.substring(0,120));
        }
      });
    } catch(e) {}
  });
} catch(e) {}
selectionStyles
```

Custom text selection = brand confidence signal. A `::selection` that matches
the brand accent color is a tell that the designer thought about every state.

---

### 4G — The personality checklist

After running all probes above, score these:

**Identity signals (does the brand have a personality beyond the visual?):**
- [ ] Tab title changes on hover/idle/return (P69)
- [ ] Text selection color matches brand (not browser blue)
- [ ] Keyboard shortcuts exist and are discoverable (P70)
- [ ] 404 page has brand personality (not generic "page not found")
- [ ] Scrollbar styled or hidden (not default grey)
- [ ] Footer has ghost wordmark (P71)
- [ ] Page transition builds the logo (not just a fade)
- [ ] Canvas art responds to mouse position (P68)

**Score: 0–8.** Sites scoring 5+ are made by people who love what they do.
Sites scoring 0–2 are made by people who finished the brief.

---

## PHASE 5 — NON-NEGOTIABLES ASSESSMENT

After completing the full analysis, explicitly evaluate the site against these 10 principles.
Include this section in every spec output.

```markdown
## NON-NEGOTIABLES ASSESSMENT

| Principle | Grade | Evidence |
|---|---|---|
| 1. First 300ms is a sensory event | A/B/C/F | [what happens on load] |
| 2. Type does structural work | A/B/C/F | [largest heading: Xpx, used as X] |
| 3. Every cursor state designed | A/B/C/F | [hover states: geometry or just color?] |
| 4. Color temp is one decision | A/B/C/F | [dark: X, light: X — same temp?] |
| 5. Scroll is authored | A/B/C/F | [scroll-scrubbed elements: X] |
| 6. Sections are moods | A/B/C/F | [section temp shift: felt or not?] |
| 7. Detail nobody asked for | A/B/C/F | [surprise elements: X] |
| 8. Font is a brand decision | A/B/C/F | [fonts used + source + cost] |
| 9. White space held under pressure | A/B/C/F | [emptiest viewport: what's there?] |
| 10. One motion vocabulary | A/B/C/F | [easing curves used: how many?] |

**Overall premium grade:** [A/B/C/F]
[2-sentence verdict]
```

---

## TIPS FOR CATCHING EVERYTHING

1. **Always scroll very slowly** — premium effects are tuned to specific scroll ranges. Big jumps miss intermediate states.

2. **Hover over everything** — premium sites have hover states on elements you wouldn't expect (headings, images, decorative elements). Move the cursor across the ASCII art. Hover the logo. Hover section headings.

3. **Watch the browser tab** — does the title change? Premium studios program it to respond on hover, idle, and return from another tab.

4. **Press keys** — `C`, `G`, `⌘G`, `D`, `T`, `?`. Watch for visual changes. Easter eggs live in keyboard handlers.

5. **Watch the fold boundary** — the most important compositional decisions happen at the very bottom of each viewport. Screenshot at Y = section_bottom - 100px to catch the bleed.

6. **Run cross-fold detection at EVERY section boundary** — not just at the start.

7. **Check z-index layers** — premium compositions rely heavily on layering. Run:
   ```javascript
   Array.from(document.querySelectorAll('*'))
     .filter(el => parseInt(window.getComputedStyle(el).zIndex) > 0)
     .map(el => ({cls: (el.className||'').substring(0,40), z: window.getComputedStyle(el).zIndex, pos: window.getComputedStyle(el).position}))
   ```

8. **Look for `overflow: hidden` on parents** — this is how cross-section reveals are masked. The element is technically larger than its container; the mask creates the "entry" effect.

9. **Test resize behavior at 1240px, 768px, 480px** — premium sites reconceive layout at each breakpoint rather than just stacking.

10. **Check for `will-change`** — it signals which elements are animated and hints at the animation type.

11. **Read the inline `<style>` tags** — frequently premium sites put one-off section-specific styles inline.

12. **For multi-page sites**, navigate between pages and immediately screenshot — the transition is often the most impressive animation on the site.

13. **Highlight some text on the page** — does the selection color match the brand? Custom `::selection` is a mark of obsessive craft.

14. **Scroll to the footer and read every element** — keyboard shortcuts, ghost wordmarks, ASCII art fragments, and easter eggs live in footers. Read the tiny monospace text.

15. **Check `document.title` in the console** — then hover a button and check again. Personality lives in the tab strip.
