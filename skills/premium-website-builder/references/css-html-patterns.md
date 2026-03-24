# CSS/HTML Premium Stack — Reference

Reference for CSS/HTML premium stack. Read this when building non-WebGL sites.

---

## PHASE 4 — COLOR + ATMOSPHERE SYSTEM

### The fundamental rule: color is mood, not branding

Lock the full palette before writing a single selector.
Every section references only these variables — no ad-hoc colors mid-page.

### Premium palette construction rules:

1. **Never use pure `#000` or `#fff`** — always warm or cool variants
   - Near-black: `#0a0a0a` (neutral) / `#0c0a08` (warm) / `#08090c` (cool)
   - Near-white: `#f0ede8` (warm) / `#f8f8f8` (neutral) / `#e8ecf0` (cool)

2. **Maximum 2 accent colors** — one primary, one secondary used sparingly
   - Primary accent: used on preloader, primary CTA, one hover state
   - Secondary: used once or twice across the whole page

3. **Background tones are a gradient in disguise** — even "flat" premium sites
   transition from section to section through 2–3 related shades, not jumps

4. **Color temperature consistency** — all colors in a palette lean the same direction
   - Warm palette: all bg/fg/accent values have orange/yellow undertones
   - Cool palette: all lean blue/green
   - Mixing warm and cool without intent creates "discount" feeling

### Palette presets:

**Warm editorial (allies.studio archetype):**
```css
:root {
  --c-bg:       #fff7ec;  /* cream — never pure white */
  --c-surface:  #f1e5dd;  /* slightly warmer — for cards, panels */
  --c-panel:    #a39b91;  /* taupe — mid bg for panel bridge */
  --c-fg:       #000000;
  --c-muted:    rgba(0,0,0,0.4);
  --c-accent:   #ff0c00;  /* one strong pop — preloader, hover, CTA only */
  --c-accent-2: #abf83e;  /* used ≤2 times total */
}
```

**Dark cinematic (product/tech/immersive):**
```css
:root {
  --c-bg:       #0a0a0a;  /* near-black, NOT pure */
  --c-surface:  #141414;  /* cards, panels */
  --c-fg:       #f0ede8;  /* warm white — NOT pure */
  --c-muted:    rgba(240,237,232,0.4);
  --c-accent:   [single brand color];
  /* ambient gradient on hero bg: */
  /* radial-gradient(ellipse at 30% 40%, #1a1a2e, #0a0a0a 70%) */
}
```

**Neutral prestige (VC/finance/architecture):**
```css
:root {
  --c-bg:       #f5f3ef;  /* warm off-white */
  --c-bg-dark:  #1a1a14;  /* warm near-black */
  --c-fg:       #111111;
  --c-accent:   #c8b89a;  /* gold-leaning neutral — never saturated */
  /* Two bgs only. All contrast comes from typography scale and spacing. */
}
```

---

## PHASE 4B — GRADIENT AND COLOR TRANSITION SYSTEM

### The critical distinction: overlay vs. background transition

**Overlay gradients** (ON top of image/video) — fine at any height:
```css
/* Dark vignette over photo — always top or bottom only, not full bleed */
.hero-overlay {
  background: linear-gradient(to bottom,
    rgba(0,0,0,0) 0%,
    rgba(0,0,0,0) 50%,
    rgba(0,0,0,0.7) 100%
  );
  position: absolute; inset: 0; z-index: 1;
}
```

**Background transitions** — MUST span multiple folds:
```css
/* WRONG — brutal gradient over a single viewport */
.section { background: linear-gradient(#000000, #ffffff); }

/* WRONG — hard cut between dark and light sections */
.section-a { background: #0a0a0a; }
.section-b { background: #f5f3ef; } /* jarring contrast cut */

/* RIGHT — transition lives on the BODY over 200-400vh */
body {
  background: linear-gradient(
    to bottom,
    #0a0a0a   0%,
    #0a0a0a  28%,    /* hero stays dark */
    #0f0d0a  36%,    /* barely starts warming */
    #1c1810  44%,    /* amber shadow enters */
    #3d2b1f  52%,    /* rich brown mid-point */
    #8c6b50  60%,    /* tan shoulder */
    #d4b896  68%,    /* arrives at light */
    #f1e5dd  75%,    /* cream */
    #fff7ec  82%,    /* full cream */
    #fff7ec 100%
  );
}
section { background: transparent; } /* sections reveal the body gradient */
```

### Color bleed techniques:

**Technique 1 — Gradient body (above):**
High-contrast transitions (dark to light) span the body gradient.
Sections are transparent windows into that gradient.
`background-attachment: fixed` adds parallax to the gradient itself.

**Technique 2 — Section slide-over with rounded top:**
```css
/* B doesn't cut A — it slides over it like a card */
.section-b {
  position: relative; z-index: 2;
  margin-top: -5rem;
  border-radius: 1.2rem 1.2rem 0 0;
  background: var(--c-bg-warm);
}
/* The rounded edge + overlap creates a "page turning" feel */
```

**Technique 3 — Ambient glow bleed between sections:**
```css
/* Instead of changing bg, add a glow that colors the space */
.section-transition::before {
  content: '';
  position: absolute; bottom: -20vh; left: 50%;
  transform: translateX(-50%);
  width: 60%; height: 40vh;
  background: radial-gradient(ellipse, var(--c-accent) 0%, transparent 70%);
  opacity: 0.12;
  pointer-events: none;
}
/* The glow "bleeds" into the next section, softening the boundary */
```

**Technique 4 — Clip-path reveal (new color emerges from a point):**
```css
/* A new bg color "grows" from where the user clicked or a CTA position */
.section-reveal {
  clip-path: circle(0% at 50% 100%);
  transition: clip-path 0.8s var(--ease-out);
  background: var(--c-accent);
}
.section-reveal.triggered {
  clip-path: circle(150% at 50% 100%);
}
/* Pairs with IntersectionObserver — trigger when top of section enters viewport */
```

