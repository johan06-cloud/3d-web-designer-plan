# 3D Web Design Rules

When the user asks for a 3D website design:

## Output Selection
- For quick concepts and mood exploration → generate an image mockup
  using the image-generator subagent
- For interactive UI patterns (card flips, hover effects, parallax,
  glassmorphism, perspective grids) → create a CSS 3D generative UI
  widget inline in chat using the generative_ui skill
- For full 3D scenes with models and lighting → create a standalone
  .html file with Three.js and tell the user to open it in their browser
- When in doubt, ask the user which output format they prefer

## Design Principles for 3D Web
- Use depth through layering: foreground, midground, background
- Apply perspective transforms purposefully — not everything needs to rotate
- Glassmorphism (backdrop-blur + transparency) creates depth without 3D geometry
- Lighting and shadows are more important than geometry for perceived depth
- Limit 3D interactions to hero sections; keep navigation and text 2D
- Dark backgrounds make 3D elements pop; use gradients for depth cues
- Motion should be subtle and purposeful — 3D ≠ spinning everything

## CSS 3D Preview Rules (Generative UI)
- Use only CSS 3D transforms (perspective, rotateX/Y/Z, translateZ) —
  no external JS libraries (CSP blocks them in chat widgets)
- Include Tailwind via the allowed gstatic CDN:
  `<script src="https://www.gstatic.com/antigravity/web/dev/tailwindcss.min.js"></script>`
- Use theme variables (var(--foreground), var(--card), etc.) for
  dark/light mode compatibility
- Keep inline previews under 450px height
- Make interactions smooth: use CSS transitions (0.3-0.6s ease)
- For standalone artifacts (> 450px), use a solid page background

## Three.js HTML Preview Rules
- Create fully self-contained .html files
- Load Three.js from CDN (cdnjs.cloudflare.com or esm.sh)
- Include OrbitControls so the user can explore the scene
- Cap pixel ratio: Math.min(window.devicePixelRatio, 2)
- Always handle window resize
- For 3D models, use free .glb files from:
  Poly Haven (polyhaven.com), Sketchfab (sketchfab.com),
  or pmndrs market (market.pmnd.rs)

## Image Mockup Rules
- When generating design concept images, describe the design in detail:
  layout structure, color palette, typography style, 3D effects,
  lighting mood, and content placement
- Always specify "web design mockup" or "website UI design" in the prompt
  to get web-appropriate output
- Include specific details about the 3D elements: floating objects,
  glassmorphism cards, depth layers, perspective views

## Code Generation Rules (when converting designs to code)
- Never use `setState` inside `useFrame`. Always mutate via refs.
- Always multiply animations by `delta` from `useFrame` for frame-rate independence.
- Cap device pixel ratio with `dpr={[1, 2]}` on Canvas.
- Use `<instancedMesh>` for any repeated geometry (>10 instances).
- Wrap 3D components in `<Suspense>` with a loading fallback.
- Keep 3D canvas logic and HTML DOM UI in separate component trees.
- Use Zustand (not Redux or Context) for state shared between 3D and UI layers.
- Recommend `.glb` over `.gltf` for production (single binary, smaller).
- Never trap scroll events inside a full-screen canvas without an escape mechanism.
