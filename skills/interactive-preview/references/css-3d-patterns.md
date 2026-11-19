# CSS 3D Patterns Reference

Complete, copy-pasteable code examples for each CSS 3D pattern.
All examples use Tailwind CSS (via allowed gstatic CDN) and CSS
theme variables for dark/light mode compatibility.

---

## 1. 3D Card Tilt on Hover

Cards that follow the mouse cursor with a smooth perspective tilt effect.

```html
<div class="perspective-container" style="perspective: 1000px;">
  <div class="tilt-card"
       style="transition: transform 0.3s ease; transform-style: preserve-3d;
              border-radius: 16px; padding: 24px;
              background: var(--card); border: 1px solid var(--card-border);">
    <h3 style="color: var(--foreground); margin: 0 0 8px;">Card Title</h3>
    <p style="color: var(--muted-foreground); margin: 0; font-size: 14px;">
      Hover over this card to see the 3D tilt effect.
    </p>
  </div>
</div>

<script>
document.querySelectorAll('.tilt-card').forEach(card => {
  card.addEventListener('mousemove', (e) => {
    const rect = card.getBoundingClientRect();
    const x = (e.clientX - rect.left) / rect.width - 0.5;
    const y = (e.clientY - rect.top) / rect.height - 0.5;
    card.style.transform =
      `rotateY(${x * 20}deg) rotateX(${y * -20}deg) translateZ(10px)`;
  });
  card.addEventListener('mouseleave', () => {
    card.style.transform = 'rotateY(0) rotateX(0) translateZ(0)';
  });
});
</script>
```

---

## 2. Glassmorphism Panel

Frosted glass overlay effect with backdrop blur.

```html
<div style="position: relative; padding: 40px;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            border-radius: 16px; overflow: hidden;">
  <!-- Background decorative shapes -->
  <div style="position: absolute; top: -20px; right: -20px; width: 100px;
              height: 100px; background: rgba(255,255,255,0.2);
              border-radius: 50%;"></div>
  <div style="position: absolute; bottom: -30px; left: 20px; width: 150px;
              height: 150px; background: rgba(255,255,255,0.1);
              border-radius: 50%;"></div>

  <!-- Glass card -->
  <div style="position: relative; z-index: 1; padding: 24px;
              background: rgba(255,255,255,0.1);
              backdrop-filter: blur(16px); -webkit-backdrop-filter: blur(16px);
              border: 1px solid rgba(255,255,255,0.2);
              border-radius: 12px;">
    <h3 style="color: white; margin: 0 0 8px;">Glassmorphism</h3>
    <p style="color: rgba(255,255,255,0.8); margin: 0; font-size: 14px;">
      Frosted glass creates depth without 3D geometry.
    </p>
  </div>
</div>
```

---

## 3. Isometric Grid

CSS-transformed grid creating a 3D isometric perspective view.

```html
<div style="display: flex; justify-content: center; align-items: center;
            padding: 60px 20px; perspective: 1200px;">
  <div style="display: grid; grid-template-columns: repeat(3, 80px);
              gap: 8px; transform: rotateX(55deg) rotateZ(-45deg);
              transform-style: preserve-3d;">
    <!-- Grid cells -->
    <div style="width: 80px; height: 80px; background: var(--card);
                border: 1px solid var(--card-border); border-radius: 4px;
                transition: transform 0.3s ease;
                display: flex; align-items: center; justify-content: center;
                color: var(--muted-foreground); font-size: 12px;"
         onmouseenter="this.style.transform='translateZ(20px)'"
         onmouseleave="this.style.transform='translateZ(0)'">01</div>
    <!-- Repeat for more cells... -->
  </div>
</div>
```

---

## 4. Parallax Depth Layers

Multi-layer mouse-tracking parallax with different movement speeds.

```html
<div id="parallax-container" style="position: relative; height: 300px;
     overflow: hidden; border-radius: 16px;
     background: linear-gradient(180deg, #0a0a2e 0%, #1a1a3e 100%);">
  <!-- Background layer (slowest) -->
  <div class="parallax-layer" data-depth="0.1"
       style="position: absolute; inset: -20px;">
    <!-- Stars or dots -->
  </div>
  <!-- Mid layer -->
  <div class="parallax-layer" data-depth="0.3"
       style="position: absolute; inset: -20px;">
    <!-- Shapes -->
  </div>
  <!-- Foreground layer (fastest) -->
  <div class="parallax-layer" data-depth="0.6"
       style="position: absolute; inset: -20px;">
    <!-- Main content -->
  </div>
</div>

<script>
const container = document.getElementById('parallax-container');
container.addEventListener('mousemove', (e) => {
  const rect = container.getBoundingClientRect();
  const x = (e.clientX - rect.left) / rect.width - 0.5;
  const y = (e.clientY - rect.top) / rect.height - 0.5;
  container.querySelectorAll('.parallax-layer').forEach(layer => {
    const depth = parseFloat(layer.dataset.depth);
    const moveX = x * depth * 40;
    const moveY = y * depth * 40;
    layer.style.transform = `translate(${moveX}px, ${moveY}px)`;
  });
});
</script>
```