**Technique 5 — Color morph via scroll-driven CSS property:**
```javascript
// A single section morphs its own background as you scroll through it
// (like dvele.io's video scrub but for color)
lenis.on('scroll', ({ scroll }) => {
  const section = document.querySelector('.color-morph');
  const top = section.offsetTop;
  const h = section.offsetHeight;
  const progress = Math.max(0, Math.min(1, (scroll - top) / h));
  // Interpolate between two HSL colors
  const hue = 220 + progress * 40; // blue to purple
  const lightness = 10 + progress * 8;
  section.style.background = `hsl(${hue}, 30%, ${lightness}%)`;
});
```

### Gradient rules — the hard list:

```
OK:  radial-gradient overlay on dark bg — ambient atmosphere
OK:  linear-gradient scrim (top 30% OR bottom 30%) on images
OK:  multi-stop body gradient spanning 200vh+ for dark to light
OK:  subtle noise/grain layer (SVG feTurbulence, opacity 0.04)
OK:  single-color section with box-shadow or glow to soften edge

NEVER: linear-gradient(black, white) — or ANY high-contrast pair — in <300px
NEVER: rainbow or multi-color gradients as background
NEVER: gradient that changes direction mid-page (breaks spatial logic)
NEVER: gradient text unless type is >80px and on plain bg
NEVER: two adjacent sections with gradient each — they'll clash
NEVER: hard cut between #0a0a0a and #ffffff — ALWAYS bridge
```

---

## PHASE 5 — DESIGN SYSTEM (lock before any component)

### Typography system:
```css
:root {
  /* Two fonts maximum. Display serif + clean sans. */
  --f-display: 'Playfair Display', Georgia, serif;  /* identity carrier */
  --f-body:    'Inter', system-ui, sans-serif;       /* function carrier */

  /* Fluid scale — one declaration covers all breakpoints */
  --t-hero:    clamp(72px, 13vw, 220px);  /* fills viewport — BRAVE with scale */
  --t-display: clamp(40px, 6vw, 96px);
  --t-h1:      clamp(28px, 4vw, 64px);
  --t-h2:      clamp(22px, 3vw, 44px);
  --t-body:    clamp(14px, 1.2vw, 17px);
  --t-label:   clamp(10px, 0.85vw, 12px);

  --ls-hero:    -0.04em;   /* tight — hero type is sculpture */
  --ls-display: -0.02em;
  --ls-label:    0.12em;   /* always uppercase at this tracking */

  --lh-hero:  0.88;   /* tight — sculptural */
  --lh-body:  1.65;   /* reading comfort */
}
```

**Typographic composition rules:**
- Mix upright + italic in one headline: `Full-blooded <em>creativity</em> for brands.`
  The italic word carries the emotion. The upright holds the structure.
- Size should feel "slightly too large" — premium is brave, not safe
- Max line width for body: 60-66 characters (approx 38em at body size)
- Weight hierarchy must be visible: heading is always dramatically heavier than sub

### Spacing system:
```css
:root {
  --sp-xs:  clamp(8px,  1vw,  12px);
  --sp-sm:  clamp(16px, 2vw,  24px);
  --sp-md:  clamp(32px, 4vw,  56px);
  --sp-lg:  clamp(64px, 8vw, 120px);
  --sp-xl:  clamp(96px,12vw, 200px);  /* section padding — generous */
}
/* When in doubt: double the whitespace. Premium breathes. */
/* Negative space is a design element, not leftover. */
```

### Motion language (set once, never override):
```css
:root {
  /* Named easings — use these vars everywhere, never hardcode */
  --ease-out:     cubic-bezier(0.22, 1, 0.36, 1);      /* exits, reveals */
  --ease-inout:   cubic-bezier(0.6, 0.14, 0, 1);        /* panels, menus */
  --ease-organic: cubic-bezier(0.18, 0.71, 0.11, 1);    /* "alive" feel */
  --ease-spring:  cubic-bezier(0.34, 1.56, 0.64, 1);    /* magnetic snap */

  /* Duration scale */
  --dur-instant:    0.15s;   /* hover color changes */
  --dur-fast:       0.3s;    /* cursor, button states */
  --dur-normal:     0.6s;    /* card reveals, small entries */
  --dur-slow:       0.9s;    /* text reveals, section entries */
  --dur-cinematic:  1.4s;    /* page transitions, preloader exit */
  --dur-luxury:     2.2s;    /* luxury sites only — ultra-slow */
}
```

---

## PHASE 6 — MANDATORY ELEMENTS

Never skip any of these. They are non-negotiable.

### 1. Preloader (brand color + brand font)
```html
<div id="pre">
  <div class="pre-track"><div class="pre-bar" id="pre-bar"></div></div>
  <span class="pre-word">BRAND.</span>
</div>
<style>
#pre {
  position:fixed;inset:0;z-index:9000;
  background: var(--c-accent); /* preloader IS the brand color */
  display:flex;flex-direction:column;align-items:center;justify-content:center;gap:1.5rem;
  transition: transform var(--dur-cinematic) var(--ease-inout);
}
#pre.done { transform: translateY(-100%); pointer-events: none; }
.pre-word { font-family:'Courier New',mono; font-size:13px;
  letter-spacing:0.5em; text-transform:uppercase; color:white; }
.pre-track { width:200px; height:1px; background:rgba(255,255,255,.15) }
.pre-bar { height:100%; width:0; background:white;
  transition: width 1.1s var(--ease-organic); }
</style>
```

