<template>
  <TheNavbar />

  <!-- Hero Section -->
  <section class="relative min-h-screen flex items-center justify-center px-4 lg:px-16 py-40">
    <!-- Background Image with Overlay -->
    <div class="absolute inset-0">
      <!-- Desktop Background -->
      <img
        src="@/assets/images/bg-about.png"
        alt=""
        class="hidden md:block w-full h-full object-cover"
      />
      <!-- Mobile Background -->
      <img
        src="@/assets/images/bg-about-mobile.png"
        alt=""
        class="block md:hidden w-full h-full object-cover"
      />
      <div class="absolute inset-0 bg-black/70"></div>
    </div>

    <!-- Content -->
    <div class="relative z-10 text-center px-4 sm:px-6">
      <h1
        class="text-6xl sm:text-7xl md:text-8xl lg:text-9xl font-bold text-brew-cream tracking-tight"
      >
        ABOUT
      </h1>
    </div>
  </section>

  <!-- About Content Section -->
  <section class="py-12 sm:py-16 px-4 sm:px-6 lg:px-8">
    <div class="max-w-7xl mx-auto">
      <!-- Your about content will go here -->
      <p class="text-brew-cream text-center text-lg sm:text-xl">About content coming soon...</p>
    </div>
  </section>
  <TheFooter />
</template>

<script setup lang="ts">
import TheFooter from '@/components/layout/TheFooter.vue'
import TheNavbar from '@/components/layout/TheNavbar.vue'
</script>
