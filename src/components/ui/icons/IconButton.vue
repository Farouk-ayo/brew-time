<template>
  <button
    class="relative w-10 h-10 rounded-full bg-brew-tan/20 flex items-center justify-center hover:bg-brew-tan/30 transition-colors flex-shrink-0"
    @click="emit('click')"
  >
    <!-- Badge -->
    <span
      v-if="badge && badge > 0"
      class="absolute -top-1 -right-1 min-w-[20px] h-5 px-1 bg-brew-tan text-brew-dark text-xs font-bold rounded-full flex items-center justify-center"
    >
      {{ badge > 9 ? '9+' : badge }}
    </span>

    <!-- Cart Icon -->
    <svg
      v-if="icon === 'cart'"
      class="w-5 h-5 text-brew-cream"
      fill="none"
      stroke="currentColor"
      viewBox="0 0 24 24"
    >
      <path
        stroke-linecap="round"
        stroke-linejoin="round"
        stroke-width="2"
        d="M3 3h2l.4 2M7 13h10l4-8H5.4M7 13L5.4 5M7 13l-2.293 2.293c-.63.63-.184 1.707.707 1.707H17m0 0a2 2 0 100 4 2 2 0 000-4zm-8 2a2 2 0 11-4 0 2 2 0 014 0z"
      />
    </svg>

    <!-- User Icon -->
    <svg
      v-else-if="icon === 'user'"
      class="w-5 h-5 text-brew-cream"
      fill="none"
      stroke="currentColor"
      viewBox="0 0 24 24"
    >
      <path
        stroke-linecap="round"
        stroke-linejoin="round"
        stroke-width="2"
        d="M16 7a4 4 0 11-8 0 4 4 0 018 0zM12 14a7 7 0 00-7 7h14a7 7 0 00-7-7z"
      />
    </svg>

    <!-- Wishlist Icon -->
    <svg
      v-else-if="icon === 'wishlist'"
      class="w-5 h-5 text-brew-cream"
      fill="none"
      stroke="currentColor"
      viewBox="0 0 24 24"
    >
      <path
        stroke-linecap="round"
        stroke-linejoin="round"
        stroke-width="2"
        d="M4.318 6.318a4.5 4.5 0 000 6.364L12 20.364l7.682-7.682a4.5 4.5 0 00-6.364-6.364L12 7.636l-1.318-1.318a4.5 4.5 0 00-6.364 0z"
      />
    </svg>
  </button>
</template>

<script setup lang="ts">
interface Props {
  icon: 'cart' | 'user' | 'wishlist'
  badge?: number
}

defineProps<Props>()

const emit = defineEmits<{
  click: []
}>()
</script>
