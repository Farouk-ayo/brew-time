<script setup lang="ts">
import TheNavbar from './TheNavbar.vue'
</script>

<template>
  <div class="min-h-screen bg-brew-dark">
    <TheNavbar />
    <main>
      <slot />
    </main>
  </div>
</template>
