---
name: premium-website-builder
version: 5
description: >
  Builds premium, award-winning websites — from CSS/HTML all the way to full
  cinematic WebGL experiences. Covers two stacks: (1) CSS/HTML premium stack
  with 74+ documented patterns, color systems, micro-animations, scrollbar
  design, and personality signals (P66–P71: CTA split, text scramble, canvas
  ASCII spotlight, dynamic tab title, keyboard easter eggs, ghost wordmark),
  and (2) Cinematic rendering stack with Three.js/R3F, GLSL shaders, HDRI
  lighting, postprocessing (bloom/grain/DoF), GSAP ScrollTrigger, barba.js
  page transitions, and particle systems. Reverse-engineered from 15+ award-
  winning studios including good-fella.com (SOTD winner) + emotional design
  research (Norman, Aarron Walter). Includes 10 Non-Negotiables framework.

  USE THIS SKILL whenever the user asks to build, design, create, or improve
  a website, landing page, or digital presence — even if they just say "make
  something that looks premium", "like a top agency", "3D experience", "cinematic",
  or "immersive". ALWAYS run Phase 0 intake BEFORE writing any code. Never skip it.
  A startup landing page and a WebGL immersive experience need completely different
  stacks — intake determines which layers to activate.
---

# Premium Website Builder — v3

**The mindset:** Premium is not a pattern checklist. It's an authored experience
with a clear emotional arc and visual composition. It shows taste, restraint, and
obsessive attention to small interactions — all reinforcing one coherent art direction.

The difference between premium and generic is NOT which patterns you use.
It's whether the site feels like a **storyboard + poster** that someone made
with intent, or a component library that someone assembled until it looked full.

---

## PHASE 0 — MANDATORY INTAKE (always run this first)

Never write a single line of CSS until you know the answers to these.
Ask them conversationally — don't paste them as a numbered list.

### The 6 essential questions:

**Q1 — What is this FOR?**
Not just the product type, but the visitor's journey.
→ "SaaS startup" → "What does the visitor do after they land? Sign up? Book a call?"
→ "Portfolio" → "Are you looking for freelance clients or a full-time role?"
→ "Brand agency" → "Is this to attract clients or to win awards?"

**Q2 — What is the ONE action you want from every visitor?**
Everything is designed backward from this single CTA.
Examples: book a call · buy now · apply to work here · feel the brand · get the app

**Q3 — What feeling should the first 3 seconds create?**
This determines hero composition, color temperature, and typography BEFORE anything else.
Get specific — "professional" is not an answer. Push for:
→ "trust and scale" / "surprising and playful" / "quiet luxury" /
   "cinematic and forward-looking" / "warm and human" / "ruthlessly focused"

**Q4 — Who is the visitor and what do they already believe?**
Shapes copy tone, interaction complexity, and how much you need to explain vs. show.
→ B2B decision-makers (skeptical, time-poor) → authority first, features second
→ Creative directors (taste-first) → composition and craft speak louder than copy
→ Consumers (emotional) → feeling first, then rationalization

**Q5 — What assets exist?** (determines if Gemini generation is needed)
```
Logo:        ☐ Y  ☐ N — need to generate SVG wordmark
Colors:      ☐ Y  ☐ N — need to derive from brand personality
Photos:      ☐ Y  ☐ N (partial) — need Gemini Imagen
Video:       ☐ Y  ☐ N — need Gemini Veo 2
Copy:        ☐ Y  ☐ N — need editorial direction
3D models:   ☐ Y  ☐ N — .glb from Blender, or product scans
```

**Q5B — Cinematic stack trigger (ask if any of these come up):**
If the brief uses words like "immersive", "3D", "cinematic", "like a WebGL site",
"interactive 3D", "scroll-driven 3D", "particles", or references sites like
Bruno Simon, Awwwards 3D winners, or similar — ask:

→ "Do you need a 3D WebGL experience, or would a premium CSS/HTML site achieve this?"
→ "What's the target device? WebGL is heavier on mobile."
→ "Do you have a 3D model (.glb / .fbx) or does it need to be created?"

If YES to 3D → activate CINEMATIC LAYERS 0–10 after Phase 5 (design system).
If NO / unsure → stick with CSS/HTML stack (Phases 0–11 sufficient).

**Q6 — Any reference sites, or "feels like X but..."?**
"Like Lusion but warmer" tells you more than a design brief.
If they have no reference: show 3 mood options (dark/cinematic / warm/editorial / clean/bold)
and ask which direction resonates.

### Confirm back before building:
```
"Based on this, here's how I'm approaching it:
- Archetype: [type]
- Emotional arc: [hook feeling] → [proof moment] → [exit desire]
- Color direction: [one sentence, not hex codes yet]
- The signature: [the one pattern that will surprise them — only one]
- Gemini assets needed: [list or 'none — using type-only hero']
Ready to proceed?"
```

If they approve → Phase 1. If they redirect → refine and confirm again.

---

## PHASE 1 — EMOTIONAL ARC (design this before any code)

Premium sites are storyboards, not component libraries.
Write the arc in plain language before touching CSS.

Based on Norman's three-level emotional design model:
- **Visceral** (first 3s) → gut reaction — composition, color, one headline
- **Behavioral** (next 2min) → usability and clarity — proof, navigation, CTA
- **Reflective** (on exit) → meaning and memory — the thing they tell someone else

```
ACT 1 — THE VISCERAL HOOK  (fold 1, 0→100vh)
  Goal: one gut reaction in 3 seconds
  Rules: one headline, one visual (or pure type), zero feature lists
  Design: composition first — focal point, negative space, color temperature
  Norman level: VISCERAL

ACT 2 — THE BRIDGE  (fold 2–3, 100→300vh)
  Goal: transition from feeling to curiosity
  Rules: one big typographic claim + one composition surprise
  Patterns: P33 panel slide / P41 photo score / P07 word opacity scrub / P32 type mask
  Color: bg starts its journey here (begin gradient body transition if dark→light)
  Norman level: VISCERAL → BEHAVIORAL

ACT 3 — THE PROOF  (fold 4–7, 300→700vh)
  Goal: show the work, the product, or the numbers — viscerally, not as a list
  Rules: trust through specificity, not claims. Real names. Real numbers.
  Patterns: P34 video scrub / P36 3D orbit / P22 canvas grid / P44 framed portrait
  Norman level: BEHAVIORAL

ACT 4 — THE HUMAN LAYER  (fold 7–9, 700→900vh)
  Goal: "there's a person on the other side" — connection and warmth
  Rules: warm bg color (P09 inversion), copy tone shifts, P41 editorial photos
  This is where cheap sites have a testimonial carousel. Don't.
  Norman level: BEHAVIORAL → REFLECTIVE

ACT 5 — THE REFLECTIVE CLOSE  (fold 9→end)
  Goal: one clear action + a memory that outlasts the session
  Rules: footer is a destination, not a sitemap. Big type. Personality.
  CTA hover must be surprising — cream→red, text swap, expansion
  Norman level: REFLECTIVE
```

**Stop here. Write one sentence per act before writing any code.**

---

## PHASE 2 — ARCHETYPE + PATTERN SELECTION

Patterns are building blocks — not a checklist to complete.
The goal is ONE thing that surprises the visitor. Two surprises = neither lands.
Sometimes the right move is to evolve an existing pattern or invent one.