### 2. Custom cursor (desktop only — `pointer: fine` media query)
```css
@media (pointer: fine) {
  body { cursor: none; }
  .cursor-wrap {
    position: fixed; inset: 0; z-index: 500;
    pointer-events: none;
    mix-blend-mode: exclusion; /* auto-inverts on ANY background */
  }
  .cursor-dot {
    position: absolute; width: 10px; height: 10px;
    background: white; border-radius: 50%;
    transform: translate(-50%,-50%);
    transition: width var(--dur-fast) var(--ease-out),
                height var(--dur-fast) var(--ease-out);
  }
  .cursor-ring {
    position: absolute; width: 40px; height: 40px;
    border: 1.5px solid white; border-radius: 50%;
    transform: translate(-50%,-50%);
    transition: width var(--dur-normal) var(--ease-out),
                height var(--dur-normal) var(--ease-out);
  }
  /* Zone states — implement ALL of these */
  body.cur-hover .cursor-dot  { width: 22px; height: 22px; }
  body.cur-hover .cursor-ring { width: 60px; height: 60px; }
  body.cur-drag  .cursor-ring { width: 80px; height: 80px; }
  body.cur-text  .cursor-ring { opacity: 0; } /* reading = ring hides */
  body.cur-play  .cursor-ring { width: 56px; height: 56px; }
}
```

### 3. Smooth scroll — Lenis v1.1.14
```html
<script src="https://cdn.jsdelivr.net/npm/lenis@1.1.14/dist/lenis.min.js"></script>
<script>
const lenis = new Lenis({ lerp: 0.1, smoothWheel: true, syncTouch: false });
;(function raf(t){ lenis.raf(t); requestAnimationFrame(raf); })(0);
</script>
```

### 4. Nav with mix-blend-mode (reads on any background)
```css
.nav {
  position: fixed; top: 0; left: 0; right: 0; z-index: 100;
  mix-blend-mode: exclusion; /* white text inverts on any bg — never disappears */
  transition: transform var(--dur-normal) var(--ease-out);
}
.nav.hidden { transform: translateY(-100%); }
.nav * { color: white !important; } /* exclusion handles contrast automatically */
```

---

## PHASE 6B — SCROLLBAR SYSTEM (P47)

The scrollbar is a design decision, not an afterthought.
It occupies prime real estate on the right edge of the viewport for the entire session.
Most premium sites treat it intentionally — either hiding it completely
or replacing it with something that carries brand meaning.

**The default browser scrollbar is never acceptable on a premium site.**
It conflicts with any custom color scheme, sits on top of compositions,
and signals that the UI was not fully considered.

### Decision tree — which approach to use:

```
Is this a Lenis / smooth-scroll site?
+-- YES -> Hide the native scrollbar entirely (approach A)
|         Then decide: does the page need a scroll signal?
|         +-- Short page (under 3 folds) -> nothing needed, just hide
|         +-- Medium (3-8 folds)         -> hero scroll invitation (approach D)
|         +-- Long (8+ folds)            -> custom progress indicator (B or C)
|
+-- NO (native scroll) -> Style the native scrollbar via CSS (approach E)
                         Use accent color thumb, transparent track
```

---

### Approach A — Fully hidden (allies.studio, ethnocare, most dark sites)

The cleanest, most common premium choice. The cursor and smooth scroll
create enough positional awareness. Nothing competes with the composition.

```css
/* Hide native scrollbar — both Firefox and Webkit */
html {
  scrollbar-width: none;         /* Firefox */
}
html::-webkit-scrollbar {
  display: none;                 /* Chrome, Safari, Edge */
}
/* Lenis scroll still works — Lenis drives scroll via JS, not the native scrollbar */
```

**When to use:** Dark cinematic sites, full-bleed immersive sites, any site where
the right edge is used for composition (section numbers, vertical labels, etc.).

---

### Approach B — Custom thin thumb (lusion.co pattern)

A 4-6px fixed element that moves as a scroll position indicator.
Barely visible — acts like a refined, minimal progress marker.
Appears on the right edge, sized proportionally to page length.

```html
<!-- Place right before </body> -->
<div class="scroll-thumb" id="scrollThumb"></div>
```

```css
.scroll-thumb {
  position: fixed;
  right: 12px;
  top: 0;
  width: 3px;
  border-radius: 3px;
  background: var(--c-fg);     /* matches text color — blends with content */
  opacity: 0.25;
  z-index: 200;
  pointer-events: none;
  transition: opacity 0.3s;
  /* Height and top are set by JS below */
}
/* Slightly more visible on scroll activity */
body.is-scrolling .scroll-thumb { opacity: 0.5; }
```

```javascript
// Size and position the thumb based on scroll position
const thumb = document.getElementById('scrollThumb');
let scrollTimer;

function updateThumb() {
  const scrollTop = window.scrollY || document.documentElement.scrollTop;
  const docH     = document.documentElement.scrollHeight;
  const winH     = window.innerHeight;
  const ratio    = winH / docH;
  const thumbH   = Math.max(ratio * winH, 40); // min 40px
  const thumbTop = (scrollTop / (docH - winH)) * (winH - thumbH);

  thumb.style.height = thumbH + 'px';
  thumb.style.top    = thumbTop + 'px';

  // "Active" class while scrolling
  document.body.classList.add('is-scrolling');
  clearTimeout(scrollTimer);
  scrollTimer = setTimeout(() => document.body.classList.remove('is-scrolling'), 800);
}
window.addEventListener('scroll', updateThumb, { passive: true });
updateThumb(); // set initial position

// If using Lenis, hook into its scroll event instead:
// lenis.on('scroll', ({ scroll, limit }) => {
//   const ratio  = window.innerHeight / document.documentElement.scrollHeight;
//   const thumbH = Math.max(ratio * window.innerHeight, 40);
//   const thumbTop = (scroll / limit) * (window.innerHeight - thumbH);
//   thumb.style.height = thumbH + 'px';
//   thumb.style.top    = thumbTop + 'px';
// });
```

