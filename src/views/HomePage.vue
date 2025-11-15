<template>
  <PageLayout>
    <!-- Hero Section with Background Image -->
    <section class="relative min-h-screen flex items-center justify-center">
      <!-- Background Image with Overlay -->
      <div class="absolute inset-0">
        <!-- Add your coffee shop image here -->
        <div class="absolute inset-0 bg-black/60"></div>
        <div
          class="absolute inset-0 bg-linear-to-b from-transparent via-black/40 to-black/80"
        ></div>
      </div>

      <!-- Decorative Outline Logos (Background Pattern) -->
      <div class="absolute inset-0 overflow-hidden opacity-5">
        <BrewTimeOutline
          v-for="i in 8"
          :key="i"
          :width="400"
          :height="200"
          :style="{
            position: 'absolute',
            top: `${Math.random() * 100}%`,
            left: `${Math.random() * 100}%`,
            transform: `rotate(${Math.random() * 360}deg)`,
          }"
          class="text-brew-cream"
        />
      </div>

      <!-- Main Content -->
      <div class="relative z-10 text-center px-4 max-w-5xl" ref="heroContent">
        <!-- Main Heading with Quotes -->
        <div class="mb-8">
          <div class="text-8xl md:text-9xl font-bold text-brew-cream leading-none mb-2">
            <span class="text-brew-cream/80">"</span>SAVOR THE MOMENT
          </div>
          <div class="text-8xl md:text-9xl font-bold text-brew-cream leading-none">
            WITH EVERY SIP<span class="text-brew-cream/80">"</span>
          </div>
        </div>

        <!-- Subtitle -->
        <p class="text-xl text-brew-cream/70 mb-12 max-w-3xl mx-auto">
          Discover our carefully crafted coffee blends, made with love and passion
        </p>

        <!-- CTA Buttons -->
        <div class="flex gap-4 justify-center">
          <RouterLink
            to="/about"
            class="px-10 py-4 bg-white text-brew-dark rounded-lg font-semibold text-lg hover:bg-brew-cream transition-all hover:scale-105 transform"
          >
            About
          </RouterLink>
          <button
            class="px-10 py-4 bg-brew-tan text-brew-dark rounded-lg font-semibold text-lg hover:bg-brew-tan/90 transition-all hover:scale-105 transform"
          >
            Order Now
          </button>
        </div>
      </div>
    </section>
  </PageLayout>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue'
import gsap from 'gsap'
import PageLayout from '@/components/layout/PageLayout.vue'

const heroContent = ref<HTMLElement | null>(null)

onMounted(() => {
  if (heroContent.value) {
    gsap.from(heroContent.value.children, {
      y: 100,
      opacity: 0,
      duration: 1.2,
      stagger: 0.2,
      ease: 'power3.out',
    })
  }
})
</script>
