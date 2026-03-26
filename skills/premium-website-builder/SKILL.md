---
name: premium-website-builder
description: >
  Use when building, designing, creating, or improving a website, landing page,
  or digital presence. Triggers on: "build a website", "premium landing page",
  "like a top agency", "make it look premium", "3D experience", "cinematic",
  "immersive", "WebGL", or any website/page creation task.
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
> "SaaS startup" → "What does the visitor do after they land? Sign up? Book a call?"
> "Portfolio" → "Are you looking for freelance clients or a full-time role?"
> "Brand agency" → "Is this to attract clients or to win awards?"

**Q2 — What is the ONE action you want from every visitor?**
Everything is designed backward from this single CTA.
Examples: book a call / buy now / apply to work here / feel the brand / get the app

**Q3 — What feeling should the first 3 seconds create?**
This determines hero composition, color temperature, and typography BEFORE anything else.
Get specific — "professional" is not an answer. Push for:
> "trust and scale" / "surprising and playful" / "quiet luxury" /
  "cinematic and forward-looking" / "warm and human" / "ruthlessly focused"

**Q4 — Who is the visitor and what do they already believe?**
Shapes copy tone, interaction complexity, and how much you need to explain vs. show.
> B2B decision-makers (skeptical, time-poor) → authority first, features second
> Creative directors (taste-first) → composition and craft speak louder than copy
> Consumers (emotional) → feeling first, then rationalization

**Q5 — What assets exist?** (determines if Gemini generation is needed)
```
Logo:        [ ] Y  [ ] N — need to generate SVG wordmark
Colors:      [ ] Y  [ ] N — need to derive from brand personality
Photos:      [ ] Y  [ ] N (partial) — need Gemini Imagen
Video:       [ ] Y  [ ] N — need Gemini Veo 2
Copy:        [ ] Y  [ ] N — need editorial direction
3D models:   [ ] Y  [ ] N — .glb from Blender, or product scans
```

**Q5B — Cinematic stack trigger (ask if any of these come up):**
If the brief uses words like "immersive", "3D", "cinematic", "like a WebGL site",
"interactive 3D", "scroll-driven 3D", "particles", or references sites like
Bruno Simon, Awwwards 3D winners, or similar — ask:

> "Do you need a 3D WebGL experience, or would a premium CSS/HTML site achieve this?"
> "What's the target device? WebGL is heavier on mobile."
> "Do you have a 3D model (.glb / .fbx) or does it need to be created?"

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
> P09 (section color inversion) → instead of IntersectionObserver bg swap,
  reveal the new bg color via an expanding clip-path circle from the CTA position

**Invert:** Reverse the spatial logic.
> P41 (photos float IN around the wordmark) → try photos that float OUT as you scroll,
  leaving the wordmark increasingly exposed and isolated

**Combine:** Merge two patterns into something unnamed.
> P32 (type as mask) + P07 (word opacity scrub) = letters that are DARK until you
  scroll past them, then each letter illuminates as the photo "fills in" behind it

**Restraint:** Sometimes the right decision is to NOT add a pattern.
> A luxury site with a single centered product on pure white needs no scroll animations.
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
rotates counterclockwise 180 degrees, no cuts, 12 seconds, seamless near-loop,
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
a subtle paper grain texture. The SVG should tile seamlessly at 200x200px.
Opacity should be near-transparent (use as a background overlay). Return only
the SVG code.
```

---

## REFERENCE FILES — Read only what you need

After Phase 3, read the relevant reference file(s) based on what you're building:

| What you're doing | Read this file |
|---|---|
| CSS/HTML implementation (colors, typography, mandatory elements, scrollbar, micro-interactions) | `references/css-html-patterns.md` |
| Cinematic/WebGL stack (3D, shaders, postprocessing, particles, page transitions) | `references/cinematic-stack.md` |
| Final review before delivering | `references/checklists.md` |

### Workflow after intake:

1. **Phases 4-8** (CSS/HTML build) → read `references/css-html-patterns.md`
2. **Cinematic layers** (if 3D/WebGL triggered in Q5B) → read `references/cinematic-stack.md`
3. **Before delivering** → read `references/checklists.md`

---

## REFERENCE: Pattern library index

All 67+ patterns + cinematic layers. Quick lookup:

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

For full pattern details and code examples, see `references/css-html-patterns.md`.
