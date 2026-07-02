<script setup lang="ts">
</script>

<template>
  <div class="base-layout">
    <main class="content">
      <RouterView />
    </main>
  </div>
</template>

<style scoped>
.base-layout {
  min-height: 100vh;
}

.content {
  min-height: 100vh;
}

@media screen and (orientation: portrait) and (hover: none) and (pointer: coarse) {
  .base-layout,
  .content {
    min-height: var(--vw, 100vw);
  }
}
</style>
