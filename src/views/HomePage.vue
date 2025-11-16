<template>
  <TheNavbar />
  <!-- Hero Section -->
  <section class="relative min-h-screen flex items-center justify-center px-4 lg:px-16 py-40">
    <!-- <TheNavbar /> -->

    <!-- Background Image with Overlay -->
    <div class="absolute inset-0 w-full h-full">
      <!-- Desktop Background -->
      <img
        src="@/assets/images/bg-home.png"
        alt=""
        class="hidden md:block w-full h-full object-cover"
      />
      <!-- Mobile Background -->
      <img
        src="@/assets/images/bg-home-mobile.png"
        alt=""
        class="block md:hidden w-full h-full object-cover"
      />
      <div class="absolute inset-0 bg-black/65"></div>
      <div class="absolute inset-0 bg-linear-to-b from-transparent via-black/10 to-black/65"></div>
    </div>

    <!-- Main Content -->
    <div ref="heroContent" class="relative z-10 text-center px-4 sm:px-6 lg:px-8 max-w-6xl mx-auto">
      <!-- Main Heading -->
      <div class="mb-2 sm:mb-4">
        <h1
          class="text-4xl sm:text-5xl md:text-7xl lg:text-8xl xl:text-9xl font-bold text-brew-cream leading-tight tracking-tight"
        >
          "SAVOR THE MOMENT
        </h1>
      </div>

      <div class="mb-2 sm:mb-4">
        <h1
          class="text-4xl sm:text-5xl md:text-7xl lg:text-8xl xl:text-9xl font-bold text-brew-cream leading-tight tracking-tight"
        >
          WITH EVERY SIP"
        </h1>
      </div>

      <!-- Subtitle -->
      <p
        class="text-base sm:text-lg md:text-xl text-brew-cream/70 mb-8 sm:mb-10 md:mb-12 max-w-3xl mx-auto px-4"
      >
        Discover our carefully crafted coffee blends, made with love and passion
      </p>

      <!-- CTA Buttons -->
      <div
        class="flex flex-col sm:flex-row gap-3 sm:gap-4 justify-center items-center w-full sm:w-auto"
      >
        <BaseButton variant="secondary" size="lg" to="/about" class="w-full sm:w-auto">
          About
        </BaseButton>
        <BaseButton variant="primary" size="lg" @click="handleOrderNow" class="w-full sm:w-auto">
          Order Now
        </BaseButton>
      </div>
    </div>
  </section>
  <TheFooter />
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue'
import { useRouter } from 'vue-router'
import gsap from 'gsap'
import BaseButton from '@/components/ui/BaseButton.vue'
import TheNavbar from '@/components/layout/TheNavbar.vue'
import TheFooter from '@/components/layout/TheFooter.vue'

const router = useRouter()
const heroContent = ref<HTMLElement | null>(null)

const handleOrderNow = () => {
  router.push('/menu')
}

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