**When to use:** Sites where page length needs signalling but visible chrome would
interrupt the composition. The 3px thumb is subtle — the visitor barely notices it
consciously but always knows where they are.

---

### Approach C — Section progress dots (editorial/VC/portfolio)

Minimal fixed dots on the right side, one per major section.
The active dot fills. Elegant navigation signal, also clickable.

```html
<nav class="section-dots" aria-label="Page sections" id="sectionDots">
  <!-- injected by JS -->
</nav>
```

```css
.section-dots {
  position: fixed;
  right: 20px;
  top: 50%;
  transform: translateY(-50%);
  z-index: 200;
  display: flex;
  flex-direction: column;
  gap: 10px;
  pointer-events: all;
  mix-blend-mode: exclusion; /* reads on any background */
}
.section-dot {
  width: 6px; height: 6px;
  border-radius: 50%;
  background: white;
  opacity: 0.25;
  cursor: pointer;
  transition: opacity 0.3s, transform 0.3s var(--ease-out), height 0.3s var(--ease-out);
  border-radius: 3px;
}
.section-dot.active {
  opacity: 1;
  height: 20px;           /* active dot stretches into a pill */
  transform: none;
}
.section-dot:hover { opacity: 0.7; }
```

```javascript
// Build dots from sections with data-section attribute
const sections = document.querySelectorAll('[data-section]');
const dotsNav  = document.getElementById('sectionDots');

sections.forEach((sec, i) => {
  const dot = document.createElement('button');
  dot.className = 'section-dot';
  dot.setAttribute('aria-label', sec.dataset.section || `Section ${i+1}`);
  dot.addEventListener('click', () => {
    lenis.scrollTo(sec, { duration: 1.2 });
  });
  dotsNav.appendChild(dot);
});

// Update active dot on scroll
const dotEls = dotsNav.querySelectorAll('.section-dot');
const io = new IntersectionObserver(entries => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      const idx = Array.from(sections).indexOf(entry.target);
      dotEls.forEach((d, i) => d.classList.toggle('active', i === idx));
    }
  });
}, { threshold: 0.5 });
sections.forEach(s => io.observe(s));
```

**When to use:** Portfolio sites, VC/finance, any site with 4-8 clearly defined
sections that benefit from direct navigation. mix-blend-mode:exclusion means
the dots read over any background color automatically.

---

### Approach D — Hero scroll invitation (scroll indicator in hero)

Not a scrollbar — a deliberate scroll prompt in the hero that disappears
once the visitor starts scrolling. Creates narrative pull.

Two variants:

**D1 — Vertical text (allies.studio style):**
```html
<div class="scroll-invite">
  <span class="scroll-invite__line"></span>
  <span class="scroll-invite__label">Scroll</span>
</div>
```
```css
.scroll-invite {
  position: absolute;
  bottom: 2rem; right: 2.5rem;
  display: flex; flex-direction: column; align-items: center; gap: 8px;
  writing-mode: vertical-rl;
  font-size: 10px; letter-spacing: 0.2em; text-transform: uppercase;
  color: var(--c-muted);
  opacity: 1;
  transition: opacity 0.5s var(--ease-out);
}
.scroll-invite.hidden { opacity: 0; pointer-events: none; }
.scroll-invite__line {
  display: block;
  width: 1px; height: 40px;
  background: currentColor;
  animation: scrollPulse 1.8s ease-in-out infinite;
}
@keyframes scrollPulse {
  0%, 100% { transform: scaleY(1);   opacity: 0.6; }
  50%       { transform: scaleY(0.3); opacity: 0.15; }
}
```
```javascript
// Hide after first scroll
lenis.on('scroll', ({ scroll }) => {
  document.querySelector('.scroll-invite')?.classList.toggle('hidden', scroll > 60);
});
```

**D2 — Animated arrow / chevron (minimal):**
```html
<div class="scroll-arrow" aria-hidden="true">
  <svg width="20" height="20" viewBox="0 0 20 20" fill="none">
    <path d="M10 4v12M4 10l6 6 6-6" stroke="currentColor" stroke-width="1.5"
          stroke-linecap="round" stroke-linejoin="round"/>
  </svg>
</div>
```
```css
.scroll-arrow {
  position: absolute; bottom: 2rem; left: 50%;
  transform: translateX(-50%);
  color: var(--c-muted);
  animation: arrowBounce 2s ease-in-out infinite;
  opacity: 1; transition: opacity 0.5s;
}
.scroll-arrow.hidden { opacity: 0; }
@keyframes arrowBounce {
  0%, 100% { transform: translateX(-50%) translateY(0); }
  50%       { transform: translateX(-50%) translateY(6px); }
}
```

**When to use:** Every hero section benefits from a scroll invitation — it guides
the eye and communicates that content continues. Always hide it after 60px scroll.

---

### Approach E — Styled native scrollbar (content-heavy sites)

For long-form articles, documentation, and any site with selectable text
content where the scrollbar serves a functional purpose (reader needs to drag it).
Still brand-aligned, never the default grey.

```css
/* Webkit-based (Chrome, Safari, Edge) */
::-webkit-scrollbar {
  width: 6px;             /* thin — not the bulky default */
}
::-webkit-scrollbar-track {
  background: transparent; /* or: var(--c-bg) */
}
::-webkit-scrollbar-thumb {
  background: var(--c-accent);   /* brand color */
  border-radius: 3px;
  /* Fade in — starts near-transparent, solid on hover */
  opacity: 0.3;
}
::-webkit-scrollbar-thumb:hover {
  background: var(--c-fg);
}

/* Firefox */
html {
  scrollbar-width: thin;
  scrollbar-color: var(--c-accent) transparent;
}
```

