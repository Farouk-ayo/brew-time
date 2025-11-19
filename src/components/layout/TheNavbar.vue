<script setup lang="ts">
import { ref } from 'vue'
import { useRouter } from 'vue-router'
import BaseButton from '../ui/BaseButton.vue'
import IconButton from '../ui/icons/IconButton.vue'

const router = useRouter()

const navLinks = [
  { name: 'Home', path: '/home' },
  { name: 'Menu', path: '/menu' },
  { name: 'About', path: '/about' },
  { name: 'Contact', path: '/contact' },
]

const searchQuery = ref('')
const cartCount = ref(3)
const wishlistCount = ref(5)
const isMobileMenuOpen = ref(false)
const isMobileSearchOpen = ref(false)

const handleSearch = () => {
  if (searchQuery.value.trim()) {
    router.push({ path: '/search', query: { q: searchQuery.value } })
    isMobileSearchOpen.value = false
  }
}

const handleCartClick = () => {
  router.push('/cart')
  isMobileMenuOpen.value = false
}

const handleUserClick = () => {
  router.push('/profile')
  isMobileMenuOpen.value = false
}

const handleWishlistClick = () => {
  router.push('/wishlist')
  isMobileMenuOpen.value = false
}

const toggleMobileMenu = () => {
  isMobileMenuOpen.value = !isMobileMenuOpen.value
  if (isMobileMenuOpen.value) {
    isMobileSearchOpen.value = false
  }
}

const toggleMobileSearch = () => {
  isMobileSearchOpen.value = !isMobileSearchOpen.value
  if (isMobileSearchOpen.value) {
    isMobileMenuOpen.value = false
  }
}
</script>

