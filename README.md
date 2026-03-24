# Claude Code Skills — Premium Web Design Toolkit

Two Claude Code skills for building and analyzing premium websites, distilled from research on 15+ award-winning studio sites and emotional design theory (Don Norman, Aarron Walter).

## Skills

### `premium-website-builder.skill`

Turns Claude Code into a premium website builder — from clean CSS/HTML sites to full cinematic WebGL experiences.

**What it does:**
- Guides Claude through a structured intake process before writing any code
- Applies emotional design principles (visceral, behavioral, reflective) to every decision
- Covers two stacks:
  - **CSS/HTML premium stack** — 67+ patterns including custom cursors, scroll-linked animations, scrollbar design, micro-interactions, color systems, and typography
  - **Cinematic stack** — Three.js/R3F, GLSL shaders, HDRI lighting, postprocessing (bloom, grain, DoF), GSAP ScrollTrigger, barba.js page transitions, particle systems
- Generates assets via Gemini (Imagen/Veo 2) when the user has no photos or video
- Includes ready-to-use HTML templates and a decision framework for pattern selection

**Trigger phrases:** "build a website", "premium landing page", "like a top agency", "3D experience", "cinematic", "immersive"

---

### `website-analyzer-v4.skill`

Turns Claude Code into a website reverse-engineering tool. Point it at any URL and get a pixel-perfect spec.

**What it does:**
- Extracts every animation, cursor state, z-index layer, gradient, SVG, hover state, and micro-interaction
- Documents scroll-tied video scrubbing, parallax, and composition bridges between sections
- Maps the full emotional arc of a page (hook, bridge, proof, humanity, ask)
- Catalogs all 46+ patterns from a built-in pattern library
- Outputs a structured `.md` spec you can hand to the builder skill to recreate anything
- Includes browser scripts for automated deep extraction (CSS, layers, video frames, composition)

**Trigger phrases:** "analyze this site", "how does this work", "deep dive", "reverse-engineer", "recreate this"

---

## Installation

Drop the `.skill` files into your Claude Code skills directory:

```bash
# Default location
cp *.skill ~/.claude/skills/

# Or wherever your skills are configured
```

Then use them in Claude Code by referencing them naturally — the skill triggers automatically based on your prompt.

## How they work together

1. **Analyze** a reference site with `website-analyzer-v4` to get a full spec
2. **Build** your own version with `premium-website-builder` using that spec as input

## Requirements

- [Claude Code](https://docs.anthropic.com/en/docs/claude-code) CLI
- For asset generation: a Google Gemini API key (optional — only needed if you don't have photos/video)
- For WebGL sites: Node.js environment with Three.js/R3F

## License

MIT