**Note:** Webkit scrollbar styling is deprecated in the spec but still works
in all Chromium-based browsers. Firefox uses `scrollbar-color` + `scrollbar-width`.
Safari on iOS ignores custom scrollbar styling entirely (no scrollbar shown).

---

### Approach F — Horizontal reading progress bar (editorial/blog/article)

A thin line at the very top of the viewport that fills left-to-right
as the user reads. Signals depth without interrupting layout.

```html
<div class="read-progress" id="readProgress"></div>
```
```css
.read-progress {
  position: fixed;
  top: 0; left: 0;
  width: 0%; height: 2px;        /* 2px — barely there */
  background: var(--c-accent);
  z-index: 9999;
  pointer-events: none;
  transform-origin: left;
  transition: width 0.1s linear; /* fast update — feels live */
}
```
```javascript
lenis.on('scroll', ({ scroll, limit }) => {
  const pct = (scroll / limit) * 100;
  document.getElementById('readProgress').style.width = pct + '%';
});
```

**When to use:** Article pages, case studies, blog posts — anywhere the reader
benefits from knowing how far through the content they are.
Not appropriate for marketing/landing pages (wrong signal — implies length).

---

### Scrollbar decision matrix:

| Site type | Default choice | Why |
|---|---|---|
| Dark cinematic / immersive | A (hidden) | Scrollbar conflicts with composition |
| Brand agency / portfolio | A (hidden) + D (hero invite) | Clean canvas, guided entry |
| Long landing page 8+ folds | B (thin thumb) | Position awareness without visual noise |
| VC / finance / corporate | C (section dots) | Navigation clarity, authoritative |
| Luxury / fashion | A (hidden) | Silence = luxury |
| SaaS / product | B (thin thumb) or E (styled native) | Functional, not decorative |
| Article / editorial | F (progress bar) | Reader benefit |
| 3D / WebGL / immersive | A (hidden) | Nothing competes with the scene |

### Anti-patterns — never do these:

- NEVER leave the default browser scrollbar on a premium site (grey square thumb)
- NEVER use `::-webkit-scrollbar { width: 10px+; }` — thick scrollbars feel 2012
- NEVER style the scrollbar with a color that doesn't exist in the palette
- NEVER add section dots AND a progress bar on the same page — pick one
- NEVER add a scroll invitation to a page with no scroll (hero fills viewport, page ends)
- NEVER animate the scroll indicator with bounce or elastic easing (distracting)

---

## PHASE 7 — COMPOSITION BRIDGES

The #1 differentiator between premium and section-stack sites.
**Every section boundary must have a visual bridge.**

### Bridge A — Rounded slide-over (section B cards over A):
```css
.section-b {
  position: relative; z-index: 2;
  margin-top: -5rem;
  border-radius: 1.2rem 1.2rem 0 0;
  background: var(--c-bg-warm);
}
/* The rounded top + overlap = "page turning" — not a cut */
```

### Bridge B — Gradient body bleed (high-contrast transitions):
```css
/* Body handles the color journey. Sections are transparent. */
body.is-transitioning {
  background: linear-gradient(
    to bottom,
    var(--c-bg) 0%, var(--c-bg) 28%,
    #1c1810 40%, #3d2b1f 50%, #d4b896 62%,
    var(--c-bg-warm) 72%, var(--c-bg-warm) 100%
  );
  background-attachment: fixed;
}
section { background: transparent; }
```

### Bridge C — Ambient glow bleeds across boundaries:
```css
.section::after {
  content: ''; position: absolute; bottom: -15vh; left: 50%;
  transform: translateX(-50%);
  width: 50%; height: 30vh;
  background: radial-gradient(ellipse, var(--c-accent), transparent 70%);
  opacity: 0.08; pointer-events: none;
}
/* Creates a "halo" that spills into the next section */
```

### Bridge D — Typography as mask window (P32):
```html
<section style="position:relative;overflow:hidden;height:100vh">
  <!-- Photo sits at z:1 — visible through letter gaps -->
  <img src="editorial.jpg" style="position:absolute;inset:0;width:100%;height:100%;object-fit:cover;z-index:1">
  <!-- Wordmark at z:2, colored to match section bg — gaps reveal photo -->
  <h1 style="position:relative;z-index:2;font-size:30vw;line-height:0.85;
              color:var(--c-bg);letter-spacing:-0.04em">
    WORDMARK
  </h1>
</section>
```

### Bridge E — Clip-path color reveal:
```css
/* New section's color expands from a focal point (CTA, center, etc.) */
.section-reveal { background: var(--c-new); clip-path: circle(0% at 50% 90%); }
/* Triggered by IntersectionObserver or scroll position: */
.section-reveal.triggered { clip-path: circle(150% at 50% 90%);
  transition: clip-path 1.2s var(--ease-out); }
```

---

## PHASE 8 — MICRO-INTERACTIONS (every state has a response)

Map every interactive state before coding. **The rule: hover is never silent. Every interaction involves geometry — not just color.**

Patterns below are extracted from 15 premium sites. Use the pattern IDs (P48-P67) in your state matrix.

### State matrix (fill out for every project):

| Element | Default | Hover entry | Pattern |
|---|---|---|---|
| Nav link | base color | underline slides in from left | P48 or P49 |
| Primary CTA | border only | bg fills from bottom + text inverts | P50 |
| Work card | flat | img scale + overlay + info lifts | P55 |
| Close btn | 0 deg | rotates 180 deg | P54 |
| Footer CTA | cream | color inverts to accent (surprise) | P50 |
| Arrow on CTA | neutral | scale(1.15) + nudge right | P57 |
| Social icon | default fill | fill changes + bg circle appears | P56 |

