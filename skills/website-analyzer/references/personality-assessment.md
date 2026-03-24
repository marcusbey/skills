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
