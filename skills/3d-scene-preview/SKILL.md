---
name: 3d-scene-preview
description: >-
  Use this skill when the user wants a full 3D scene preview with real
  3D models, lighting, materials, and orbit controls. Creates a standalone
  HTML file with Three.js that the user opens in their browser. Activate
  when the user says things like "create a 3D scene", "show a rotating
  model", "Three.js preview", or "3D with orbit controls".
---

# Create a Three.js 3D Scene Preview

Create standalone HTML files with full Three.js 3D scenes. These are
saved to disk and opened in a browser — they cannot render inline in
chat due to CSP restrictions on external CDNs.

## When to Use

- User wants real 3D geometry, models, or complex materials
- Scenes requiring orbit/zoom/pan controls
- Product showcases with realistic lighting and reflections
- Any design that requires WebGL rendering

## Steps

1. **Understand the scene requirements**:
   - What objects? (geometric shapes, 3D models, text)
   - What lighting? (studio, dramatic, ambient, neon)
   - What background? (gradient, solid color, environment map)
   - What interaction? (orbit controls, auto-rotation, click events)
   - What mood? (dark & moody, bright & clean, colorful & playful)

2. **Create a self-contained HTML file** with:
   - Three.js loaded via ESM import map (esm.sh CDN)
   - OrbitControls for interactive exploration
   - Proper lighting setup
   - Responsive window handling
   - Capped pixel ratio

3. **Save to the project directory** (or artifact directory if no project)
   and tell the user to open it in their browser.

## Base Template

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>3D Scene Preview</title>
  <style>
    * { margin: 0; padding: 0; box-sizing: border-box; }
    body { overflow: hidden; background: #0a0a0a; }
    canvas { display: block; }
    #info {
      position: absolute;
      bottom: 16px;
      left: 50%;
      transform: translateX(-50%);
      color: rgba(255,255,255,0.5);
      font-family: system-ui, sans-serif;
      font-size: 12px;
      pointer-events: none;
    }
  </style>
  <script type="importmap">
    {
      "imports": {
        "three": "https://esm.sh/three@0.170.0",
        "three/addons/": "https://esm.sh/three@0.170.0/examples/jsm/"
      }
    }
  </script>
</head>
<body>
  <div id="info">Drag to orbit · Scroll to zoom</div>
  <script type="module">
    import * as THREE from 'three';
    import { OrbitControls } from 'three/addons/controls/OrbitControls.js';

    // --- Scene ---
    const scene = new THREE.Scene();
    scene.background = new THREE.Color(0x0a0a0a);

    // --- Camera ---
    const camera = new THREE.PerspectiveCamera(
      45, window.innerWidth / window.innerHeight, 0.1, 1000
    );
    camera.position.set(0, 2, 5);

    // --- Renderer ---
    const renderer = new THREE.WebGLRenderer({ antialias: true });
    renderer.setSize(window.innerWidth, window.innerHeight);
    renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));
    renderer.toneMapping = THREE.ACESFilmicToneMapping;
    renderer.toneMappingExposure = 1.2;
    document.body.appendChild(renderer.domElement);

    // --- Controls ---
    const controls = new OrbitControls(camera, renderer.domElement);
    controls.enableDamping = true;
    controls.dampingFactor = 0.05;
    controls.autoRotate = true;
    controls.autoRotateSpeed = 1.0;

    // --- Lighting ---
    const ambientLight = new THREE.AmbientLight(0xffffff, 0.4);
    scene.add(ambientLight);

    const mainLight = new THREE.DirectionalLight(0xffffff, 1.5);
    mainLight.position.set(5, 8, 5);
    mainLight.castShadow = true;
    scene.add(mainLight);

    const fillLight = new THREE.DirectionalLight(0x8b5cf6, 0.6);
    fillLight.position.set(-5, 2, -5);
    scene.add(fillLight);

    // --- Objects ---
    // ADD YOUR 3D OBJECTS HERE

    // --- Resize ---
    window.addEventListener('resize', () => {
      camera.aspect = window.innerWidth / window.innerHeight;
      camera.updateProjectionMatrix();
      renderer.setSize(window.innerWidth, window.innerHeight);
    });

    // --- Animate ---
    const clock = new THREE.Clock();
    function animate() {
      requestAnimationFrame(animate);
      const delta = clock.getDelta();
      const elapsed = clock.getElapsedTime();
      controls.update();
      renderer.render(scene, camera);
    }
    animate();
  </script>
</body>
</html>
```

## Common Scene Recipes

### Floating Geometric Shapes
Add multiple geometric shapes with different materials, positions,
and subtle animations (rotation, bobbing). Use `MeshStandardMaterial`
with metalness and roughness for a polished look.

### Product on Pedestal
Center a 3D model on a circular platform (`CylinderGeometry` with
small height). Add a `ContactShadow` plane below. Use studio lighting
(key light from top-right, fill from left, rim light from behind).

### Particle Field
Create a `BufferGeometry` with thousands of random points. Use
`PointsMaterial` with small size and additive blending for a starfield
or particle effect. Animate rotation slowly.

### Gradient Background
Instead of a solid `scene.background`, use a full-screen quad with a
`ShaderMaterial` that renders a gradient. Or use CSS gradient on the
body and set `renderer.setClearColor` to transparent with `alpha: true`.

## Loading 3D Models

To load `.glb` models from free sources:

```javascript
import { GLTFLoader } from 'three/addons/loaders/GLTFLoader.js';
import { DRACOLoader } from 'three/addons/loaders/DRACOLoader.js';

const dracoLoader = new DRACOLoader();
dracoLoader.setDecoderPath('https://www.gstatic.com/draco/versioned/decoders/1.5.7/');

const gltfLoader = new GLTFLoader();
gltfLoader.setDRACOLoader(dracoLoader);

gltfLoader.load('https://example.com/model.glb', (gltf) => {
  const model = gltf.scene;
  model.scale.set(1, 1, 1);
  scene.add(model);
});
```

## Adding Environment Maps (HDRIs)

```javascript
import { RGBELoader } from 'three/addons/loaders/RGBELoader.js';

new RGBELoader()
  .load('https://dl.polyhaven.org/file/ph-assets/HDRIs/hdr/1k/studio_small_09_1k.hdr',
    (texture) => {
      texture.mapping = THREE.EquirectangularReflectionMapping;
      scene.environment = texture;
      // Optionally: scene.background = texture;
    });
```

## Post-Processing (Bloom)

```javascript
import { EffectComposer } from 'three/addons/postprocessing/EffectComposer.js';
import { RenderPass } from 'three/addons/postprocessing/RenderPass.js';
import { UnrealBloomPass } from 'three/addons/postprocessing/UnrealBloomPass.js';

const composer = new EffectComposer(renderer);
composer.addPass(new RenderPass(scene, camera));
composer.addPass(new UnrealBloomPass(
  new THREE.Vector2(window.innerWidth, window.innerHeight),
  0.5,  // strength
  0.4,  // radius
  0.85  // threshold
));

// In animate loop, replace renderer.render() with:
// composer.render();
```

## Reference
See [Free 3D Resources](./references/free-3d-resources.md) for
curated links to free models, textures, and HDRIs.
