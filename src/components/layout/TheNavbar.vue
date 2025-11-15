<template>
  <nav
    class="fixed top-0 left-0 right-0 z-50 bg-black/80 backdrop-blur-md border-b border-brew-tan/10"
  >
    <div class="max-w-7xl mx-auto px-8">
      <!-- Top Row: Logo, Search, Icons -->
      <div class="flex items-center justify-between py-4">
        <!-- Logo -->
        <RouterLink to="/" class="flex items-center">
          <img src="@/assets/icons/brewtime.svg" alt="BrewTime Logo" class="h-12 w-auto" />
        </RouterLink>

        <!-- Search Bar -->
        <div class="flex-1 max-w-xl mx-8">
          <div class="relative">
            <input
              type="text"
              placeholder="Search something here..."
              class="w-full px-6 py-3 bg-transparent border border-brew-cream/20 rounded-full text-brew-cream placeholder-brew-cream/50 focus:outline-none focus:border-brew-tan transition-colors"
            />
            <svg
              class="absolute left-4 top-1/2 -translate-y-1/2 w-5 h-5 text-brew-cream/50"
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
          </div>
        </div>

        <!-- Right Icons -->
        <div class="flex items-center gap-4">
          <button
            class="px-6 py-2 bg-brew-tan text-brew-dark rounded-full font-medium hover:bg-brew-tan/90 transition-all"
          >
            Search
          </button>

          <!-- Cart Icon -->
          <button
            class="w-10 h-10 rounded-full bg-brew-tan/20 flex items-center justify-center hover:bg-brew-tan/30 transition-colors"
          >
            <svg
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
          </button>

          <!-- User Icon -->
          <button
            class="w-10 h-10 rounded-full bg-brew-tan/20 flex items-center justify-center hover:bg-brew-tan/30 transition-colors"
          >
            <svg
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
          </button>

          <!-- Wishlist Icon -->
          <button
            class="w-10 h-10 rounded-full bg-brew-tan/20 flex items-center justify-center hover:bg-brew-tan/30 transition-colors"
          >
            <svg
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
        </div>
      </div>

      <!-- Bottom Row: Navigation Links -->
      <div class="border-t border-brew-tan/10">
        <div class="flex items-center gap-8 py-4">
          <RouterLink
            v-for="link in navLinks"
            :key="link.path"
            :to="link.path"
            class="text-brew-cream hover:text-brew-tan transition-colors font-medium"
            active-class="text-brew-tan"
          >
            {{ link.name }}
          </RouterLink>

          <!-- Contact with Dropdown -->
          <button
            class="flex items-center gap-1 text-brew-cream hover:text-brew-tan transition-colors font-medium"
          >
            Contact
            <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M19 9l-7 7-7-7"
              />
            </svg>
          </button>
        </div>
      </div>
    </div>
  </nav>
</template>

<script setup lang="ts">
const navLinks = [
  { name: 'Menu', path: '/menu' },
  { name: 'About', path: '/about' },
]
</script>
