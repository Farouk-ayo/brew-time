<template>
  <div class="relative min-h-screen w-full overflow-hidden bg-brew-dark">
    <!-- Background Image -->
    <div class="absolute inset-0">
      <img
        src="@/assets/images/bg-coffee-shop.png"
        alt="Coffee Shop"
        class="w-full h-full object-cover"
      />
      <div class="absolute inset-0 bg-black/65"></div>
    </div>

    <!-- Repeating Pattern Background (Outline Logos) -->
    <div class="absolute inset-0 overflow-hidden z-40">
      <div class="grid grid-cols-4 gap-8 p-8">
        <img
          v-for="i in 16"
          :key="i"
          src="@/assets/icons/brewtime-outline.svg"
          alt=""
          class="w-64 h-32 object-contain"
        />
      </div>
    </div>

    <!-- Main Content -->
    <div class="relative z-10 flex flex-col items-center justify-center min-h-screen" ref="content">
      <!-- Main Logo -->
      <div class="mb-16 animate-fade-in">
        <img src="@/assets/icons/brewtime.svg" alt="BrewTime" class="w-96 h-auto" />
      </div>

      <!-- Bottom Section -->
      <div class="flex items-center gap-16 text-white">
        <div class="">
          <img src="@/assets/icons/horizontalLine.svg" alt="BrewTime Logo" />
        </div>
        <div class="flex items-center gap-4">
          <img src="@/assets/icons/rage-media.svg" alt="BrewTime Logo" />
        </div>
        <div class="">
          <img src="@/assets/icons/horizontalLine.svg" alt="BrewTime Logo" />
        </div>
        <div class="">
          <h2 class="text-base md:text-4xl font-bold">Assessment Test</h2>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
// import { ref, onMounted } from 'vue'
// import { useRouter } from 'vue-router'
// import gsap from 'gsap'

// const router = useRouter()
const content = ref<HTMLElement | null>(null)

// onMounted(() => {
//   if (content.value) {
//     // Fade in animation
//     gsap.from(content.value.children, {
//       opacity: 0,
//       y: 30,
//       duration: 1,
//       stagger: 0.3,
//       ease: 'power3.out',
//     })

//     // Auto redirect after 3 seconds (optional)
//     setTimeout(() => {
//       router.push('/home')
//     }, 10000)
//   }
// })
</script>

<style scoped>
@keyframes fade-in {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.animate-fade-in {
  animation: fade-in 1s ease-out;
}
</style>
