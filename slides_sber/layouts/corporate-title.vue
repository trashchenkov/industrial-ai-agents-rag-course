<template>
  <div class="slidev-layout corporate-title">
    <img
      v-if="showLogo"
      :src="logoSrc"
      class="corporate-logo"
      alt=""
    />
    <div class="title-content">
      <slot />
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue'
// Логотип: после extract из .pptx положите файл в public/ (имя из design.json → mediaRefs role "image")
const logoSrc = ref('/image32.png')
const showLogo = ref(false)
onMounted(() => {
  const img = new Image()
  img.onerror = () => { showLogo.value = false }
  img.onload = () => { showLogo.value = true }
  img.src = logoSrc.value
})
</script>

<style scoped>
.corporate-title {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  text-align: center;
  padding: 2rem;
}

.corporate-logo {
  position: absolute;
  top: 1.5rem;
  right: 1.5rem;
  height: 2.5rem;
  width: auto;
  object-fit: contain;
}

.title-content {
  width: 100%;
}

.title-content :deep(h1) {
  font-size: 3rem;
  font-weight: 600;
  margin-bottom: 0.5em;
}

.title-content :deep(p) {
  font-size: 1.25rem;
  opacity: 0.95;
}
</style>
