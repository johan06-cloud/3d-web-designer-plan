---
name: design-concept
description: >-
  Use this skill when the user wants a visual concept or mockup of a 3D
  website design. Generates AI-rendered design concept images showing
  layout, color, 3D effects, and mood — similar to a Figma design mockup.
  Activate when the user says things like "design a landing page",
  "show me a concept for", "mockup a 3D website", or "what would a 3D
  portfolio look like".
---

# Generate a 3D Website Design Concept

Generate visual mockups of 3D website designs using the image-generator
subagent. This produces static design concept images similar to what you'd
create in Figma — showing layout, typography, color, 3D effects, and mood.

## When to Use

- User wants to explore a visual direction before committing
- Quick concept iteration (try different color schemes, layouts, moods)
- Communicating a design idea visually
- Getting inspiration for a 3D web project

## Steps

1. **Understand the design brief** — ask the user (if not already clear):
   - What type of site? (landing page, portfolio, product showcase, SaaS,
     agency, e-commerce, blog)
   - What brand/mood? (dark & techy, light & minimal, colorful & playful,
     luxury & elegant, neon & cyberpunk, organic & natural)
   - What 3D effects? (floating elements, parallax layers, glassmorphism,
     3D product renders, particle fields, geometric shapes, isometric)
   - What content? (hero text, product images, navigation, feature cards,
     testimonials, pricing tables, footer)
   - Any color preferences? (specific hex colors, or general direction)

2. **Compose a detailed image generation prompt** including:
   - "Professional website UI/UX design mockup, high fidelity"
   - Layout structure with specific section descriptions
   - 3D visual effects described concretely
   - Color palette (mention specific colors or gradients)
   - Typography style (modern sans-serif, bold display, elegant serif)
   - Specific UI elements (buttons, nav bars, cards, icons)
   - "Desktop browser frame" or "full-page website screenshot"
   - "Dribbble quality, Awwwards-level design"

3. **Generate the concept** using the image-generator subagent

4. **Present and iterate** — after showing the result, offer options:
   - "Want to try a different color palette or mood?"
   - "Should I make this into an interactive CSS 3D preview you can
     interact with?" (→ activate `interactive-preview` skill)
   - "Want a full Three.js 3D scene from this design?"
     (→ activate `3d-scene-preview` skill)
   - "Should I convert this into production code?"

## Prompt Templates

### Dark Tech Landing Page
"A professional website landing page UI/UX design mockup. Dark gradient
background transitioning from #0a0a0a to #1a1a2e. Hero section with large
bold white headline text and a glowing 3D geometric shape (icosahedron)
floating with soft purple (#8b5cf6) rim lighting. Glassmorphism card below
with frosted glass effect showing feature highlights. Subtle dot grid
pattern in background. Modern sans-serif typography. Gradient CTA button
(purple to pink). Clean minimal navigation bar with logo on left. Desktop
browser frame. Dribbble quality, premium web design."

### Product Showcase
"A premium product showcase website design mockup. Clean white/light gray
background with subtle gradient. Large 3D product render floating in center
with soft shadow underneath. Minimal navigation at top. Product name in
bold display font. Color/variant selector dots below product. 'Add to Cart'
button with depth shadow. Specifications in a clean grid layout below.
Apple-inspired minimalism. High-end e-commerce design. Desktop view."

### Creative Portfolio
"A creative portfolio website design mockup. Dark background #111111 with
large bold typography. Hero section with the name in oversized display font
(200px+). 3D floating project thumbnails arranged in an asymmetric grid
with perspective tilt. Hover state shown on one card with slight zoom and
glow. Smooth rounded corners on cards. Accent color electric blue #3b82f6.
Navigation as minimal text links. Scroll indicator at bottom. Awwwards
style editorial design. Desktop browser frame."

### SaaS Dashboard Landing
"A modern SaaS landing page design mockup. Light mode with white background.
Hero section showing a 3D-perspective view of the dashboard product,
slightly rotated with a subtle shadow creating depth. Gradient blob shapes
in background (soft purple and blue). Feature cards in a 3-column grid
below, each with an icon and short description. Social proof logos bar.
Pricing table section. Clean sans-serif typography. Blue primary color
#2563eb. Professional and trustworthy feel. Desktop browser frame."

## Tips for Better Results
- Be specific about colors: use hex codes, not just "blue"
- Describe the layout spatially: "hero section at top, 3-column grid below"
- Mention the 3D effect explicitly: "floating with shadow", "perspective
  tilt", "glassmorphism overlay"
- Reference design inspiration: "Apple-inspired", "Awwwards quality",
  "Dribbble style"
- Include typography details: "bold display heading, light body text"
