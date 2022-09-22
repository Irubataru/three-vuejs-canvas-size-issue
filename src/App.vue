<script setup lang="ts">
import { ref, onMounted } from "vue";
import * as THREE from "three";
import { OrbitControls } from "three/examples/jsm/controls/OrbitControls.js";

const canvas = ref<HTMLCanvasElement | null>(null);

onMounted(async () => {
  if (canvas.value === null) {
    return;
  }

  const camera = new THREE.PerspectiveCamera(
    75,
    document.body.clientWidth / document.body.clientHeight,
    0.1,
    1000
  );
  camera.position.set(10, 10, 0);

  // Initialise renderer
  const renderer = new THREE.WebGLRenderer({
    canvas: canvas.value as HTMLCanvasElement,
    antialias: true,
  });
  renderer.setPixelRatio(window.devicePixelRatio);
  renderer.setSize(document.body.clientWidth, document.body.clientHeight);

  console.log(document.body.clientHeight);
  console.log(document.body.clientWidth);

  // Add camera controls
  const camera_controls = new OrbitControls(
    camera,
    canvas.value as HTMLCanvasElement
  );
  camera_controls.minDistance = 0.1;
  camera_controls.maxDistance = 20;

  // Initialise scene
  const scene = new THREE.Scene();
  scene.background = new THREE.Color(0xb0b0b0);

  function animate() {
    requestAnimationFrame(animate);
    renderer.render(scene, camera);
  }

  window.onresize = function() {
    camera.aspect = document.body.clientWidth / document.body.clientHeight;
    camera.updateProjectionMatrix();
    renderer.setSize(document.body.clientWidth, document.body.clientHeight);
  }

  animate();
});
</script>

<template>
  <canvas ref="canvas"></canvas>
</template>
