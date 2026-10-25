# Creating a 3D Web Preview with Blender and Three.js

## 1. Overview

**Three.js** is a JavaScript library that allows you to display and interact with 3D objects directly in a web browser.

You can create a model in Blender, export it as a `.glb` file, and use Three.js to display it on your website.

The process is simple:

**Blender → Export** **.glb** **→ Load with Three.js → Display in the browser**

## 2. What You Need

- **Blender:** To create your 3D model.
- **Three.js:** To render the 3D scene.
- **GLTFLoader:** To import your Blender model.
- **OrbitControls:** To allow users to rotate and zoom around the object.

Useful resources:

- Three.js: [https://threejs.org/](https://threejs.org/)
- Documentation: [https://threejs.org/docs/](https://threejs.org/docs/)
- Blender: [https://www.blender.org/](https://www.blender.org/)

## 3. Export the Model from Blender

In Blender, select your model and go to:

**File → Export → glTF 2.0 → glTF Binary (.glb)**

Save the file as `model.glb`.

The GLB format is convenient because it can contain the model's geometry, materials, textures, and animations in a single file.

## 4. The Basic Structure of a Three.js Scene

A simple 3D scene requires three essential elements:

- **Scene:** The environment containing your objects and lights.
- **Camera:** Determines what the viewer sees.
- **Renderer:** Draws the scene in the browser.

You can then add a 3D model, lighting, and controls.

## 5. A Very Simple Example

Create an `index.html` file and place your exported `model.glb` in the same folder.

The following example creates a scene, loads the Blender model, and allows the visitor to rotate it.

> [!important] Your project should look like this:

> [!folder] Structure
> - 📁 my-3d-website/
> 	- 📄 index.html
> 	- 📄 my-model.glb

```js
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>My 3D Preview</title>
  <style>
    body { margin: 0; }
    #viewer { width: 100%; height: 500px; }
  </style>
</head>
<body>

  <div id="viewer"></div>

  <script type="importmap">
  {
    "imports": {
      "three": "https://cdn.jsdelivr.net/npm/three@0.180.0/build/three.module.js",
      "three/addons/": "https://cdn.jsdelivr.net/npm/three@0.180.0/examples/jsm/"
    }
  }
  </script>

  <script type="module">
    import * as THREE from 'three';
    import { GLTFLoader } from
      'three/addons/loaders/GLTFLoader.js';
    import { OrbitControls } from
      'three/addons/controls/OrbitControls.js';

    // Create the scene
    const scene = new THREE.Scene();
    scene.background = new THREE.Color('#eeeeee');

    // Create the camera
    const camera = new THREE.PerspectiveCamera(
      45, window.innerWidth / 500, 0.1, 1000
    );
    camera.position.set(0, 1, 5);

    // Create the renderer
    const viewer = document.getElementById('viewer');
    const renderer = new THREE.WebGLRenderer({
      antialias: true
    });
    renderer.setSize(window.innerWidth, 500);
    viewer.appendChild(renderer.domElement);

    // Add lighting
    scene.add(new THREE.HemisphereLight(
      0xffffff, 0x444444, 3
    ));

    // Enable rotation and zoom
    const controls = new OrbitControls(
      camera, renderer.domElement
    );

    // Load the Blender model
    const loader = new GLTFLoader();

    loader.load('model.glb', (gltf) => {
      const model = gltf.scene;
      scene.add(model);
    });

    // Render the scene
    function animate() {
      requestAnimationFrame(animate);
      controls.update();
      renderer.render(scene, camera);
    }

    animate();
  </script>

</body>
</html>
```

Run the page using a local web server, such as VS Code Live Server.

## 6. How the Library Works

The most important parts are:

|Code|Purpose|
|---|---|
|`THREE.Scene()`|Creates the 3D environment|
|`THREE.PerspectiveCamera()`|Defines the viewing angle|
|`THREE.WebGLRenderer()`|Displays the scene|
|`GLTFLoader()`|Imports the Blender model|
|`OrbitControls()`|Enables rotation and zoom|
|`renderer.render()`|Draws the scene|

---

# Three.js — Importing and Using a 3D Model

### 1. Import the library

```js
import * as THREE from 'three';

import { GLTFLoader } from
  'three/addons/loaders/GLTFLoader.js';

import { OrbitControls } from
  'three/addons/controls/OrbitControls.js';
```

### 2. Create the basic scene

```js
const scene = new THREE.Scene();

const camera = new THREE.PerspectiveCamera(
  45,
  window.innerWidth / window.innerHeight,
  0.1,
  1000
);

camera.position.set(0, 1, 5);

const renderer = new THREE.WebGLRenderer({
  antialias: true
});

renderer.setSize(window.innerWidth, window.innerHeight);

document.body.appendChild(renderer.domElement);
```

### 3. Add lighting and controls

```js
const light = new THREE.HemisphereLight(
  0xffffff,
  0x444444,
  3
);

scene.add(light);

const controls = new OrbitControls(
  camera,
  renderer.domElement
);
```

### 4. Import the Blender model

```js
const loader = new GLTFLoader();

loader.load('model.glb', (gltf) => {
  const model = gltf.scene;

  scene.add(model);
});
```

### 5. Use and animate the model

```js
let model;

loader.load('model.glb', (gltf) => {
  model = gltf.scene;
  scene.add(model);
});

function animate() {
  requestAnimationFrame(animate);

  if (model) {
    model.rotation.y += 0.01;
  }

  controls.update();
  renderer.render(scene, camera);
}

animate();
```

### 6. Remember

- `THREE` — creates scenes, cameras, lights, and 3D objects.
- `GLTFLoader` — loads models exported from Blender as `.glb` or `.gltf`.
- `OrbitControls` — enables interactive rotation and zoom.
- `scene.add(model)` — adds the imported model to the scene.
- `model.rotation.y` — rotates the model around its vertical axis.

**Note:** These snippets are separate building blocks. In a complete implementation, load the model only once, inside the fifth section's loader callback, and use the same `model` variable in your animation loop. Run the code in a JavaScript module using a local web server.

---