---

## 5. Card Flip

3D card with front and back faces, flips on hover or click.

```html
<div style="perspective: 1000px; width: 200px; height: 260px;">
  <div class="flip-card" style="position: relative; width: 100%;
       height: 100%; transition: transform 0.6s ease;
       transform-style: preserve-3d; cursor: pointer;"
       onclick="this.classList.toggle('flipped')">
    <!-- Front -->
    <div style="position: absolute; inset: 0; backface-visibility: hidden;
                background: var(--card); border: 1px solid var(--card-border);
                border-radius: 12px; padding: 20px;
                display: flex; align-items: center; justify-content: center;">
      <span style="color: var(--foreground);">Front Face</span>
    </div>
    <!-- Back -->
    <div style="position: absolute; inset: 0; backface-visibility: hidden;
                transform: rotateY(180deg);
                background: linear-gradient(135deg, #6366f1, #8b5cf6);
                border-radius: 12px; padding: 20px;
                display: flex; align-items: center; justify-content: center;">
      <span style="color: white;">Back Face</span>
    </div>
  </div>
</div>

<style>
.flip-card.flipped { transform: rotateY(180deg); }
</style>
```

---

## 6. Floating Elements

CSS keyframe animation for elements that gently float/bob.

```css
@keyframes float-1 {
  0%, 100% { transform: translateY(0) rotate(0deg); }
  25% { transform: translateY(-8px) rotate(1deg); }
  75% { transform: translateY(4px) rotate(-1deg); }
}

@keyframes float-2 {
  0%, 100% { transform: translateY(0) rotate(0deg); }
  50% { transform: translateY(-12px) rotate(-2deg); }
}

.float-slow { animation: float-1 6s ease-in-out infinite; }
.float-medium { animation: float-2 4s ease-in-out infinite; }
.float-fast { animation: float-1 3s ease-in-out infinite; }
```

---

## 7. 3D Button Press

Buttons with physical depth that press down on click.

```html
<button style="
  padding: 12px 28px;
  background: var(--primary);
  color: var(--primary-foreground);
  border: none;
  border-radius: 8px;
  font-size: 14px;
  font-weight: 600;
  cursor: pointer;
  transform: translateY(0);
  box-shadow: 0 4px 0 rgba(0,0,0,0.3), 0 6px 12px rgba(0,0,0,0.15);
  transition: all 0.1s ease;
" onmousedown="this.style.transform='translateY(4px)';this.style.boxShadow='0 0 0 rgba(0,0,0,0.3), 0 2px 4px rgba(0,0,0,0.15)'"
  onmouseup="this.style.transform='translateY(0)';this.style.boxShadow='0 4px 0 rgba(0,0,0,0.3), 0 6px 12px rgba(0,0,0,0.15)'"
  onmouseleave="this.style.transform='translateY(0)';this.style.boxShadow='0 4px 0 rgba(0,0,0,0.3), 0 6px 12px rgba(0,0,0,0.15)'">
  Press Me
</button>
```

---

## 8. Layered Depth Shadows

Progressive multi-shadow technique for realistic depth.

```css
/* Subtle elevation */
.shadow-sm-3d {
  box-shadow:
    0 1px 2px rgba(0,0,0,0.05),
    0 2px 4px rgba(0,0,0,0.05),
    0 4px 8px rgba(0,0,0,0.05);
}

/* Medium elevation */
.shadow-md-3d {
  box-shadow:
    0 2px 4px rgba(0,0,0,0.04),
    0 4px 8px rgba(0,0,0,0.06),
    0 8px 16px rgba(0,0,0,0.08),
    0 16px 32px rgba(0,0,0,0.06);
}

/* High elevation (floating card) */
.shadow-lg-3d {
  box-shadow:
    0 4px 6px rgba(0,0,0,0.04),
    0 8px 15px rgba(0,0,0,0.06),
    0 16px 30px rgba(0,0,0,0.08),
    0 32px 60px rgba(0,0,0,0.1),
    0 64px 120px rgba(0,0,0,0.06);
}
```

---

## 9. CSS 3D Carousel

Rotating carousel of panels arranged in 3D space.

```html
<div style="perspective: 1000px; display: flex;
            justify-content: center; padding: 40px;">
  <div id="carousel" style="width: 160px; height: 200px;
       transform-style: preserve-3d; transition: transform 1s ease;
       position: relative;">
    <!-- Panels positioned around a circle -->
    <!-- Each panel: rotateY(N * 60deg) translateZ(200px) for 6 panels -->
  </div>
</div>

<script>
const carousel = document.getElementById('carousel');
let angle = 0;
setInterval(() => {
  angle += 60; // 360/6 panels
  carousel.style.transform = `rotateY(${angle}deg)`;
}, 3000);
</script>
```
