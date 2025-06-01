<template>
  <div style="margin: 0; overflow: hidden">
    <a-scene
      embedded
      arjs="sourceType: webcam; debugUIEnabled: false;"
    >
      <a-marker preset="hiro">
        <a-entity
          id="model"
          :gltf-model="modelUrl"
          scale="0.5 0.5 0.5"
        ></a-entity>
      </a-marker>
      <a-entity camera></a-entity>
    </a-scene>
  </div>
  <!-- Importamos A-Frame y AR.js directamente -->
<!-- <script src="https://aframe.io/releases/1.4.1/aframe.min.js"></script>
<script src="https://cdn.jsdelivr.net/gh/AR-js-org/AR.js/aframe/build/aframe-ar.min.js"></script> -->
</template>

<script setup>
import { onMounted, ref } from 'vue'

const modelUrl = ref('')

onMounted(() => {
  const urlParams = new URLSearchParams(window.location.search)
  modelUrl.value = urlParams.get('model') || '/modelos/silla.glb'
})
</script>


