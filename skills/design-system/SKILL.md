---
name: 3d-design-system
description: >-
  Use this skill when the user wants guidance on 3D web design principles,
  color theory for depth, lighting strategies, choosing the right 3D effects,
  or creating a consistent design system for 3D web projects. Activate when
  the user asks "how should I design this", "what 3D effects work best for",
  "help me choose colors for a 3D site", or "design system for 3D".
---

# 3D Web Design System

Provides design guidance and principles for creating effective,
visually stunning 3D-looking websites. Use this skill to advise the
user on design decisions before generating mockups or previews.

## Core Design Pillars

### 1. Depth Through Layering
Every great 3D website creates a sense of depth with layers:
- **Foreground**: Interactive elements, CTAs, floating UI, text overlays
- **Midground**: Content cards, images, main sections, feature grids
- **Background**: Gradients, particles, ambient 3D shapes, grid patterns

Minimum 3 layers visible in hero sections for effective depth.

### 2. Lighting Creates Dimension
Lighting is MORE important than geometry for perceived 3D:
- **Key light** (top-left or top-right): Main light source, creates
  primary shadows. Strongest intensity.
- **Fill light** (opposite side): Softens shadows, prevents pure black.
  About 40-60% of key light intensity.
- **Rim/accent light** (behind subject): Creates edge glow, separates
  subject from background. Often a brand accent color.
- **Ambient**: General scene illumination. Keep low for dramatic feel.

### 3. Motion Hierarchy
Not everything should move. Apply motion purposefully:
- **Hero elements**: Dramatic 3D motion (rotation, float, parallax) ✅
- **Secondary elements**: Subtle hover effects, gentle parallax ✅
- **Text and navigation**: Static or minimal translate only ✅
- **Everything at once**: Competing motion = visual chaos ❌

**Rule**: Maximum 2-3 animated elements visible at the same time.

### 4. Color for Depth
Colors naturally suggest spatial position:
- **Dark colors** recede (feel further away)
- **Light colors** advance (feel closer)
- **Warm colors** (red, orange, yellow) advance
- **Cool colors** (blue, purple) recede
- **High saturation** advances; **low saturation** recedes

## 3D Effect Decision Guide

| Goal | Best Effect | Complexity |
|:--|:--|:--|
| Depth without 3D geometry | Glassmorphism + layered shadows | Low |
| Interactive product display | Three.js with orbit controls | High |
| Engaging landing page hero | Floating elements + parallax | Medium |
| Card-based content layout | 3D card tilt on hover | Low |
| Immersive storytelling | Scroll-driven camera animation | High |
| Data/dashboard design | Isometric CSS grid | Medium |
| Portfolio/gallery | CSS 3D carousel | Medium |
| Background atmosphere | Particle field (Three.js) | Medium |

## Color Palettes for 3D Web

### Dark Techy
- Background: `#0a0a0a` → `#1a1a2e` gradient
- Primary: `#6366f1` (Indigo) or `#8b5cf6` (Purple)
- Accent: `#f472b6` (Pink) or `#22d3ee` (Cyan)
- Text: `#ffffff` / `#a1a1aa` (muted)
- Glass: `rgba(255,255,255,0.05)` with `blur(16px)`

### Light Minimal
- Background: `#fafafa` → `#f1f5f9` gradient
- Primary: `#2563eb` (Blue) or `#0ea5e9` (Sky)
- Accent: `#f59e0b` (Amber)
- Text: `#0f172a` / `#64748b` (muted)
- Shadows: `rgba(0,0,0,0.08)` multi-layered

### Neon Cyberpunk
- Background: `#000000` → `#0a0014`
- Primary: `#00ff88` (Neon green) or `#ff0080` (Hot pink)
- Accent: `#00d4ff` (Electric blue)
- Text: `#ffffff` / `#666666`
- Glow: `0 0 20px rgba(0,255,136,0.5)` box-shadow

### Luxury Elegant
- Background: `#1a1a1a` → `#2d2d2d`
- Primary: `#d4af37` (Gold) or `#c0c0c0` (Silver)
- Accent: `#ffffff`
- Text: `#f5f5f5` / `#888888`
- Surfaces: subtle noise texture overlay

### Organic Natural
- Background: `#fef9ef` → `#f0ebe3`
- Primary: `#2d5016` (Forest green) or `#8b4513` (Earth brown)
- Accent: `#d4a373` (Warm sand)
- Text: `#1a1a1a` / `#6b6b6b`
- Shapes: organic blobs, smooth curves

## Typography for 3D Design

- **Hero headings**: Bold 700-900 weight, oversized (48-120px).
  Consider letter-spacing adjustments (tighter for display fonts).
- **Body text**: Regular 400 weight, 16-18px. Keep on flat planes —
  never apply 3D transforms to body text.
- **Labels & captions**: Light 300-400 weight, 12-14px, muted color.
- **Font pairing suggestions**:
  - Modern: Inter + Space Grotesk
  - Bold: Plus Jakarta Sans + DM Sans
  - Editorial: Playfair Display + Source Sans
  - Tech: JetBrains Mono + Inter

## Responsive Considerations

- **Desktop** (1200px+): Full 3D effects, all layers active
- **Tablet** (768-1199px): Reduce parallax intensity by 50%,
  simplify particle counts
- **Mobile** (< 768px): Disable heavy 3D (orbit controls, particles),
  keep glassmorphism and shadows, simplify to 2 depth layers
- **Performance**: Always offer a graceful 2D fallback for
  low-end devices and browsers without WebGL

## Reference
See [3D Design Principles](./references/3d-design-principles.md)
for in-depth theory on depth perception, lighting psychology,
and motion design for the web.
