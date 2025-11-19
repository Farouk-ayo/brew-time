<template>
  <button
    :class="[
      'relative w-10 h-10 rounded-full flex items-center justify-center transition-colors shrink-0',
      customClass || 'bg-brew-tan/5 hover:bg-brew-tan/30',
    ]"
    @click="emit('click')"
  >
    <!-- Badge -->
    <span
      v-if="badge && badge > 0"
      :class="[
        'absolute -top-1 -right-1 min-w-5 h-5 px-1 text-xs font-bold rounded-full flex items-center justify-center',
        badgeClass || 'bg-brew-tan text-brew-dark',
      ]"
    >
      {{ badge > 9 ? '9+' : badge }}
    </span>

    <!-- Cart Icon -->
    <svg
      v-if="icon === 'cart'"
      :class="iconClass || 'w-5 h-5 text-brew-cream'"
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

    <!-- Search Icon -->
    <svg
      v-if="icon === 'search'"
      :class="iconClass || 'w-5 h-5 text-brew-cream'"
      fill="none"
      stroke="currentColor"
      viewBox="0 0 24 24"
    >
      <path
        stroke-linecap="round"
        stroke-linejoin="round"
        stroke-width="2"
        d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"
      />
    </svg>

    <!-- User Icon -->
    <svg
      v-else-if="icon === 'user'"
      :class="iconClass || 'w-5 h-5 text-brew-cream'"
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
      :class="iconClass || 'w-5 h-5 text-brew-cream'"
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

    <svg
      v-else-if="icon === 'menu'"
      :class="iconClass || 'w-5 h-5 text-brew-cream'"
      fill="none"
      stroke="currentColor"
      viewBox="0 0 24 24"
    >
      <path
        stroke-linecap="round"
        stroke-linejoin="round"
        stroke-width="2"
        d="M4 6h16M4 12h16M4 18h16"
      />
    </svg>

    <svg
      v-else-if="icon === 'close'"
      class="w-5 h-5 text-brew-cream"
      fill="none"
      stroke="currentColor"
      viewBox="0 0 24 24"
    >
      <path
        stroke-linecap="round"
        stroke-linejoin="round"
        stroke-width="2"
        d="M6 18L18 6M6 6l12 12"
      />
    </svg>
  </button>
</template>

<script setup lang="ts">
interface Props {
  icon: string
  badge?: number
  customClass?: string
  iconClass?: string
  badgeClass?: string
}

defineProps<Props>()

const emit = defineEmits<{
  click: []
}>()
</script>
