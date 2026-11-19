# 3D Design Principles for the Web

In-depth theory on creating effective 3D-looking website designs.
This reference covers perception, lighting psychology, and motion
design principles specific to web interfaces.

---

## Depth Perception on Screens

Humans perceive depth on flat screens through **monocular cues** —
visual hints that don't require two eyes (since screens are flat):

### 1. Occlusion (Overlap)
Objects in front partially block objects behind. This is the
strongest depth cue on screens.
- **Web application**: Layer cards, images, and UI panels so they
  overlap slightly. Even 10-20px overlap creates clear depth ordering.

### 2. Relative Size
Closer objects appear larger; distant objects appear smaller.
- **Web application**: Use size variation in grids. Hero elements
  should be prominently larger than supporting elements.

### 3. Atmospheric Perspective (Haze)
Distant objects appear lighter, blurrier, and less saturated.
- **Web application**: Apply blur (`filter: blur()`) and reduce
  opacity on background layers. Use lower contrast and saturation
  for elements that should appear further away.

### 4. Linear Perspective (Vanishing Points)
Parallel lines converge toward a vanishing point.
- **Web application**: CSS `perspective` and `rotateX/Y` transforms
  create vanishing-point depth. Use sparingly — one vanishing point
  per viewport section.

### 5. Shadow and Shading
Shadows indicate an object is lifted above a surface.
- **Web application**: Multi-layered box-shadows. Larger blur radius
  and offset = higher elevation = closer to viewer. Keep shadow
  direction consistent (usually top-left light source).

### 6. Motion Parallax
Closer objects move faster than distant objects when the viewport moves.
- **Web application**: Mouse-tracking or scroll-driven parallax with
  different movement speeds per layer.

---

## Lighting Psychology in Web Design

Lighting affects how users emotionally respond to a design:

### Top-Left Lighting (Default)
- Feels natural (matches sunlight and reading direction)
- Creates familiar shadow patterns
- Best for: Most websites, especially B2B, SaaS, e-commerce

### Dramatic Side Lighting
- Creates strong contrast (light vs. dark split)
- Feels edgy, artistic, high-end
- Best for: Fashion, creative agencies, portfolio sites

### Rim/Back Lighting
- Silhouettes with glowing edges
- Feels mysterious, premium, sci-fi
- Best for: Product reveals, tech products, gaming

### Bottom-Up Lighting
- Unnatural, unsettling (campfire effect)
- Feels dramatic, horror-adjacent, attention-grabbing
- Best for: Sparing use in hero sections for impact. Avoid for
  sustained reading or browsing areas.

### Ambient/Flat Lighting
- Even illumination, minimal shadows
- Feels clean, modern, approachable
- Best for: Minimal designs, documentation, tools

---

## Motion Design for 3D Web

### The 12 Principles Applied to Web

Borrowed from Disney animation, adapted for web interfaces:

1. **Squash & Stretch**: Buttons press down (squash) and bounce back.
   Use `scaleY` on press events.

2. **Anticipation**: Before a big transition, do a small reverse motion.
   Cards might slightly pull back before sliding forward.

3. **Staging**: Direct the user's eye to one thing at a time. Don't
   animate multiple unrelated elements simultaneously.

4. **Follow Through**: After an element stops moving, let it overshoot
   slightly and settle. Use `cubic-bezier(0.34, 1.56, 0.64, 1)`.

5. **Ease In / Ease Out**: Never use `linear` for UI motion. Always
   ease: `ease-out` for entrances, `ease-in` for exits,
   `ease-in-out` for position changes.

6. **Secondary Action**: While the main card animates, its shadow
   updates independently. While a panel slides in, the background
   dims separately.

### Timing Guidelines

| Animation Type | Duration | Easing |
|:--|:--|:--|
| Hover state change | 150-250ms | ease-out |
| Card tilt (mouse follow) | 100-200ms | ease-out |
| Panel slide in | 300-400ms | ease-out or cubic-bezier |
| Page transition | 400-600ms | ease-in-out |
| Floating/bobbing loop | 3000-6000ms | ease-in-out |
| Auto-rotation (3D) | Continuous, 0.5-2 RPM | linear |
| Parallax response | 0ms (immediate) or 50-100ms | ease-out |

### Performance Rules for Animation
- Use `transform` and `opacity` only — they don't trigger layout/paint
- Avoid animating `width`, `height`, `margin`, `padding`, `top`, `left`
- Use `will-change: transform` on animated elements (but not on too many)
- Prefer CSS animations over JavaScript for simple transitions
- Use `requestAnimationFrame` for JS-driven animations

---

## Typography in 3D Contexts

### Never 3D-Transform Body Text
Rotated or perspective-transformed text is hard to read. Reserve 3D
transforms for headings, decorative text, and labels only.

### Create Typographic Depth Without Transforms
- **Text shadow**: `text-shadow: 0 2px 4px rgba(0,0,0,0.3)` adds
  subtle depth without distortion
- **Gradient text**: `background-clip: text` with a subtle gradient
  creates dimensionality
- **Layered text**: Place a blurred, offset copy behind the main text
  for a 3D shadow effect
- **Outline + fill**: Combine `-webkit-text-stroke` with fill for
  dimensional headings

### Size Hierarchy for 3D Layouts
- **Display/Hero**: 48-120px+ (can go very large in 3D contexts)
- **Section Heading**: 32-48px
- **Card Heading**: 20-28px
- **Body**: 16-18px (never smaller on 3D sites where elements compete)
- **Caption/Label**: 12-14px

---

## Responsive 3D Design

### Progressive Enhancement Strategy

**Layer 1: Base (all devices)**
- Layered shadows for depth
- Subtle gradients
- Well-structured layout hierarchy
- Glassmorphism with fallback

**Layer 2: Enhanced (tablets+)**
- CSS 3D transforms on hover
- Parallax on scroll
- Animated transitions
- More complex shadow stacking

**Layer 3: Full 3D (desktop with capable GPU)**
- Three.js WebGL scenes
- Post-processing effects (bloom, DOF)
- Complex particle systems
- Multiple simultaneous animations

### GPU Capability Detection
```javascript
// Quick GPU check
const canvas = document.createElement('canvas');
const gl = canvas.getContext('webgl2') || canvas.getContext('webgl');
const hasWebGL = !!gl;
const renderer = gl?.getExtension('WEBGL_debug_renderer_info');
const gpu = renderer ? gl.getParameter(renderer.UNMASKED_RENDERER_WEBGL) : '';
const isLowEnd = /Mali|Adreno [34]|Intel HD [56]/i.test(gpu);
```

### Fallback Patterns
- **No WebGL**: Show a static high-quality image or CSS-only 3D
- **Low-end GPU**: Reduce particle count, disable post-processing,
  lower shadow map resolution
- **Mobile**: Disable orbit controls (use auto-rotation instead),
  reduce draw calls, limit to 2 depth layers
- **Reduced motion preference**: Respect
  `prefers-reduced-motion: reduce` — disable parallax, auto-rotation,
  and floating animations. Keep static depth cues (shadows, layers).