<template>
  <nav class="fixed top-0 left-0 right-0 z-50 backdrop-blur-md border-b border-brew-cream/10">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="flex items-center justify-between py-4 md:py-4">
        <RouterLink to="/" class="flex items-center shrink-0">
          <img src="@/assets/icons/brewtime.svg" alt="BrewTime Logo" class="h-12 md:h-10 w-auto" />
        </RouterLink>

        <div class="hidden lg:flex flex-1 max-w-2xl mx-8">
          <div class="relative w-full">
            <div class="absolute left-4 top-1 w-5 h-5 text-brew-cream/50 pointer-events-none">
              <IconButton class="bg-transparent" icon="search" @click="handleSearch" />
            </div>

            <input
              v-model="searchQuery"
              type="text"
              placeholder="Search something here..."
              class="w-full pl-14 pr-28 py-3 border border-brew-cream/20 bg-brew-tan/5 rounded-md text-white placeholder-brew-cream/60 focus:outline-none focus:border-brew-tan/50 transition-colors"
              @keyup.enter="handleSearch"
            />
            <div class="absolute right-0 top-0">
              <BaseButton size="md" variant="primary" @click="handleSearch">Search</BaseButton>
            </div>
          </div>
        </div>

        <div class="flex items-center gap-3 md:gap-4">
          <button
            class="lg:hidden w-10 h-10 md:w-10 md:h-10 rounded-full bg-brew-tan/5 flex items-center justify-center hover:bg-brew-tan/30 transition-colors"
            @click="toggleMobileSearch"
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
                d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"
              />
            </svg>
          </button>

          <IconButton
            icon="cart"
            :badge="cartCount"
            @click="handleCartClick"
            customClass="w-10 h-10 md:w-10 md:h-10 bg-brew-tan/5 hover:bg-brew-tan/30"
            iconClass="w-5 h-5 md:w-5 md:h-5 text-brew-cream"
          />
          <IconButton
            icon="user"
            @click="handleUserClick"
            customClass="hidden sm:flex w-10 h-10 md:w-10 md:h-10 bg-brew-tan/5 hover:bg-brew-tan/30"
            iconClass="w-5 h-5 md:w-5 md:h-5 text-brew-cream"
          />
          <IconButton
            icon="wishlist"
            :badge="wishlistCount"
            @click="handleWishlistClick"
            customClass="hidden sm:flex w-10 h-10 md:w-10 md:h-10 bg-brew-tan/5 hover:bg-brew-tan/30"
            iconClass="w-5 h-5 md:w-5 md:h-5 text-brew-cream"
          />

          <button
            class="md:hidden w-10 h-10 rounded-full bg-brew-tan/5 flex items-center justify-center hover:bg-brew-tan/30 transition-colors"
            @click="toggleMobileMenu"
          >
            <svg
              v-if="!isMobileMenuOpen"
              class="w-6 h-6 text-brew-cream"
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
              v-else
              class="w-6 h-6 text-brew-cream"
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
        </div>
      </div>

      <div v-if="isMobileSearchOpen" class="pb-4 lg:hidden border-t border-brew-cream/10 pt-4">
        <div class="relative">
          <input
            v-model="searchQuery"
            type="text"
            placeholder="Search..."
            class="w-full pl-4 pr-24 py-3 border border-brew-cream/20 bg-brew-tan/5 rounded-md text-white placeholder-brew-cream/60 focus:outline-none focus:border-brew-tan/50 transition-colors"
            @keyup.enter="handleSearch"
          />
          <div class="absolute right-0 top-0">
            <BaseButton size="md" variant="primary" @click="handleSearch">Search</BaseButton>
          </div>
        </div>
      </div>

      <div class="hidden md:flex border-t border-brew-cream/10">
        <div class="flex items-center gap-6 lg:gap-8 py-3 md:py-4">
          <RouterLink
            v-for="link in navLinks"
            :key="link.path"
            :to="link.path"
            class="text-sm md:text-base text-brew-cream hover:text-brew-tan transition-colors font-medium"
            active-class="text-brew-tan"
          >
            {{ link.name }}
          </RouterLink>
        </div>
      </div>
    </div>

    <div
      v-if="isMobileMenuOpen"
      class="md:hidden border-t border-brew-cream/10 bg-brew-dark/95 backdrop-blur-md"
    >
      <div class="px-4 py-3 space-y-1">
        <RouterLink
          v-for="link in navLinks"
          :key="link.path"
          :to="link.path"
          class="block px-4 py-3 text-brew-cream hover:text-brew-tan hover:bg-brew-tan/5 rounded-md transition-colors font-medium"
          active-class="text-brew-tan bg-brew-tan/10"
          @click="isMobileMenuOpen = false"
        >
          {{ link.name }}
        </RouterLink>

        <div class="flex gap-3 pt-3 border-t border-brew-cream/10 px-4">
          <button
            class="flex-1 flex items-center justify-center gap-2 py-3 bg-brew-tan/5 hover:bg-brew-tan/10 rounded-md transition-colors text-brew-cream text-sm font-medium"
            @click="handleUserClick"
          >
            <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M16 7a4 4 0 11-8 0 4 4 0 018 0zM12 14a7 7 0 00-7 7h14a7 7 0 00-7-7z"
              />
            </svg>
            Profile
          </button>
          <button
            class="flex-1 flex items-center justify-center gap-2 py-3 bg-brew-tan/5 hover:bg-brew-tan/10 rounded-md transition-colors text-brew-cream text-sm font-medium relative"
            @click="handleWishlistClick"
          >
            <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M4.318 6.318a4.5 4.5 0 000 6.364L12 20.364l7.682-7.682a4.5 4.5 0 00-6.364-6.364L12 7.636l-1.318-1.318a4.5 4.5 0 00-6.364 0z"
              />
            </svg>
            Wishlist
            <span
              v-if="wishlistCount > 0"
              class="absolute -top-1 -right-1 min-w-5 h-5 px-1 bg-brew-tan text-brew-dark text-xs font-bold rounded-full flex items-center justify-center"
            >
              {{ wishlistCount > 9 ? '9+' : wishlistCount }}
            </span>
          </button>
        </div>
      </div>
    </div>
  </nav>
</template>