---

### P48 — Underline scaleX origin-swap *(allies, creandum, truekind)*

```css
.link { position: relative; display: inline-block; }
.link::after {
  content: ''; position: absolute;
  bottom: -2px; left: 0; width: 100%; height: 1px;
  background: currentColor;
  transform: scaleX(0);
  transform-origin: right center;
  transition: transform 0.4s var(--ease-out);
}
.link:hover::after {
  transform: scaleX(1);
  transform-origin: left center; /* swap origin — grows left-to-right */
}
```

---

### P49 — Underline keyframe slide *(noomo — more dramatic)*

```css
.link { position: relative; overflow: hidden; }
.link::before {
  content: ''; position: absolute;
  bottom: 0; left: 0; width: 100%; height: 1px;
  background: currentColor; transform: translateX(-100%);
}
.link:hover::before { animation: hoverLineIn 0.35s var(--ease-out) both; }
@keyframes hoverLineIn  { from { transform: translateX(-100%); } to { transform: translateX(0); } }
.link.leaving::before   { animation: hoverLineOut 0.25s ease-in both; }
@keyframes hoverLineOut { from { transform: translateX(0); } to { transform: translateX(100%); } }
```

---

### P50 — CTA color inversion *(allies footer, lusion header)*

```css
.cta { background: var(--c-surface); color: var(--c-fg);
  transition: background 0.3s var(--ease-out), color 0.3s; }
.cta:hover { background: var(--c-accent); color: white; }
.cta svg path { fill: currentColor; transition: fill 0.3s; }
```

---

### P51 — Dots scale-zero / text slides in *(lusion "LET'S TALK")*

```css
.btn-dots { transition: transform 0.3s var(--ease-out), opacity 0.3s; }
.btn:hover .btn-dots { transform: scale(0) translateZ(0); opacity: 0; }
.btn-text { transform: translate3d(-1.5em, 0, 0); opacity: 0;
  transition: transform 0.3s var(--ease-out), opacity 0.3s; }
.btn:hover .btn-text { transform: translate3d(0, 0, 0); opacity: 1; }
.btn-arrow { transform: translateX(120%);
  transition: transform 0.3s var(--ease-out) 0.05s; }
.btn:hover .btn-arrow { transform: translateX(0); }
```

---

### P54 — Icon rotate 180 deg *(close / toggle / accordion)*

```css
.icon-close { transition: transform 0.4s var(--ease-out); }
.icon-close:hover { transform: rotate(180deg); }
.accordion.open .toggle { transform: rotate(45deg); }
```

---

### P55 — Card image + overlay + info *(universal premium card)*

```css
.card { overflow: hidden; }
.card-img { transition: transform 0.7s var(--ease-organic); }
.card:hover .card-img { transform: scale(1.05); }
.card-overlay {
  position: absolute; inset: 0; opacity: 0;
  background: linear-gradient(to top, rgba(0,0,0,0.72) 0%, transparent 55%);
  transition: opacity 0.4s var(--ease-out);
}
.card:hover .card-overlay { opacity: 1; }
.card-info { transform: translateY(12px); opacity: 0;
  transition: transform 0.45s var(--ease-out), opacity 0.45s; }
.card:hover .card-info { transform: translateY(0); opacity: 1; }
```

---

### P58 — Variable font weight morph *(bottega53 — luxury)*

```css
.shrink-link {
  font-variation-settings: "wght" 640, "opsz" 20;
  transition: font-variation-settings 0.4s var(--ease-out);
  position: relative;
}
.shrink-link::after { content: ''; position: absolute; bottom: -2px; left: 0;
  width: 100%; height: 1px; background: currentColor;
  transition: width 0.4s var(--ease-out); }
.shrink-link:hover { font-variation-settings: "wght" 240, "opsz" 8; }
.shrink-link:hover::after { width: 0; }
```

---

### P59 — CSS :has() sibling fade *(yodezeen — zero JS)*

```css
.list { }
.item { transition: opacity 0.4s var(--ease-out); }
.list:has(.item:hover) .item:not(:hover) { opacity: 0.4; }
/* Chrome 105+, Safari 15.4+, Firefox 121+ */
@supports not selector(:has(a, b)) { .item:hover { opacity: 1; } }
```

---

### P65 — Text swap dual-span *(aventura dental — premium button)*

```html
<a class="btn-swap" href="#">
  <span>Get in touch</span>
  <span aria-hidden="true">Let's talk</span>
</a>
```
```css
.btn-swap { position: relative; overflow: hidden;
  display: inline-flex; flex-direction: column; }
.btn-swap span { display: block; transition: transform 0.4s var(--ease-out); }
.btn-swap span:last-child { position: absolute; top: 100%; left: 0; width: 100%; }
.btn-swap:hover span:first-child { transform: translateY(-110%); }
.btn-swap:hover span:last-child  { transform: translateY(-110%); }
```

---


### P66 — 3-part CTA split *(good-fella.com — physically separates on hover)*

The button is built from three distinct blocks. On hover, the `+` icon physically separates
leftward, leaving the text as its own pill. Unlike P65 (text swap), this pattern changes
the **geometry** of the button — it becomes two elements instead of one.

```html
<a class="btn-split" href="#">
  <span class="btn-split-inner">
    <span class="btn-icon">+</span>          <!-- Part 1: icon block, 40x40px -->
    <span class="btn-text">SEE OUR PRICING</span> <!-- Part 2: text, flex-1 -->
    <span class="btn-ghost"></span>           <!-- Part 3: invisible at rest -->
  </span>
</a>
```

