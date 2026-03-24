# Cinematic Rendering Stack — Reference

Reference for cinematic/WebGL stack. Read this when the brief calls for 3D, immersive, or cinematic experiences.

---

# CINEMATIC RENDERING STACK — ADVANCED LAYER SYSTEM

This is the system underneath the most visually impressive agency sites.
Not every site needs it. But when the brief calls for "cinematic", "immersive",
or "3D experience" — this is the architecture to reach for.

**Decision gate — when to use the cinematic stack:**
```
Does the site need:
  [ ] 3D objects / environments?             -> YES: use WebGL layer
  [ ] Scroll-driven 3D camera movement?      -> YES: use Lenis + ScrollTrigger + Three.js
  [ ] Custom shaders (water, glass, distort)? -> YES: use GLSL layer
  [ ] Postprocessing (bloom, grain, DoF)?    -> YES: use EffectComposer
  [ ] Page transitions (no hard reload)?     -> YES: use barba.js
  [ ] Particle systems?                      -> YES: use Three.js Points / GPUComputationRenderer
  [ ] Realistic lighting / reflections?      -> YES: use HDRI

All NO -> use CSS/HTML stack only (Phases 0-11 above are sufficient)
Any YES -> add the layers below on top of the CSS/HTML foundation
```

---

## CINEMATIC LAYER 0 — ARCHITECTURE OVERVIEW

Every cinematic site is built from stacked layers, each with a clear responsibility.
Never mix responsibilities across layers.

```
+-------------------------------------------------------------+
|  LAYER 7 — UI + DOM                                         |
|  HTML/CSS, custom cursor, nav, overlays, micro-anim         |
+-------------------------------------------------------------+
|  LAYER 6 — TYPOGRAPHY                                       |
|  Variable fonts, SVG type, GSAP text splits                 |
+-------------------------------------------------------------+
|  LAYER 5 — SCROLL ORCHESTRATION                             |
|  Lenis -> normalized 0-1 value -> GSAP timelines            |
+-------------------------------------------------------------+
|  LAYER 4 — POSTPROCESSING                                   |
|  EffectComposer: bloom, DoF, motion blur, grain, grade      |
+-------------------------------------------------------------+
|  LAYER 3 — SHADERS (GLSL)                                   |
|  Custom materials: water, glass, distortion, gradients      |
+-------------------------------------------------------------+
|  LAYER 2 — SCENE                                            |
|  Three.js: camera, lights, meshes, HDRI env map             |
+-------------------------------------------------------------+
|  LAYER 1 — RENDERING ENGINE                                 |
|  Three.js WebGLRenderer (or WebGPURenderer next-gen)        |
+-------------------------------------------------------------+
|  LAYER 0 — GPU                                              |
|  WebGL context / WebGPU context (hardware acceleration)     |
+-------------------------------------------------------------+
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
  45,                                    // FOV — 35-50 for architectural/product
  window.innerWidth / window.innerHeight,
  0.1,
  1000
);
camera.position.set(0, 0, 5);
```

### Asset loading with Draco compression
```javascript
// Draco reduces .glb file size by 80-95%
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
// HDRI = 360 deg environment map — provides realistic reflections + lighting
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
uniform float uDistortion;  /* 0 to 1 on hover */
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
Raw 3D render -> Bloom -> Depth of Field -> Motion Blur -> Film Grain -> Color Grade -> Screen
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
    |
Lenis (virtual scroll — adds inertia, smoothness, lerp)
    |
Normalized progress (0 to 1, never raw pixels)
    |
GSAP ScrollTrigger (maps sections to timelines)
    |
Branches simultaneously to:
  +-- Three.js scene (camera pos, object rotations)
  +-- DOM animations (text reveals, section fades)
  +-- Shader uniforms (distortion, color shifts)
  +-- CSS custom properties (gradient pos, blur amount)
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
    end:      '+=400%',    // 4x viewport height = 400vh of scroll
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
TIER 1 — Custom / Commissioned      -> Only the client has it. Maximum brand identity.
TIER 2 — Independent foundries       -> Rarely seen on other sites
  - Pangram Pangram (PP Neue Montreal, PP Editorial New)
  - Klim Type Foundry (Domaine, Feijoa)
  - Colophon Foundry (Apercu, Raisonne)
  - Commercial Type (Graphik, Canela)
  - Grilli Type (GT America, GT Walsheim, GT Super)
  - Production Type (Romain BP, Antique Legacy)

TIER 3 — Adobe Fonts / Typekit       -> Good quality, less exclusive
TIER 4 — Google Fonts                -> Free but seen everywhere — use only if variable font
  - Recommended: DM Sans, Inter, Plus Jakarta Sans (all variable)
  - Display: Playfair Display, Fraunces (variable), Cormorant

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
MORPH ELEMENT: clicked card expands to fill screen -> becomes new page hero
3D CUBE:       page flips like a 3D cube face (impressive, use sparingly)
```

---

## CINEMATIC PHASE 9B — PERFORMANCE RULES

Cinematic effects are expensive. Every decision has a cost.

### Performance budget
```
TARGET: 60fps on a mid-range laptop (not just a development machine)

Render budget by archetype:
+-------------------------------------------+
| HEAVY 3D (immersive, gaming-adjacent)     |
|  Polygon count:   <500K total scene       |
|  Textures:        <4K max, compressed     |
|  Draw calls:      <100 per frame          |
|  Postprocessing:  max 3 effects           |
+-------------------------------------------+
| MODERATE (product, architecture)          |
|  Polygon count:   <200K total scene       |
|  Textures:        <2K max                 |
|  Draw calls:      <50 per frame           |
|  Postprocessing:  max 2 effects           |
+-------------------------------------------+
| LIGHT (accent 3D, logo, one object)       |
|  Polygon count:   <50K                    |
|  Textures:        <1K max                 |
|  Draw calls:      <20 per frame           |
|  Postprocessing:  1 effect or none        |
+-------------------------------------------+
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
Calling new THREE.Material() inside the render loop -> memory leak
Pixel ratio set to devicePixelRatio without cap -> 3x cost on retina
Unbounded postprocessing -> DOF + Bloom + SSAO + Grain at once
GSAP ScrollTrigger refresh() on every scroll event
No mobile fallback -> 3D hangs on mobile CPU
Loading 8K textures uncompressed -> .jpg compressed to 512px max
Scroll-jacking on page load before Lenis is ready -> jank on first scroll
Not disposing geometries/materials on page transition -> memory grows
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
Assets:      Blender -> .glb -> Draco compressed -> served via CDN
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
- [ ] Scroll progress normalized (0 to 1) and used consistently
- [ ] Mobile: native scroll (syncTouch: false)

**Postprocessing:**
- [ ] Bloom threshold high enough (not blooming everything)
- [ ] Grain opacity subtle (0.04-0.12)
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
