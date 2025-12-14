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

<template>
  <TheNavbar />
  <section class="relative min-h-screen flex items-center justify-center px-4 sm:px-6 lg:px-8">
    <div class="absolute inset-0 w-full h-full">
      <img
        src="@/assets/images/bg-home.webp"
        alt=""
        class="hidden md:block w-full h-full object-cover"
      />
      <img
        src="@/assets/images/bg-home-mobile.webp"
        alt=""
        class="block md:hidden w-full h-full object-cover"
      />
      <div class="absolute inset-0 bg-black/65"></div>
      <div class="absolute inset-0 bg-linear-to-b from-transparent via-black/10 to-black/65"></div>
    </div>

    <div
      ref="heroContent"
      class="relative z-10 text-center items-center max-w-xs md:max-w-3xl mx-auto flex flex-col justify-center pt-20 sm:pt-24 md:pt-28 pb-8"
    >
      <h1
        class="relative text-6xl lg:text-7xl xl:text-8xl text-brew-cream tracking-tight mb-6 sm:mb-8 md:mb-10 px-4 before:content-[''] after:content-[''] before:absolute after:absolute before:w-8 before:h-8 lg:before:w-12 lg:before:h-12 after:w-8 after:h-8 lg:after:w-12 lg:after:h-12 before:bg-[url('@/assets/icons/apostrophe-t.svg')] after:bg-[url('@/assets/icons/apostrophe-b.svg')] before:bg-contain after:bg-contain before:bg-no-repeat after:bg-no-repeat before:top-0 before:left-0 after:bottom-0 after:right-0 before:opacity-90 after:opacity-90"
      >
        SAVOR THE MOMENT WITH EVERY SIP
      </h1>

      <p
        class="text-sm sm:text-base md:text-lg lg:text-xl text-brew-cream/70 mb-6 sm:mb-8 md:mb-10 max-w-3xl mx-auto px-2"
      >
        Discover our carefully crafted coffee blends, made with love and passion
      </p>

      <div
        class="flex flex-col sm:flex-row gap-3 sm:gap-4 justify-center items-stretch sm:items-center px-2"
      >
        <BaseButton
          variant="secondary"
          size="lg"
          to="/about"
          class="w-auto min-w-[140px] hidden! md:inline-block!"
        >
          About
        </BaseButton>
        <BaseButton
          variant="primary"
          size="lg"
          @click="handleOrderNow"
          class="w-auto min-w-[140px]"
        >
          Order Now
        </BaseButton>
      </div>
    </div>
  </section>
  <TheFooter />
</template>