```css
.btn-split {
  display: inline-flex;
  background: var(--c-accent);
  color: var(--c-fg-dark);
  text-transform: uppercase;
  font-size: 14px; font-weight: 500;
  overflow: hidden;
}
.btn-split-inner {
  display: flex; align-items: stretch;
  width: 100%; position: relative;
}
.btn-icon, .btn-ghost {
  width: 40px; height: 40px;
  display: flex; align-items: center; justify-content: center;
  flex-shrink: 0;
  transition: transform 700ms cubic-bezier(0.22, 1, 0.36, 1);
}
.btn-text {
  flex: 1; padding: 0 12px;
  display: flex; align-items: center; justify-content: center;
  transition: transform 700ms cubic-bezier(0.22, 1, 0.36, 1);
}
.btn-split:hover .btn-icon  { transform: translateX(-100%); }
.btn-split:hover .btn-text  { transform: translateX(-40px); }
```

**Key:** `cubic-bezier(0.22, 1, 0.36, 1)` at 700ms is essential. The long duration +
deceleration creates the satisfying "spring to rest." Too fast = mechanical. Too slow = sluggish.

---

### P67 — Text scramble on hover *(good-fella.com)*

Characters cycle through random glyphs and resolve left-to-right to the final string.
Creates the impression the text is "computing" its answer.

```javascript
class TextScramble {
  constructor(el) {
    this.el = el;
    this.chars = '!<>-_\\/[]{}--=+*^?#';
    this.update = this.update.bind(this);
  }
  setText(newText) {
    const length = Math.max(this.el.innerText.length, newText.length);
    const promise = new Promise(resolve => this.resolve = resolve);
    this.queue = Array.from({length}, (_, i) => ({
      from: this.el.innerText[i] || '',
      to: newText[i] || '',
      start: Math.floor(Math.random() * 8),
      end: Math.floor(Math.random() * 8) + Math.floor(Math.random() * 8),
    }));
    cancelAnimationFrame(this.frameRequest);
    this.frame = 0;
    this.update();
    return promise;
  }
  update() {
    let output = '', complete = 0;
    for (let { from, to, start, end, char } of this.queue) {
      if (this.frame >= end) { complete++; output += to; }
      else if (this.frame >= start) {
        char = Math.random() < 0.28 ? this.chars[Math.floor(Math.random()*this.chars.length)] : (char||from);
        output += '<span class="scramble-char">' + char + '</span>';
      } else { output += from; }
    }
    this.el.innerHTML = output; // NOTE: Only use with trusted/controlled content
    if (complete === this.queue.length) this.resolve();
    else { this.frameRequest = requestAnimationFrame(this.update); this.frame++; }
  }
}
// Usage:
const fx = new TextScramble(btnEl);
btnEl.addEventListener('mouseenter', () => fx.setText(btnEl.dataset.text));
```

```css
.scramble-char { color: var(--c-accent); opacity: 0.7; }
```

**When to use:** Dev/tech brands only. Signals craft and code-adjacency. Wrong for luxury,
beauty, or editorial brands where it reads as gimmicky.

---

### P68 — Canvas ASCII art with mouse spotlight *(good-fella.com)*

A `<canvas>` renders a portrait or product as ASCII characters. Mouse position creates a
"torch effect" — characters near the cursor illuminate. The image exists in two states:
invisible without the cursor, revealed by the visitor's presence.

```javascript
function renderASCII(canvas, imageSrc, options = {}) {
  const {
    fontSize = 8,
    chars = '@#S%?*+;:,.',
    spotRadius = 100,
    baseColor = [105, 103, 105],   // muted
    accentColor = [251, 70, 13],   // brand orange (mid-range)
    highlightColor = [238, 238, 238], // near-white (close)
  } = options;

  const ctx = canvas.getContext('2d');
  let mouseX = -999, mouseY = -999;
  const cols = Math.floor(canvas.width / fontSize);
  const rows = Math.floor(canvas.height / fontSize);

  const img = new Image();
  img.onload = () => {
    const off = Object.assign(document.createElement('canvas'), {width: cols, height: rows});
    off.getContext('2d').drawImage(img, 0, 0, cols, rows);
    const px = off.getContext('2d').getImageData(0, 0, cols, rows).data;
    ctx.font = `${fontSize}px monospace`;

    function draw() {
      ctx.clearRect(0, 0, canvas.width, canvas.height);
      for (let r = 0; r < rows; r++) {
        for (let c = 0; c < cols; c++) {
          const i = (r * cols + c) * 4;
          const bright = (px[i]*0.299 + px[i+1]*0.587 + px[i+2]*0.114) / 255;
          const char = chars[Math.floor((1 - bright) * (chars.length - 1))];
          const cx = c * fontSize, cy = r * fontSize;
          const dist = Math.hypot(cx - mouseX, cy - mouseY);
          const prox = Math.max(0, 1 - dist / spotRadius);
          const [R,G,B] = prox > 0.6 ? highlightColor : prox > 0 ? accentColor : baseColor;
          ctx.fillStyle = `rgb(${R},${G},${B})`;
          ctx.fillText(char, cx, cy);
        }
      }
      requestAnimationFrame(draw);
    }
    draw();
  };
  img.src = imageSrc;
  document.addEventListener('mousemove', e => {
    const r = canvas.getBoundingClientRect();
    mouseX = e.clientX - r.left; mouseY = e.clientY - r.top;
  });
  // Keyboard easter egg: C reshuffles character density map
  document.addEventListener('keydown', e => {
    if (e.key.toLowerCase() === 'c') {
      options.chars = chars.split('').sort(() => Math.random()-0.5).join('');
    }
  });
}
```

**Canvas sizing:** Position in document flow alongside text. The canvas doesn't need to be
full-bleed — it reads as a panel. typical size: 40-60% of viewport width.

---

### P69 — Dynamic tab title as brand voice *(good-fella.com)*

