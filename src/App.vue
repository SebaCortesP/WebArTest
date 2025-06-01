<template>
  <component :is="currentView" />
  
</template>

<script setup>
import ScannerView from './views/ScannerView.vue'
import ARViewerView from './views/ARViewerView.vue'

const path = window.location.pathname
const currentView = path.includes('ar-viewer') ? ARViewerView : ScannerView
</script>
