---
name: interactive-preview
description: >-
  Use this skill when the user wants an interactive 3D-like design preview
  they can interact with directly in chat. Creates CSS 3D previews using
  perspective transforms, glassmorphism, hover effects, and animations —
  no external libraries needed. Activate when the user says things like
  "show me an interactive preview", "make a card with hover effect",
  "create a 3D card grid", or "glassmorphism design".
---

# Create an Interactive CSS 3D Preview

Create interactive 3D-looking website design previews that render inline
in the chat using the generative UI system. Uses pure CSS 3D transforms
and inline JavaScript — no Three.js or external CDNs (CSP blocks them
in chat widgets, except the allowed Tailwind CDN).

## When to Use

- User wants to see and interact with a 3D-like UI pattern
- Demonstrating hover effects, card flips, perspective grids
- Creating glassmorphism, parallax, or depth-layered designs
- Prototyping interactive UI components with 3D feel

## Available CSS 3D Patterns

1. **3D Card Tilt on Hover** — Cards that follow mouse with perspective
   transform. Use `perspective(1000px)` on parent, `rotateX/Y` based on
   mouse position within card.

2. **Glassmorphism Panels** — Frosted glass overlays with
   `backdrop-filter: blur(16px)` and semi-transparent backgrounds.
   Layer multiple panels at different depths.

3. **Isometric Grid** — CSS-transformed grid creating 3D isometric view
   using `rotateX(60deg) rotateZ(-45deg)`.

4. **Parallax Depth Layers** — Multi-layer mousemove parallax. Each layer
   moves at a different speed based on its "depth". Use `translateX/Y`
   with multiplied offsets.

5. **Card Flip** — 3D card flip reveal on hover/click using
   `transform-style: preserve-3d` and `rotateY(180deg)` on backface.

6. **Perspective Section** — Full sections with vanishing point transforms
   using `perspective` and `translateZ` for depth layers.

7. **Floating Elements** — CSS `@keyframes` animated floating/bobbing
   elements with `translateY` oscillation and subtle rotation.

8. **3D Button Press** — Buttons with `translateY` depth that
   `translateY(4px)` on click with shadow reduction.

9. **Layered Shadows** — Multi-shadow depth effects using multiple
   `box-shadow` values at increasing blur/spread.

10. **CSS 3D Carousel** — Rotating carousel of panels positioned with
    `rotateY` and `translateZ` in 3D space using `transform-style: preserve-3d`.

## Implementation Steps

1. **Create the HTML file** in the artifact directory:
   - Path: `<Artifact Directory>/<descriptive-name>.html`
   - Include Tailwind CSS via allowed CDN
   - Use CSS theme variables for dark/light mode
   - All JavaScript inline (no external scripts)

2. **Structure the HTML**:
   ```html
   <!DOCTYPE html>
   <html>
   <head>
     <script src="https://www.gstatic.com/antigravity/web/dev/tailwindcss.min.js"></script>
     <style>
       /* CSS 3D transforms, animations, and custom styles */
     </style>
   </head>
   <body class="bg-transparent text-[var(--foreground)] antialiased p-0 m-0">
     <div class="py-2 space-y-3">
       <!-- Design content here -->
     </div>
     <script>
       // Mouse tracking, interaction handlers
     </script>
   </body>
   </html>
   ```

3. **Apply 3D transforms**:
   - Set `perspective: 1000px` on parent containers
   - Use `transform-style: preserve-3d` for true 3D child positioning
   - Apply `rotateX`, `rotateY`, `rotateZ`, `translateZ` for depth
   - Use `backface-visibility: hidden` for card flips

4. **Add interactions**:
   - `mousemove` for tilt/parallax tracking
   - `mouseenter`/`mouseleave` for hover states
   - `click` for toggles (card flip, expand)
   - Use `transition: transform 0.4s ease` for smooth motion

5. **Keep it compact**:
   - Target under 450px total height for inline embed
   - If the design needs more room, make it a standalone artifact
   - Never use `h-screen`, `100vh`, or `height: 100%` on top containers

6. **Save with proper metadata**:
   - `UserFacing: true`
   - `RequestFeedback: false`

7. **Embed inline** in your chat response:
   ```
   <agent-embed src="file:///<path>/<name>.html"></agent-embed>
   ```

## Key CSS Properties Reference

```css
/* Parent: sets the perspective viewing distance */
.perspective-container {
  perspective: 1000px;
  perspective-origin: center;
}

/* Child: positioned in 3D space */
.card-3d {
  transform-style: preserve-3d;
  transition: transform 0.4s ease;
}

/* Glassmorphism */
.glass {
  background: rgba(255, 255, 255, 0.08);
  backdrop-filter: blur(16px);
  -webkit-backdrop-filter: blur(16px);
  border: 1px solid rgba(255, 255, 255, 0.12);
  border-radius: 16px;
}

/* Floating animation */
@keyframes float {
  0%, 100% { transform: translateY(0px) rotate(0deg); }
  50% { transform: translateY(-12px) rotate(2deg); }
}

/* Layered depth shadows */
.depth-shadow {
  box-shadow:
    0 2px 4px rgba(0,0,0,0.1),
    0 8px 16px rgba(0,0,0,0.1),
    0 16px 32px rgba(0,0,0,0.15);
}
```

## Mouse Tracking Template (Inline JS)

```javascript
document.querySelectorAll('.tilt-card').forEach(card => {
  card.addEventListener('mousemove', (e) => {
    const rect = card.getBoundingClientRect();
    const x = e.clientX - rect.left;
    const y = e.clientY - rect.top;
    const centerX = rect.width / 2;
    const centerY = rect.height / 2;
    const rotateX = ((y - centerY) / centerY) * -10; // max 10deg
    const rotateY = ((x - centerX) / centerX) * 10;
    card.style.transform =
      `perspective(1000px) rotateX(${rotateX}deg) rotateY(${rotateY}deg)`;
  });
  card.addEventListener('mouseleave', () => {
    card.style.transform = 'perspective(1000px) rotateX(0) rotateY(0)';
  });
});
```

## Reference
See [CSS 3D Patterns Reference](./references/css-3d-patterns.md)
for complete, copy-pasteable code examples of each pattern.
