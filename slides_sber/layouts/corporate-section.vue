<template>
  <div class="slidev-layout corporate-section">
    <img
      v-if="showLogo"
      :src="logoSrc"
      class="corporate-logo"
      alt=""
    />
    <div class="section-content">
      <slot />
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue'
const logoSrc = '/image32.png'
const showLogo = ref(false)
onMounted(() => {
  const img = new Image()
  img.onerror = () => { showLogo.value = false }
  img.onload = () => { showLogo.value = true }
  img.src = logoSrc
})
</script>

<style scoped>
.corporate-section {
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

.section-content :deep(h1),
.section-content :deep(h2) {
  font-size: 2.5rem;
  font-weight: 600;
}
</style>