### Archetypes and their core approach:

| Archetype | Core tension | Color direction | Signature pattern |
|---|---|---|---|
| BRAND_AGENCY | "Do they have taste?" → show via craft | Warm cream or pure black. Nothing in between. | P41 photo score OR P32 type mask — pick one |
| PRODUCT_PHYSICAL | "Does it look and feel premium?" → staging | Dark base, product emerges from darkness | P34 video scrub — the product orbits on scroll |
| PRODUCT_DIGITAL | "Will this solve my problem?" → clarity + momentum | Clean white or deep dark, strong single accent | P17 horizontal scroll for features — each has a frame |
| PORTFOLIO | "Have they done my kind of work?" → selective confidence | Neutral — work IS the palette | P15 hover video preview on each project row |
| BRAND_CONSUMER | "Will this make me feel something?" → sensory | Warm organic or high-contrast mono | P35 macro texture — ingredient fills the viewport |
| VC_FINANCE | "Can I trust these people?" → authority + restraint | Deep warm near-black + warm off-white. One gold/tan accent. | Numbers that animate from 0 as they scroll in |
| PERSONALITY | "Is this person interesting?" → distinctive voice | Derives from the person — not generic "dark mode" | One real-time live feed (Strava, last album, last match) |
| LUXURY | "Does this feel expensive?" → silence + precision | Black + white + one metallic or deep accent. Ultra-slow. | Variable font morph on key word — weight shifts on hover |
| 3D_IMMERSIVE | "What is this?" → spectacle + discovery | Near-black — objects ARE the color | Mouse-reactive Three.js scene over type (P10/P23) |

### Pattern invention rules (critical — read this):

Applying patterns mechanically produces "premium-looking but generic" sites.
The skill is **knowing when to evolve, invert, or combine**.

**Evolve:** Take a known pattern and push one axis further.
→ P09 (section color inversion) → instead of IntersectionObserver bg swap,
  reveal the new bg color via an expanding clip-path circle from the CTA position

**Invert:** Reverse the spatial logic.
→ P41 (photos float IN around the wordmark) → try photos that float OUT as you scroll,
  leaving the wordmark increasingly exposed and isolated

**Combine:** Merge two patterns into something unnamed.
→ P32 (type as mask) + P07 (word opacity scrub) = letters that are DARK until you
  scroll past them, then each letter illuminates as the photo "fills in" behind it

**Restraint:** Sometimes the right decision is to NOT add a pattern.
→ A luxury site with a single centered product on pure white needs no scroll animations.
  The restraint IS the luxury signal.

---

## PHASE 3 — ASSET AUDIT + GEMINI TRIGGER

Run this before writing HTML. Generate anything marked GENERATE.

```
HERO:
[ ] Full-bleed visual exists?
    → Agency / portfolio: type-only hero (type IS the art — no Gemini needed)
    → Product (physical): needs orbital video (GENERATE VEO 2 — see prompts below)
    → Architecture: needs drone footage (GENERATE VEO 2)
    → Beauty / consumer: needs macro texture (GENERATE IMAGEN 3)
    → Tech / SaaS: can use abstract 3D gradient — CSS only if no assets

BACKGROUND TEXTURES (always generate — they separate premium from flat):
[ ] Grain/noise overlay → GENERATE SVG: feTurbulence noise tile, opacity 0.04–0.08
[ ] Footer texture → GENERATE IMAGEN: aged paper macro, near-black, seamless

SVG DECORATIONS:
[ ] Starburst → GENERATE via Gemini text (see prompt below)
[ ] Organic blob → GENERATE via Gemini text
[ ] Contour lines → GENERATE via Gemini text

BRAND:
[ ] Logo SVG exists? → if N, generate animated path-draw wordmark (SVG stroke-dashoffset)
```

### Gemini generation prompts:

**Macro hero (beauty/consumer) — Imagen 3:**
```
Extreme macro photograph of [ingredient/material], ultra close-up fills entire
frame, individual texture visible, soft diffused golden light, shallow DOF,
commercial beauty brand photography, no text, no face, no hands
```

**Drone orbit (architecture/real estate) — Veo 2:**
```
Smooth aerial drone footage slowly orbiting a [modern/minimalist] [building type],
golden hour warm light, long shadows, camera maintains constant altitude and
rotates counterclockwise 180°, no cuts, 12 seconds, seamless near-loop,
commercial architectural photography quality
```

**Product emergence (dark staging) — Imagen 3:**
```
[Product name/type] on pure matte black background. Single spotlight from
upper-right creates one sharp rim highlight along top edge. No background
shadows, no reflections. Ultra-sharp commercial advertising photography, 8K
```

**SVG starburst — via Gemini text:**
```
Write an SVG starburst element. viewBox="0 0 500 500". Thin lines radiating
from center point (250,250). Vary the line lengths slightly. Stroke: currentColor,
stroke-width: 1.5. Add a CSS class "rotating" with @keyframes that rotates it
one full turn infinitely. Return only the SVG code, no explanation.
```

**Noise texture tile — via Gemini text:**
```
Write an inline SVG with an feTurbulence + feColorMatrix filter that creates
a subtle paper grain texture. The SVG should tile seamlessly at 200×200px.
Opacity should be near-transparent (use as a background overlay). Return only
the SVG code.
```

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
/* ✅ This is fine — it's a supporting layer, not the background itself */
```

**Background transitions** — MUST span multiple folds:
```css
/* ❌ WRONG — brutal gradient over a single viewport */
.section { background: linear-gradient(#000000, #ffffff); }

/* ❌ WRONG — hard cut between dark and light sections */
.section-a { background: #0a0a0a; }
.section-b { background: #f5f3ef; } /* jarring contrast cut */

/* ✅ RIGHT — transition lives on the BODY over 200–400vh */
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
High-contrast transitions (dark → light) span the body gradient.
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
  const hue = 220 + progress * 40; // blue → purple
  const lightness = 10 + progress * 8;
  section.style.background = `hsl(${hue}, 30%, ${lightness}%)`;
});
```

### Gradient rules — the hard list:

```
✅ OK:  radial-gradient overlay on dark bg — ambient atmosphere
✅ OK:  linear-gradient scrim (top 30% OR bottom 30%) on images
✅ OK:  multi-stop body gradient spanning 200vh+ for dark→light
✅ OK:  subtle noise/grain layer (SVG feTurbulence, opacity 0.04)
✅ OK:  single-color section with box-shadow or glow to soften edge

❌ NEVER: linear-gradient(black, white) — or ANY high-contrast pair — in <300px
❌ NEVER: rainbow or multi-color gradients as background
❌ NEVER: gradient that changes direction mid-page (breaks spatial logic)
❌ NEVER: gradient text unless type is >80px and on plain bg
❌ NEVER: two adjacent sections with gradient each — they'll clash
❌ NEVER: hard cut between #0a0a0a and #ffffff — ALWAYS bridge
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
- Max line width for body: 60–66 characters (≈38em at body size)
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
├── YES → Hide the native scrollbar entirely (approach A)
│         Then decide: does the page need a scroll signal?
│         ├── Short page (under 3 folds) → nothing needed, just hide
│         ├── Medium (3–8 folds)         → hero scroll invitation (approach D)
│         └── Long (8+ folds)            → custom progress indicator (B or C)
│
└── NO (native scroll) → Style the native scrollbar via CSS (approach E)
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

A 4–6px fixed element that moves as a scroll position indicator.
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

**When to use:** Portfolio sites, VC/finance, any site with 4–8 clearly defined
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

Patterns below are extracted from 15 premium sites. Use the pattern IDs (P48–P67) in your state matrix.

### State matrix (fill out for every project):

| Element | Default | Hover entry | Pattern |
|---|---|---|---|
| Nav link | base color | underline slides in from left | P48 or P49 |
| Primary CTA | border only | bg fills from bottom + text inverts | P50 |
| Work card | flat | img scale + overlay + info lifts | P55 |
| Close btn | 0° | rotates 180° | P54 |
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
  transform-origin: left center; /* swap origin → grows left-to-right */
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

### P54 — Icon rotate 180° *(close / toggle / accordion)*

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
  <span aria-hidden="true">Let's talk →</span>
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
    <span class="btn-icon">+</span>          <!-- Part 1: icon block, 40×40px -->
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
    this.chars = '!<>-_\\/[]{}—=+*^?#';
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
        output += `<span class="scramble-char">${char}</span>`;
      } else { output += from; }
    }
    this.el.innerHTML = output;
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
full-bleed — it reads as a panel. typical size: 40–60% of viewport width.