The browser tab title changes based on user behavior. 3 lines of JavaScript, deeply
personal moment. The first thing users see when they switch back to your tab.

```javascript
const T = {
  default: document.title,
  hover:   "Don't be shy, Fella.",      // on CTA hover — playful nudge
  idle:    'Still thinking?',           // after 30s no interaction
  return:  'Welcome back!',            // on visibilitychange visible
};
let idleTimer;
document.querySelectorAll('a,button').forEach(el => {
  el.addEventListener('mouseenter', () => { clearTimeout(idleTimer); document.title = T.hover; });
  el.addEventListener('mouseleave', () => { document.title = T.default; resetIdle(); });
});
document.addEventListener('visibilitychange', () => {
  if (document.visibilityState === 'visible') {
    document.title = T.return;
    setTimeout(() => document.title = T.default, 3000);
  }
});
function resetIdle() {
  clearTimeout(idleTimer);
  idleTimer = setTimeout(() => document.title = T.idle, 30000);
}
resetIdle();
```

**Emoji selection rule:** Use an emoji in the brand's accent color. good-fella uses an
orange square (their brand orange). A blue brand would use a blue square. The emoji renders
next to the favicon — it becomes a second brand touchpoint in the tab strip.

---

### P70 — Keyboard easter eggs *(good-fella.com footer)*

Hidden shortcuts that do visual things. Zero business value, maximum craft signal.
Surface them visibly in the footer as `<kbd>` pills so curious users discover them.

```javascript
const shortcuts = {
  'g': toggleGrid,   // Cmd+G — show 12-column design grid overlay
  'c': randomizeArt, // C — reshuffle ASCII art character map
};
document.addEventListener('keydown', e => {
  const k = e.key.toLowerCase();
  if ((e.metaKey || e.ctrlKey) && k === 'g') { e.preventDefault(); toggleGrid(); }
  else shortcuts[k]?.();
});

function toggleGrid() {
  const g = document.querySelector('.dev-grid') || (() => {
    const el = document.createElement('div');
    el.className = 'dev-grid';
    document.body.appendChild(el);
    return el;
  })();
  g.classList.toggle('active');
}
```

```css
.dev-grid.active {
  position: fixed; inset: 0; z-index: 9999; pointer-events: none;
  background-image: repeating-linear-gradient(
    90deg,
    rgba(255,0,0,0.06) 0, rgba(255,0,0,0.06) calc(100%/12 - 16px),
    transparent calc(100%/12 - 16px), transparent calc(100%/12)
  );
}
kbd {
  background: #333; color: #818; border-radius: 0;
  padding: 2px 5px; font: 12px monospace;
}
```

**The rule:** shortcuts must do something **visually interesting**, not navigate to a page.
Grid overlays, color mode switches, character randomizations — right targets.
"Go to /about" as a keyboard shortcut — wrong target.

---

### P71 — Ghost brand wordmark behind footer *(good-fella.com)*

Massive, very-low-opacity wordmark sits behind all footer content. Creates depth, makes
the footer feel designed rather than obligatory. You sense it rather than see it.

```css
footer { position: relative; overflow: hidden; }

.footer-ghost {
  position: absolute;
  bottom: -0.12em;        /* letterforms touch the footer floor */
  left: -0.02em;
  font-size: clamp(100px, 16vw, 260px);
  font-weight: 900;
  line-height: 1;
  white-space: nowrap;
  color: var(--c-fg);     /* same color as text — opacity does the work */
  opacity: 0.05;          /* 0.04-0.08 is the sweet spot */
  pointer-events: none;
  user-select: none;
  /* Intentionally overflows the container — partial letterforms on edges */
}

.footer-content {
  position: relative;
  z-index: 1;
}
```

**Opacity calibration:**
- `0.03` = invisible (pointless)
- `0.05` = sensed, not seen (correct)
- `0.10` = visible and intentional (different, louder effect)
- `0.15` = decoration, not depth (wrong)

**Size calibration:** The wordmark should be wide enough that letters bleed off both
left and right edges. If it fits within the footer width, it's too small.

---

### MICRO-ANIMATION QUALITY CHECKLIST

**Geometry (every interactive element must change shape, not just color):**
- [ ] Every `<a>` has **geometry** change on hover (not just color)
- [ ] Primary CTA fills from direction (P50), or splits (P66), or swaps text (P65)
- [ ] Cards use scale + overlay + info lift (P55)
- [ ] Close/toggle icons rotate 180 deg (P54)
- [ ] Nav underlines use origin-swap (P48) or keyframe slide (P49)
- [ ] Footer CTA color inverts as surprise (P50)

**Advanced (for studios, agencies, and technical brands):**
- [ ] CTA button has mechanism, not just style — consider P66 split or P67 scramble
- [ ] Variable font? — consider weight morph (P58)
- [ ] List of items? — consider :has() sibling fade (P59)
- [ ] Tab title has brand voice? — P69 on hover + return states
- [ ] Canvas or interactive art? — P68 mouse spotlight
- [ ] Any keyboard shortcuts discoverable in footer? — P70

**Brand depth (the details nobody asked for):**
- [ ] Footer has ghost wordmark behind content — P71
- [ ] Text selection color (`::selection`) matches brand, not browser blue
- [ ] Focus rings match brand, not browser default blue outline
- [ ] 404 page has personality — brand statement, not "page not found"
- [ ] Scrollbar styled (or hidden) — never default grey

**Code hygiene:**
- [ ] No `transition: all` anywhere
- [ ] All easings use named CSS vars — never bare `ease`
- [ ] All durations use named CSS vars — `--dur-fast`, `--dur-normal`, etc.
- [ ] Mobile: hover states disabled on touch devices (`@media (hover: hover)`)
