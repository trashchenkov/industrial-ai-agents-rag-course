<template>
  <div class="slidev-layout corporate-default">
    <img
      v-if="showLogo"
      :src="logoSrc"
      class="corporate-logo"
      alt=""
    />
    <div class="slide-content">
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
.corporate-default {
  padding: 2rem 3rem 2rem 2rem;
}

.corporate-logo {
  position: absolute;
  top: 1rem;
  right: 1.5rem;
  height: 2rem;
  width: auto;
  object-fit: contain;
}

.slide-content {
  padding-right: 1rem;
}

.slide-content :deep(h1),
.slide-content :deep(h2) {
  font-size: 2rem;
  font-weight: 600;
  margin-bottom: 0.75em;
}

.slide-content :deep(ul),
.slide-content :deep(ol) {
  padding-left: 1.5em;
}

.slide-content :deep(li) {
  margin-bottom: 0.35em;
}
</style>