---

### P69 — Dynamic tab title as brand voice *(good-fella.com)*

The browser tab title changes based on user behavior. 3 lines of JavaScript, deeply
personal moment. The first thing users see when they switch back to your tab.

```javascript
const T = {
  default: document.title,
  hover:   "Don't be shy, Fella. 🟧",     // on CTA hover — playful nudge
  idle:    'Still thinking? 👀',           // after 30s no interaction
  return:  'Welcome back! 🎉',             // on visibilitychange visible
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

**Emoji selection rule:** Use an emoji in the brand's accent color. good-fella uses 🟧
(orange square = their brand orange). A blue brand would use 🟦. The emoji renders next
to the favicon — it becomes a second brand touchpoint in the tab strip.

---

### P70 — Keyboard easter eggs *(good-fella.com footer)*

Hidden shortcuts that do visual things. Zero business value, maximum craft signal.
Surface them visibly in the footer as `<kbd>` pills so curious users discover them.

```javascript
const shortcuts = {
  'g': toggleGrid,   // ⌘G — show 12-column design grid overlay
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
  opacity: 0.05;          /* 0.04–0.08 is the sweet spot */
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
- [ ] Close/toggle icons rotate 180° (P54)
- [ ] Nav underlines use origin-swap (P48) or keyframe slide (P49)
- [ ] Footer CTA color inverts as surprise (P50)

**Advanced (for studios, agencies, and technical brands):**
- [ ] CTA button has mechanism, not just style — consider P66 split or P67 scramble
- [ ] Variable font? → consider weight morph (P58)
- [ ] List of items? → consider :has() sibling fade (P59)
- [ ] Tab title has brand voice? → P69 on hover + return states
- [ ] Canvas or interactive art? → P68 mouse spotlight
- [ ] Any keyboard shortcuts discoverable in footer? → P70

**Brand depth (the details nobody asked for):**
- [ ] Footer has ghost wordmark behind content → P71
- [ ] Text selection color (`::selection`) matches brand, not browser blue
- [ ] Focus rings match brand, not browser default blue outline
- [ ] 404 page has personality — brand statement, not "page not found"
- [ ] Scrollbar styled (or hidden) — never default grey

**Code hygiene:**
- [ ] No `transition: all` anywhere
- [ ] All easings use named CSS vars — never bare `ease`
- [ ] All durations use named CSS vars — `--dur-fast`, `--dur-normal`, etc.
- [ ] Mobile: hover states disabled on touch devices (`@media (hover: hover)`)
---

## NON-NEGOTIABLES — What separates premium from polished-generic

These 10 principles are synthesized from live analysis of award-winning sites.
They are not patterns to apply — they are standards to judge against.
**If a build violates any of these, it cannot read as premium regardless of other quality.**

### 1. The first 300ms is a sensory event, not a message
Premium sites use the load/entry as an **authored moment** — a flash of brand color,
a logo building itself, an illustration fading in. Nothing happens before something
has already happened. The visitor is inside the brand before they've read a word.

→ Bad: white flash → content appears
→ Good: full-screen brand color → logo animates → content reveals

### 2. Type does structural work, not label work
Headlines are sized and positioned like architectural elements, not text containers.
A heading at 87px with -3px letter-spacing sitting next to a canvas is a column.
A heading at 32px centered above a card grid is a label.

→ Bad: h2 centered above a card grid, 36px, weight 700, bottom margin 24px
→ Good: h1 at 87px overflowing the viewport, positioned to cross a split boundary

### 3. Every cursor state is designed
The single biggest tell between premium and not. Nothing is static under the cursor.
Every interactive zone has a **geometric** response — not just color change.

→ Bad: `color: var(--primary)` on link hover
→ Good: text scrambles, splits, swaps, grows, or reveals a second element

### 4. Color temperature is one decision, not a palette
One atmospheric choice applied consistently. Never pure `#000` or pure `#fff`.
All surfaces shifted toward the same warmth or coolness.

→ Bad: `#141414` dark sections, `#ffffff` light sections
→ Good: `#141314` (warm dark) and `#eee` (warm white) — identical temperature

### 5. Scroll is authored, not navigated
Every scroll unit spent on a designed reveal. If you can scroll through a section
without anything changing except position, that section is not earned.

→ Bad: sections fade in with IntersectionObserver opacity 0→1
→ Good: active process step tracks scroll position, photo panel swaps, sticky portrait

### 6. Sections are moods, not containers
Each section has a distinct emotional temperature that shifts the visitor's state
before they read a word. The shift should feel like entering a different room.

→ Bad: all sections same light grey background, content swaps
→ Good: warm editorial → near-black studio → silhouette against gradient

### 7. The detail nobody asked for
At least one element exists purely because it's delightful, not because it converts.
Keyboard shortcuts, ASCII art, tab title changes, ghost wordmarks, selection colors.
This is the most reliable signal that the site was made by people who love what they do.

→ Bad: every element has a conversion purpose
→ Good: `C` key reshuffles the ASCII art; tab says "Don't be shy, Fella. 🟧" on hover

### 8. Font loading is a brand decision, not a default
Premium sites never use a widely-used free font as the display face.
The font is a budget line item. The cost makes the distinctiveness possible.

→ Bad: Inter + Playfair Display (Google Fonts, seen on 200,000 sites)
→ Good: aktiv-grotesk (Adobe Fonts, $), BerlingskeSerif (paid), custom variable font

### 9. White space is held under pressure
The ability to hold empty space without discomfort is the clearest indicator of
design confidence. Amateurs fill space. Premium designers hold it.

→ Bad: every viewport has something in every quadrant
→ Good: couple's names separated by 900px of intentional nothing

### 10. Motion has one vocabulary per site
2–3 named easing curves maximum, applied to every animation. Inconsistent easings
are the motion equivalent of using 8 different font weights.

→ Bad: `ease`, `ease-in-out`, `0.3s`, `cubic-bezier(0.4,0,0.2,1)`, all mixed
→ Good: `--ease-out-quint: cubic-bezier(0.22,1,0.36,1)` used everywhere, 700ms

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
| Touch target | Whatever size | Min 44×44px |
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

---

## REFERENCE: Pattern library index

All 67+ patterns + cinematic layers in references/pattern_library.md.
Quick lookup:

```
CURSOR:     P14 magnetic  P46 3D tilt  (types A–E in cursor catalog)
BRIDGES:    P01 split     P03 bleed    P32 type-mask  P33 panel  P39 cross-fold
SCROLL:     P07 word-fade P17 horiz    P18 card-peel  P34 video-scrub
COLOR:      P09 inversion P31 blend-nav
HERO:       P05 portal    P10 3D-over-type P35 macro  P36 product-emerge
MOTION:     P20 stagger   P21 SVG-draw P04 marquee
BRAND:      P25 preloader P26 ambient  P37 pixel-font P38 dual-counter
SCROLLBAR:  P47 hidden   P47 thin-thumb P47 section-dots P47 hero-invite P47 progress-bar
MICRO-ANIM: P48 underline-scalex  P49 underline-keyframe  P50 cta-inversion
            P51 dots-scale-zero   P54 icon-rotate         P55 card-3layer
            P58 variable-font     P59 has-sibling-fade    P65 text-swap-dual
            P66 cta-split-3part   P67 text-scramble       P68 canvas-ascii-spotlight
PERSONALITY:P69 tab-title-voice   P70 keyboard-easter-egg P71 ghost-footer-wordmark
CINEMATIC:
  Layer 0: Architecture overview (CSS/HTML → GPU layers)
  Layer 1: Three.js / R3F setup (renderer, Draco, HDRI, GLTF loader)
  Layer 2: Scene (camera keyframes, HDRI lighting, time-of-day presets)
  Layer 3: GLSL shaders (distortion, gradient noise, glass material)
  Layer 4: Postprocessing (bloom, DoF, grain, vignette, color grade)
  Layer 5: Scroll orchestration (Lenis + GSAP ScrollTrigger pipeline)
  Layer 6: Typography (font foundries, variable fonts, GSAP SplitType, SVG type)
  Layer 7: Particles (Three.js Points, atmospheric dust, sakura)
  Layer 8: Page transitions (barba.js, panel wipe, morph, fade)
  Layer 9: Performance rules (budget, mobile fallback, LOD, dispose)
  Layer 10: Modern stack (Next.js, R3F, Zustand, Draco, Vercel)
```

---

# CINEMATIC RENDERING STACK — ADVANCED LAYER SYSTEM

This is the system underneath the most visually impressive agency sites.
Not every site needs it. But when the brief calls for "cinematic", "immersive",
or "3D experience" — this is the architecture to reach for.

**Decision gate — when to use the cinematic stack:**
```
Does the site need:
  [ ] 3D objects / environments?             → YES: use WebGL layer
  [ ] Scroll-driven 3D camera movement?      → YES: use Lenis + ScrollTrigger + Three.js
  [ ] Custom shaders (water, glass, distort)?→ YES: use GLSL layer
  [ ] Postprocessing (bloom, grain, DoF)?    → YES: use EffectComposer
  [ ] Page transitions (no hard reload)?     → YES: use barba.js
  [ ] Particle systems?                      → YES: use Three.js Points / GPUComputationRenderer
  [ ] Realistic lighting / reflections?      → YES: use HDRI

All NO → use CSS/HTML stack only (Phases 0–11 above are sufficient)
Any YES → add the layers below on top of the CSS/HTML foundation
```

---

## CINEMATIC LAYER 0 — ARCHITECTURE OVERVIEW

Every cinematic site is built from stacked layers, each with a clear responsibility.
Never mix responsibilities across layers.

```
┌─────────────────────────────────────────────────────────┐
│  LAYER 7 — UI + DOM                                     │
│  HTML/CSS, custom cursor, nav, overlays, micro-anim     │
├─────────────────────────────────────────────────────────┤
│  LAYER 6 — TYPOGRAPHY                                   │
│  Variable fonts, SVG type, GSAP text splits             │
├─────────────────────────────────────────────────────────┤
│  LAYER 5 — SCROLL ORCHESTRATION                         │
│  Lenis → normalized 0–1 value → GSAP timelines          │
├─────────────────────────────────────────────────────────┤
│  LAYER 4 — POSTPROCESSING                               │
│  EffectComposer: bloom, DoF, motion blur, grain, grade  │
├─────────────────────────────────────────────────────────┤
│  LAYER 3 — SHADERS (GLSL)                               │
│  Custom materials: water, glass, distortion, gradients  │
├─────────────────────────────────────────────────────────┤
│  LAYER 2 — SCENE                                        │
│  Three.js: camera, lights, meshes, HDRI env map         │
├─────────────────────────────────────────────────────────┤
│  LAYER 1 — RENDERING ENGINE                             │
│  Three.js WebGLRenderer (or WebGPURenderer next-gen)    │
├─────────────────────────────────────────────────────────┤
│  LAYER 0 — GPU                                          │
│  WebGL context / WebGPU context (hardware acceleration) │
└─────────────────────────────────────────────────────────┘
```

The canvas lives BEHIND the DOM. The DOM lives on top with `pointer-events: none`
on everything except interactive elements.

---

## CINEMATIC LAYER 1 — RENDERING ENGINE SETUP

### Three.js core setup (vanilla — works in any stack)
```javascript
import * as THREE from 'three';
import { GLTFLoader }  from 'three/examples/jsm/loaders/GLTFLoader.js';
import { DRACOLoader } from 'three/examples/jsm/loaders/DRACOLoader.js';
import { RGBELoader }  from 'three/examples/jsm/loaders/RGBELoader.js';

// Renderer — behind the DOM
const renderer = new THREE.WebGLRenderer({
  antialias: true,
  alpha: true,        // transparent bg — DOM layers over it
  powerPreference: 'high-performance',
});
renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2)); // cap at 2 — perf
renderer.setSize(window.innerWidth, window.innerHeight);
renderer.toneMapping = THREE.ACESFilmicToneMapping; // cinematic color grading
renderer.toneMappingExposure = 1.2;
renderer.shadowMap.enabled = true;
renderer.shadowMap.type = THREE.PCFSoftShadowMap;
renderer.outputColorSpace = THREE.SRGBColorSpace;

// Canvas behind everything
const canvas = renderer.domElement;
canvas.style.position = 'fixed';
canvas.style.inset = '0';
canvas.style.zIndex = '0';       // behind DOM
canvas.style.pointerEvents = 'none';
document.body.prepend(canvas);

// Scene
const scene = new THREE.Scene();
const camera = new THREE.PerspectiveCamera(
  45,                                    // FOV — 35–50 for architectural/product
  window.innerWidth / window.innerHeight,
  0.1,
  1000
);
camera.position.set(0, 0, 5);
```

### Asset loading with Draco compression
```javascript
// Draco reduces .glb file size by 80–95%
const dracoLoader = new DRACOLoader();
dracoLoader.setDecoderPath('https://www.gstatic.com/draco/versioned/decoders/1.5.6/');

const gltfLoader = new GLTFLoader();
gltfLoader.setDRACOLoader(dracoLoader);

gltfLoader.load('/models/product.glb', (gltf) => {
  const model = gltf.scene;
  // Optimize: merge geometries, dispose unused
  model.traverse(child => {
    if (child.isMesh) {
      child.castShadow = true;
      child.receiveShadow = true;
      child.material.envMapIntensity = 1.2; // HDRI reflection strength
    }
  });
  scene.add(model);
});
```

### React Three Fiber (R3F) setup — for Next.js / React projects
```jsx
// npm install three @react-three/fiber @react-three/drei
import { Canvas } from '@react-three/fiber';
import { Environment, useGLTF, PresentationControls } from '@react-three/drei';

// R3F declarative scene — same Three.js under the hood
export default function Scene() {
  return (
    <Canvas
      camera={{ position: [0, 0, 5], fov: 45 }}
      gl={{ antialias: true, toneMapping: THREE.ACESFilmicToneMapping }}
      style={{ position: 'fixed', inset: 0, zIndex: 0 }}
    >
      <Environment preset="studio" />   {/* HDRI from Drei's presets */}
      <ambientLight intensity={0.5} />
      <ProductModel />
    </Canvas>
  );
}
```

---

## CINEMATIC LAYER 2 — SCENE COMPOSITION

### HDRI lighting (replaces fake lights — critical for realism)
```javascript
// HDRI = 360° environment map — provides realistic reflections + lighting
const rgbeLoader = new RGBELoader();
rgbeLoader.load('/hdri/studio_warm.hdr', (texture) => {
  texture.mapping = THREE.EquirectangularReflectionMapping;
  scene.environment = texture; // applies to ALL materials with envMap
  // scene.background = texture; // if you want the HDR as visible backdrop
});

// HDRI sources:
// - Poly Haven (polyhaven.com) — free, commercial use
// - HDR Haven
// - Custom baked in Blender
```

### Lighting presets (time-of-day moods)
```javascript
const LIGHTING = {
  // Morning — warm, low angle
  morning: {
    ambientColor:     0xfff4e0,  ambientIntensity: 0.4,
    directionalColor: 0xffb347,  directionalIntensity: 1.2,
    directionalPos:   [-5, 3, 5],
    hdri: '/hdri/morning_golden.hdr',
  },
  // Studio — neutral, controlled
  studio: {
    ambientColor:     0xffffff,  ambientIntensity: 0.6,
    directionalColor: 0xfff0e8,  directionalIntensity: 1.0,
    directionalPos:   [5, 8, 5],
    hdri: '/hdri/studio_soft.hdr',
  },
  // Night — deep, moody
  night: {
    ambientColor:     0x1a1a2e,  ambientIntensity: 0.2,
    directionalColor: 0x4444ff,  directionalIntensity: 0.4,
    directionalPos:   [0, 10, -5],
    hdri: '/hdri/night_city.hdr',
  },
};

function applyLighting(preset) {
  const L = LIGHTING[preset];
  ambientLight.color.setHex(L.ambientColor);
  ambientLight.intensity = L.ambientIntensity;
  // Transition via GSAP for time-of-day shifts
  gsap.to(renderer, { toneMappingExposure: preset==='night' ? 0.7 : 1.2, duration: 2 });
}
```

### Camera system — scroll-linked cinematic movement
```javascript
import gsap from 'gsap';
import ScrollTrigger from 'gsap/ScrollTrigger';

// Camera keyframes — define where the camera is at each scroll position
const CAM_KEYFRAMES = [
  { progress: 0,    pos: [0, 0, 5],    target: [0, 0, 0] },  // hero
  { progress: 0.25, pos: [3, 1, 3],    target: [0, 0, 0] },  // right reveal
  { progress: 0.5,  pos: [0, 2, -2],   target: [0, 0, 0] },  // top-down
  { progress: 0.75, pos: [-3, 0.5, 3], target: [0, 0, 0] },  // left orbit
  { progress: 1.0,  pos: [0, 0, 5],    target: [0, 0, 0] },  // back to start
];

// Lerp camera to target each frame (organic feel — not instant snap)
const camTarget = { pos: new THREE.Vector3(0,0,5), lookAt: new THREE.Vector3() };

lenis.on('scroll', ({ progress }) => {
  // Find which keyframe segment we're in
  const kf = getKeyframeAtProgress(progress, CAM_KEYFRAMES);
  camTarget.pos.set(...kf.pos);
  camTarget.lookAt.set(...kf.target);
});

// In render loop — lerp creates the smooth camera motion
function tick() {
  camera.position.lerp(camTarget.pos, 0.05);   // 0.05 = heavy, cinematic lag
  camera.lookAt(camTarget.lookAt);
  requestAnimationFrame(tick);
}
```

---

## CINEMATIC LAYER 3 — SHADERS (GLSL)

Shaders are where premium = custom math. The browser runs GLSL directly on the GPU.
Every visual effect that looks impossible in CSS is a shader.

### Shader structure (always the same two files)
```glsl
/* vertex.glsl — runs once per vertex, sets position */
varying vec2 vUv;       /* passes UV to fragment shader */
varying vec3 vNormal;

void main() {
  vUv = uv;
  vNormal = normalize(normalMatrix * normal);
  gl_Position = projectionMatrix * modelViewMatrix * vec4(position, 1.0);
}
```

```glsl
/* fragment.glsl — runs once per pixel, sets color */
uniform float uTime;    /* time since start — for animation */
uniform vec2 uResolution;
varying vec2 vUv;

void main() {
  /* Color output */
  gl_FragColor = vec4(vUv.x, vUv.y, 0.5, 1.0); /* gradient from UV */
}
```

### Common premium shader recipes

**Distortion (hover ripple, portal effect):**
```glsl
/* fragment.glsl */
uniform sampler2D uTexture;
uniform float uTime;
uniform float uDistortion;  /* 0→1 on hover */
varying vec2 vUv;

void main() {
  /* Wave distortion */
  vec2 distortedUV = vUv;
  distortedUV.x += sin(vUv.y * 10.0 + uTime) * 0.02 * uDistortion;
  distortedUV.y += cos(vUv.x * 10.0 + uTime) * 0.02 * uDistortion;
  
  vec4 color = texture2D(uTexture, distortedUV);
  gl_FragColor = color;
}
```

**Gradient noise (organic backgrounds):**
```glsl
/* Classic Perlin noise for fluid, organic gradient bg */
float noise(vec2 p) {
  return fract(sin(dot(p, vec2(127.1, 311.7))) * 43758.5453);
}
void main() {
  float n = noise(vUv * 3.0 + uTime * 0.1);
  vec3 colorA = vec3(0.04, 0.04, 0.04); /* near-black */
  vec3 colorB = vec3(0.12, 0.08, 0.05); /* warm dark */
  gl_FragColor = vec4(mix(colorA, colorB, n), 1.0);
}
```

**Glass / frosted material:**
```javascript
// Three.js MeshPhysicalMaterial — no custom shader needed
const glassMaterial = new THREE.MeshPhysicalMaterial({
  transmission:       1.0,   // 0=opaque, 1=fully transparent
  thickness:          0.5,
  roughness:          0.05,
  ior:                1.5,   // index of refraction (glass = 1.5)
  envMapIntensity:    1.5,
  transparent:        true,
});
```

### Connecting shader uniforms to scroll/mouse
```javascript
// Shader material with live uniforms
const shaderMaterial = new THREE.ShaderMaterial({
  uniforms: {
    uTime:       { value: 0 },
    uMouse:      { value: new THREE.Vector2(0.5, 0.5) },
    uDistortion: { value: 0 },
    uTexture:    { value: textureLoader.load('/img/hero.jpg') },
  },
  vertexShader:   vertexGLSL,
  fragmentShader: fragmentGLSL,
});

// Update each frame
function tick(t) {
  shaderMaterial.uniforms.uTime.value = t * 0.001;
  renderer.render(scene, camera);
  requestAnimationFrame(tick);
}

// Distortion on hover (P50 but for 3D)
document.addEventListener('mousemove', e => {
  shaderMaterial.uniforms.uMouse.value.set(
    e.clientX / window.innerWidth,
    1.0 - e.clientY / window.innerHeight
  );
});
```

---

## CINEMATIC LAYER 4 — POSTPROCESSING

Postprocessing = the camera's "film" processing. Renders the 3D scene, then passes
it through a chain of effects before displaying on screen.

```
Raw 3D render → Bloom → Depth of Field → Motion Blur → Film Grain → Color Grade → Screen
```

### Setup with `postprocessing` library (recommended over Three.js EffectComposer)
```javascript
// npm install postprocessing
import { EffectComposer, RenderPass, EffectPass,
         BloomEffect, DepthOfFieldEffect, NoiseEffect,
         VignetteEffect, ChromaticAberrationEffect,
         ToneMappingEffect } from 'postprocessing';

const composer = new EffectComposer(renderer);
composer.addPass(new RenderPass(scene, camera)); // always first

// BLOOM — makes bright areas glow (essential for dark cinematic sites)
const bloom = new BloomEffect({
  intensity:    0.8,
  threshold:    0.85, // only pixels brighter than this bloom
  smoothing:    0.2,
  kernelSize:   KernelSize.MEDIUM,
});

// DEPTH OF FIELD — background blur (luxury product photography feel)
const dof = new DepthOfFieldEffect(camera, {
  focalLength: 0.048,
  bokehScale:  3.0,
  height:      480,
});

// FILM GRAIN — texture, not flatness
const grain = new NoiseEffect({ premultiply: true, blendFunction: BlendFunction.ADD });
grain.blendMode.opacity.value = 0.08; // subtle — just enough

// VIGNETTE — darkens edges, focuses attention on center
const vignette = new VignetteEffect({ eskil: false, offset: 0.4, darkness: 0.6 });

// CHROMATIC ABERRATION — slight color fringe (film camera feel)
const aberration = new ChromaticAberrationEffect({ offset: new THREE.Vector2(0.001, 0.001) });

// CINEMATIC COLOR GRADE preset — warm contrast
const toneMap = new ToneMappingEffect({ mode: ToneMappingMode.ACES_FILMIC });

// Combine into one pass (more efficient than separate passes)
composer.addPass(new EffectPass(camera, bloom, grain, vignette, toneMap));

// Replace renderer.render() with:
function tick() {
  composer.render(); // uses composer instead of renderer
  requestAnimationFrame(tick);
}
```

### Postprocessing presets for different archetypes

```javascript
const POSTPROCESS_PRESETS = {
  // Dark product/tech — maximum cinematic
  DARK_CINEMATIC: {
    bloomIntensity: 1.2, bloomThreshold: 0.8,
    grainOpacity: 0.1, vignetteOffset: 0.5, vignetteDarkness: 0.7,
    aberrationOffset: 0.001,
  },
  // Luxury/fashion — subtle, almost invisible
  LUXURY_MINIMAL: {
    bloomIntensity: 0.3, bloomThreshold: 0.95,
    grainOpacity: 0.04, vignetteOffset: 0.3, vignetteDarkness: 0.3,
    aberrationOffset: 0,
  },
  // Architecture — clean, daylight
  ARCHITECTURE: {
    bloomIntensity: 0.5, bloomThreshold: 0.9,
    grainOpacity: 0.06, vignetteOffset: 0.25, vignetteDarkness: 0.2,
    aberrationOffset: 0,
  },
  // 3D Immersive — full effect stack
  IMMERSIVE_3D: {
    bloomIntensity: 1.5, bloomThreshold: 0.75,
    grainOpacity: 0.12, vignetteOffset: 0.6, vignetteDarkness: 0.8,
    aberrationOffset: 0.002,
  },
};
```

---

## CINEMATIC LAYER 5 — SCROLL ORCHESTRATION

This is the nervous system of the cinematic site.
Everything animates in response to scroll — the scroll value is the single source of truth.

### The architecture
```
User scroll input
    ↓
Lenis (virtual scroll — adds inertia, smoothness, lerp)
    ↓
Normalized progress (0 → 1, never raw pixels)
    ↓
GSAP ScrollTrigger (maps sections to timelines)
    ↓
Branches simultaneously to:
  ├── Three.js scene (camera pos, object rotations)
  ├── DOM animations (text reveals, section fades)
  ├── Shader uniforms (distortion, color shifts)
  └── CSS custom properties (gradient pos, blur amount)
```

### Lenis + GSAP ScrollTrigger integration (the canonical setup)
```javascript
import Lenis from 'lenis';
import gsap from 'gsap';
import ScrollTrigger from 'gsap/ScrollTrigger';
gsap.registerPlugin(ScrollTrigger);

// Lenis setup
const lenis = new Lenis({
  lerp:        0.08,   // 0.05 = very heavy/cinematic, 0.15 = snappy
  smoothWheel: true,
  syncTouch:   false,  // native scroll on mobile
});

// CRITICAL: hook Lenis into GSAP's RAF (they share the same animation frame)
lenis.on('scroll', ScrollTrigger.update);
gsap.ticker.add((time) => lenis.raf(time * 1000));
gsap.ticker.lagSmoothing(0);

// Expose the normalized scroll progress globally for Three.js use
let scrollProgress = 0;
lenis.on('scroll', ({ progress }) => { scrollProgress = progress; });
```

### ScrollTrigger timeline patterns

**Scene-pinned scroll animation (the signature cinematic technique):**
```javascript
// A section is 500vh tall — visitor scrolls through it like a movie timeline
const heroTl = gsap.timeline({
  scrollTrigger: {
    trigger:  '#hero-scene',
    start:    'top top',
    end:      '+=400%',    // 4× viewport height = 400vh of scroll
    scrub:    1.5,         // scrub:1.5 = 1.5s lag behind scroll (more cinematic)
    pin:      true,        // pin the section while scrolling through it
  }
});

heroTl
  // Phase 1: camera pulls back, type fades in
  .to(camera.position, { z: 8, duration: 1 }, 0)
  .from('.hero-title', { opacity: 0, y: 40, duration: 0.5 }, 0.2)

  // Phase 2: camera orbits right, product rotates
  .to(camera.position, { x: 3, z: 5, duration: 1 }, 1)
  .to(product.rotation, { y: Math.PI * 0.25, duration: 1 }, 1)

  // Phase 3: deep zoom in, fade to black
  .to(camera.position, { z: 1.5, duration: 1 }, 2)
  .to('.hero-overlay', { opacity: 1, duration: 0.5 }, 2.5);
```

**Text reveal stagger (P42 + GSAP SplitText):**
```javascript
import SplitType from 'split-type'; // lightweight SplitText alternative

const split = new SplitType('.reveal-text', { types: 'words,chars' });

gsap.from(split.chars, {
  scrollTrigger: {
    trigger: '.reveal-text',
    start: 'top 80%',
    end: 'top 20%',
    scrub: true,
  },
  opacity: 0,
  y: '120%',
  rotateX: -90,
  stagger: 0.02,
  ease: 'none',
});
```

**Horizontal scroll section:**
```javascript
const panels = gsap.utils.toArray('.h-panel');
gsap.to(panels, {
  xPercent: -100 * (panels.length - 1),
  ease: 'none',
  scrollTrigger: {
    trigger: '.h-scroll-container',
    pin: true,
    scrub: 1,
    end: () => '+=' + document.querySelector('.h-scroll-container').offsetWidth,
  },
});
```

---

## CINEMATIC LAYER 6 — TYPOGRAPHY SYSTEM

### Premium font sources (hierarchy by exclusivity)
```
TIER 1 — Custom / Commissioned      → Only the client has it. Maximum brand identity.
TIER 2 — Independent foundries       → Rarely seen on other sites
  • Pangram Pangram (PP Neue Montreal, PP Editorial New)
  • Klim Type Foundry (Domaine, Feijoa)
  • Colophon Foundry (Aperçu, Raisonne)
  • Commercial Type (Graphik, Canela)
  • Grilli Type (GT America, GT Walsheim, GT Super)
  • Production Type (Romain BP, Antique Legacy)

TIER 3 — Adobe Fonts / Typekit       → Good quality, less exclusive
TIER 4 — Google Fonts                → Free but seen everywhere — use only if variable font
  • Recommended: DM Sans, Inter, Plus Jakarta Sans (all variable)
  • Display: Playfair Display, Fraunces (variable), Cormorant

NEVER: Poppins, Montserrat, Open Sans, Raleway on premium sites
These are instantly recognizable as template fonts.
```

### Variable font configuration
```css
/* Variable font setup — full axis control */
@font-face {
  font-family: 'GT America';
  src: url('/fonts/GTAmerica-Variable.woff2') format('woff2-variations');
  font-weight: 100 900;
  font-display: swap;
}

:root {
  /* Base: normal weight */
  --font-weight-display: 'wght' 400, 'wdth' 100;
  /* Hero: heavy + condensed */
  --font-weight-hero:    'wght' 800, 'wdth' 85, 'opsz' 72;
  /* Caption: light + wide */
  --font-weight-caption: 'wght' 300, 'wdth' 110, 'opsz' 12;
}

.hero-title {
  font-variation-settings: var(--font-weight-hero);
  /* Axes available depend on the font: wght, wdth, opsz, slnt, GRAD */
}
```

### GSAP text animations (beyond CSS)
```javascript
import gsap from 'gsap';
import SplitType from 'split-type';

// Word-by-word reveal with 3D rotation (premium feel)
function revealText(selector) {
  const split = new SplitType(selector, { types: 'words' });
  return gsap.from(split.words, {
    opacity:  0,
    y:        '100%',
    rotateX: -90,
    transformOrigin: '0% 50% -50px',
    stagger:  0.06,
    duration: 0.8,
    ease: 'power3.out',
    scrollTrigger: { trigger: selector, start: 'top 75%' },
  });
}

// Variable font weight animation (P58 but scroll-driven)
gsap.to('.display-heading', {
  scrollTrigger: { trigger: '.display-heading', scrub: true, start: 'top bottom', end: 'top top' },
  onUpdate: function() {
    const p = this.progress();
    const wght = gsap.utils.interpolate(200, 800, p);
    document.querySelector('.display-heading').style.fontVariationSettings = `"wght" ${wght}`;
  }
});
```

### SVG typography (hero wordmarks)
```html
<!-- SVG text = vector shape, not a font — total control, no font loading -->
<svg class="hero-wordmark" viewBox="0 0 1200 200">
  <text
    x="0" y="160"
    font-family="sans-serif"
    font-size="180"
    font-weight="800"
    letter-spacing="-8"
    fill="currentColor"
  >STUDIO</text>
</svg>
```

```javascript
// Animate SVG text stroke as path draw (P21)
gsap.from('.hero-wordmark text', {
  strokeDashoffset: '100%',
  duration: 2,
  ease: 'power2.inOut',
});
```

---

## CINEMATIC LAYER 7 — PARTICLES + ATMOSPHERE

### Particle system (Three.js Points)
```javascript
// Dust / floating particles for atmosphere
function createParticles(count = 2000) {
  const geometry = new THREE.BufferGeometry();
  const positions = new Float32Array(count * 3);
  const sizes     = new Float32Array(count);

  for (let i = 0; i < count; i++) {
    positions[i * 3]     = (Math.random() - 0.5) * 20; // x
    positions[i * 3 + 1] = (Math.random() - 0.5) * 20; // y
    positions[i * 3 + 2] = (Math.random() - 0.5) * 20; // z
    sizes[i]             = Math.random() * 2 + 0.5;
  }

  geometry.setAttribute('position', new THREE.BufferAttribute(positions, 3));
  geometry.setAttribute('aSize',    new THREE.BufferAttribute(sizes, 1));

  const material = new THREE.ShaderMaterial({
    uniforms: {
      uTime:  { value: 0 },
      uColor: { value: new THREE.Color(0xfff7ec) },
    },
    vertexShader: `
      attribute float aSize;
      uniform float uTime;
      void main() {
        vec3 pos = position;
        pos.y += sin(uTime * 0.3 + position.x) * 0.1; /* gentle float */
        vec4 mvPos = modelViewMatrix * vec4(pos, 1.0);
        gl_PointSize = aSize * (300.0 / -mvPos.z);    /* size by distance */
        gl_Position = projectionMatrix * mvPos;
      }
    `,
    fragmentShader: `
      uniform vec3 uColor;
      void main() {
        float d = length(gl_PointCoord - 0.5); /* round particle */
        if (d > 0.5) discard;
        float alpha = 1.0 - smoothstep(0.3, 0.5, d);
        gl_FragColor = vec4(uColor, alpha * 0.4);
      }
    `,
    transparent: true,
    depthWrite:  false,
    blending:    THREE.AdditiveBlending,
  });

  return new THREE.Points(geometry, material);
}

// Update in render loop
particles.material.uniforms.uTime.value += 0.01;
```

---

## CINEMATIC LAYER 8 — PAGE TRANSITIONS

No hard reloads. Every page change is a choreographed scene transition.

### barba.js setup (the standard for premium page transitions)
```html
<!-- Wrap all page content -->
<div data-barba="wrapper">
  <div data-barba="container" data-barba-namespace="home">
    <!-- page content -->
  </div>
</div>
```

```javascript
import barba from '@barba/core';
import gsap from 'gsap';

barba.init({
  transitions: [{
    name: 'panel-wipe',   // name for debugging
    async leave({ current }) {
      // Animate OUT — panel slides down over current page
      await gsap.to('#transition-panel', {
        scaleY:   1,
        duration: 0.6,
        ease:     'power3.inOut',
        transformOrigin: 'top',
      });
    },
    async enter({ next }) {
      // New page is now visible — panel lifts up
      await gsap.to('#transition-panel', {
        scaleY:   0,
        duration: 0.6,
        ease:     'power3.inOut',
        transformOrigin: 'bottom',
        delay:    0.1,
      });
      // Animate new page elements in
      gsap.from(next.container.querySelectorAll('[data-reveal]'), {
        opacity: 0, y: 30, stagger: 0.1, duration: 0.8,
      });
    },
  }],
});
```

```html
<!-- The transition panel — sits at z:5000 -->
<div id="transition-panel" style="
  position:fixed; inset:0; z-index:5000;
  background:var(--c-accent);
  transform:scaleY(0); transform-origin:top;
  pointer-events:none;
"></div>
```

### Page transition archetypes

```
PANEL WIPE:    colored panel slides over screen, new page loads, panel lifts
FADE BLACK:    opacity to black, switch, fade from black (simple but cinematic)
CLIP CIRCLE:   circle expands from click point, covers screen, new page appears
MORPH ELEMENT: clicked card expands to fill screen → becomes new page hero
3D CUBE:       page flips like a 3D cube face (impressive, use sparingly)
```

---

## CINEMATIC PHASE 9B — PERFORMANCE RULES

Cinematic effects are expensive. Every decision has a cost.

### Performance budget
```
TARGET: 60fps on a mid-range laptop (not just a development machine)

Render budget by archetype:
┌─────────────────────────────────────────┐
│ HEAVY 3D (immersive, gaming-adjacent)   │
│  Polygon count:   <500K total scene     │
│  Textures:        <4K max, compressed   │
│  Draw calls:      <100 per frame        │
│  Postprocessing:  max 3 effects         │
├─────────────────────────────────────────┤
│ MODERATE (product, architecture)        │
│  Polygon count:   <200K total scene     │
│  Textures:        <2K max               │
│  Draw calls:      <50 per frame         │
│  Postprocessing:  max 2 effects         │
├─────────────────────────────────────────┤
│ LIGHT (accent 3D, logo, one object)     │
│  Polygon count:   <50K                  │
│  Textures:        <1K max               │
│  Draw calls:      <20 per frame         │
│  Postprocessing:  1 effect or none      │
└─────────────────────────────────────────┘
```

### Must-implement optimizations
```javascript
// 1. Pixel ratio cap — most critical single optimization
renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));

// 2. Dispose of scene objects when navigating away (memory leaks)
function disposeScene() {
  scene.traverse(child => {
    if (child.isMesh) {
      child.geometry.dispose();
      if (Array.isArray(child.material)) child.material.forEach(m => m.dispose());
      else child.material.dispose();
    }
  });
}

// 3. Frustum culling — Three.js does this automatically, but confirm it's not disabled
renderer.info.render; // monitor draw calls in dev

// 4. Level of detail (LOD) — simpler mesh at distance
const lod = new THREE.LOD();
lod.addLevel(highDetailMesh, 0);   // full detail close up
lod.addLevel(medDetailMesh, 5);    // medium detail at 5 units
lod.addLevel(lowDetailMesh, 15);   // low detail far away

// 5. Lazy-load 3D scenes — only initialize when section enters viewport
const observer = new IntersectionObserver(entries => {
  if (entries[0].isIntersecting) {
    initThreeScene(); // only now create the WebGL context
    observer.disconnect();
  }
}, { threshold: 0.1 });
observer.observe(document.querySelector('#three-section'));

// 6. Mobile fallback — disable 3D entirely on low-end devices
const isMobile = window.innerWidth < 768 || navigator.maxTouchPoints > 0;
const isLowEnd = navigator.hardwareConcurrency <= 4;
if (isMobile || isLowEnd) {
  // Show static fallback image instead of canvas
  document.querySelector('#three-canvas').style.display = 'none';
  document.querySelector('#fallback-image').style.display = 'block';
}
```

### Common mistakes that kill performance
```
❌ Calling new THREE.Material() inside the render loop → memory leak
❌ Pixel ratio set to devicePixelRatio without cap → 3× cost on retina
❌ Unbounded postprocessing → DOF + Bloom + SSAO + Grain at once
❌ GSAP ScrollTrigger refresh() on every scroll event
❌ No mobile fallback → 3D hangs on mobile CPU
❌ Loading 8K textures uncompressed → .jpg compressed to 512px max
❌ Scroll-jacking on page load before Lenis is ready → jank on first scroll
❌ Not disposing geometries/materials on page transition → memory grows
```

---

## CINEMATIC PHASE 10 — MODERN STACK (NEXT.JS / REACT)

For team projects and larger builds:

```
Frontend:    Next.js 14+ (App Router, RSC, streaming)
3D:          React Three Fiber + @react-three/drei
Animation:   GSAP (server-safe via useEffect)
Scroll:      Lenis (via @studio-freight/react-lenis wrapper)
State:       Zustand (lightweight, no Redux complexity)
Assets:      Blender → .glb → Draco compressed → served via CDN
Fonts:       next/font (local or Google) — zero layout shift
Deploy:      Vercel (edge network, auto-optimization)
```

### R3F + Lenis + GSAP ScrollTrigger (the full cinematic stack in React):
```jsx
// providers/Lenis.jsx
'use client';
import { useEffect } from 'react';
import Lenis from 'lenis';
import gsap from 'gsap';
import ScrollTrigger from 'gsap/ScrollTrigger';

export function LenisProvider({ children }) {
  useEffect(() => {
    const lenis = new Lenis({ lerp: 0.08, smoothWheel: true });
    lenis.on('scroll', ScrollTrigger.update);
    gsap.ticker.add(time => lenis.raf(time * 1000));
    gsap.ticker.lagSmoothing(0);
    return () => { lenis.destroy(); gsap.ticker.remove(); };
  }, []);
  return <>{children}</>;
}
```

---

## CINEMATIC CHECKLIST

Before calling a cinematic site complete:

**Rendering:**
- [ ] Pixel ratio capped at 2
- [ ] Draco compression on all .glb files
- [ ] HDRI loaded and applied as environment
- [ ] Tone mapping: ACESFilmic
- [ ] Textures compressed, max 2K

**Scroll:**
- [ ] Lenis + GSAP RAF properly connected
- [ ] ScrollTrigger refresh called on window resize
- [ ] Scroll progress normalized (0→1) and used consistently
- [ ] Mobile: native scroll (syncTouch: false)

**Postprocessing:**
- [ ] Bloom threshold high enough (not blooming everything)
- [ ] Grain opacity subtle (0.04–0.12)
- [ ] Vignette not too dark on mobile
- [ ] Composer replaces raw renderer.render()

**Typography:**
- [ ] No Poppins, Montserrat, or Open Sans
- [ ] Variable font loaded with woff2-variations format
- [ ] SplitType used for scroll-revealed text
- [ ] Font display: swap to prevent invisible text flash

**Performance:**
- [ ] 60fps confirmed on mid-range hardware
- [ ] Mobile fallback exists (image or simplified version)
- [ ] Scene disposed on barba.js page leave
- [ ] LOD applied if >200K polygons in scene

**Transitions:**
- [ ] No hard page reloads (barba.js or router-based)
- [ ] Transition panel at z:5000
- [ ] ScrollTrigger.refresh() called in barba enter hook
