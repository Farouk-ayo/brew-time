<template>
  <nav class="fixed top-0 left-0 right-0 z-50 backdrop-blur-md">
    <div class="max-w-7xl mx-auto px-8">
      <!-- Top Row: Logo, Search, Icons -->
      <div class="flex items-center justify-between py-4">
        <!-- Logo -->
        <RouterLink to="/" class="flex items-center">
          <img src="@/assets/icons/brewtime.svg" alt="BrewTime Logo" class="h-10 w-auto" />
        </RouterLink>

        <!-- Search Bar -->
        <div class="flex-1 max-w-2xl mx-8">
          <div class="relative">
            <div class="absolute left-4 top-1 w-5 h-5 text-brew-cream/50 pointer-events-none">
              <IconButton class="bg-transparent" icon="search" @click="handleSearch" />
            </div>

            <input
              v-model="searchQuery"
              type="text"
              placeholder="Search something here..."
              class="w-full pl-15 pr-6 py-3 border border-brew-cream/2 bg-brew-tan/5 rounded-md text-white placeholder-brew-cream focus:outline-none focus:border-brew-tan/50 transition-colors"
              @keyup.enter="handleSearch"
            />
            <div class="absolute right-0 top-0">
              <BaseButton size="md" variant="primary" @click="handleSearch"> Search </BaseButton>
            </div>
          </div>
        </div>

        <!-- Right Icons -->
        <div class="flex items-center gap-4">
          <!-- Cart Icon -->
          <IconButton icon="cart" :badge="cartCount" @click="handleCartClick" />

          <!-- User Icon -->
          <IconButton icon="user" @click="handleUserClick" />

          <!-- Wishlist Icon -->
          <IconButton icon="wishlist" :badge="wishlistCount" @click="handleWishlistClick" />
        </div>
      </div>

      <!-- Bottom Row: Navigation Links -->
      <div class="border-t border-brew-cream">
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
        </div>
      </div>
    </div>
  </nav>
</template>

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

const handleSearch = () => {
  if (searchQuery.value.trim()) {
    router.push({ path: '/search', query: { q: searchQuery.value } })
  }
}

const handleCartClick = () => {
  router.push('/cart')
}

const handleUserClick = () => {
  router.push('/profile')
}

const handleWishlistClick = () => {
  router.push('/wishlist')
}
</script>
