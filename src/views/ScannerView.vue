<template>
  <div>
    <h2>Escanea un QR</h2>
    <div id="reader" style="width: 300px"></div>
  </div>
</template>

<script setup>
import { onMounted } from 'vue'
import { Html5Qrcode } from 'html5-qrcode'

const fetchModelFromCode = async (code) => {
  try {
    const response = await fetch('/db.json')
    const data = await response.json()

    const item = data.find(entry => entry.code === code)

    if (item) {
      const modelPath = item.model
      window.location.href = `/ar-viewer?model=${encodeURIComponent(modelPath)}`
    } else {
      alert(`No se encontró ningún modelo para el código: ${code}`)
    }
  } catch (error) {
    console.error('Error al buscar modelo en db.json:', error)
    alert('Error al cargar los datos del modelo.')
  }
}

onMounted(() => {
  const html5QrCode = new Html5Qrcode("reader")

  html5QrCode.start(
    { facingMode: "environment" },
    {
      fps: 10,
      qrbox: 250
    },
    async qrCodeMessage => {
      console.log("Código leído:", qrCodeMessage)
      await html5QrCode.stop()
      await fetchModelFromCode(qrCodeMessage)
    },
    errorMessage => {
      // Puedes ocultar esto si te molesta mucho:
      // console.warn("QR error:", errorMessage)
    }
  )
})
</script>
