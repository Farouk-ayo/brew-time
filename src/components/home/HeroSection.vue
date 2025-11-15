<template>
  <section class="relative min-h-screen flex items-center justify-center overflow-hidden">
    <!-- Background with image (add your coffee shop image) -->
    <div class="absolute inset-0 bg-linear-to-br from-brew-dark to-brew-brown opacity-90"></div>

    <!-- Content -->
    <div class="relative z-10 text-center px-4" ref="heroContent">
      <h1 class="text-6xl md:text-8xl font-barna text-brew-cream mb-6">
        "Savor the moment<br />with every sip"
      </h1>
      <p class="text-xl text-brew-cream/80 mb-8 max-w-2xl mx-auto">
        Discover our carefully blended coffee blends, made with love and passion
      </p>

      <div class="flex gap-4 justify-center">
        <button
          class="px-8 py-3 bg-transparent border-2 border-brew-cream text-brew-cream hover:bg-brew-cream hover:text-brew-dark transition-all"
        >
          About
        </button>
        <button class="px-8 py-3 bg-brew-tan text-brew-dark hover:bg-brew-tan/90 transition-all">
          Order Now
        </button>
      </div>
    </div>

    <!-- Scroll indicator -->
    <div class="absolute bottom-8 left-1/2 -translate-x-1/2">
      <div
        class="w-6 h-10 border-2 border-brew-cream rounded-full flex items-start justify-center p-2"
      >
        <div class="w-1 h-3 bg-brew-cream rounded-full animate-bounce"></div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue'
import gsap from 'gsap'

const heroContent = ref<HTMLElement | null>(null)

onMounted(() => {
  if (heroContent.value) {
    gsap.from(heroContent.value.children, {
      y: 50,
      opacity: 0,
      duration: 1,
      stagger: 0.2,
      ease: 'power3.out',
    })
  }
})
</script>
