<template>
  <footer class="relative bg-brew-dark border-t border-brew-tan/10">
    <!-- Background Image -->
    <div class="absolute inset-0">
      <!-- Desktop Background -->
      <img
        src="@/assets/images/bg-footer.png"
        alt=""
        class="hidden sm:block w-full h-full object-cover"
      />
      <!-- Mobile Background (optional - you can use same or different) -->
      <img
        src="@/assets/images/bg-footer-mobile.png"
        alt=""
        class="block sm:hidden w-full h-full object-cover"
      />
    </div>

    <!-- Decorative Coffee Cup Overlays - Hidden on mobile -->
    <div class="hidden md:block absolute inset-0 overflow-hidden opacity-10">
      <div
        v-for="i in 3"
        :key="i"
        class="absolute rounded-full border-4 border-brew-cream"
        :style="{
          width: '400px',
          height: '400px',
          top: `${i * 30}%`,
          left: `${i * 25}%`,
        }"
      >
        <!-- Coffee latte art pattern -->
        <div class="absolute inset-0 flex items-center justify-center">
          <div class="w-32 h-32 rounded-full border-2 border-brew-cream"></div>
        </div>
      </div>
    </div>

    <!-- Content -->
    <div class="relative z-10 max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-12 sm:py-16">
      <!-- Top Section: Logo and Social Icons -->
      <div class="mb-10 sm:mb-12 text-center sm:text-left">
        <RouterLink to="/" class="inline-block mb-4 sm:mb-6">
          <img
            src="@/assets/icons/brewtime.svg"
            alt="BrewTime Logo"
            class="h-12 sm:h-16 w-auto mx-auto sm:mx-0"
          />
        </RouterLink>

        <div class="flex items-center justify-center sm:justify-start gap-3 sm:gap-4">
          <SocialIcon
            v-for="social in socialLinks"
            :key="social.name"
            :icon="social.icon"
            :href="social.href"
            :aria-label="social.name"
          />
        </div>
      </div>

      <!-- Navigation Columns -->
      <div class="grid grid-cols-2 md:grid-cols-4 gap-6 sm:gap-8 mb-10 sm:mb-12">
        <FooterColumn
          v-for="column in footerColumns"
          :key="column.title"
          :title="column.title"
          :links="column.links"
        />
      </div>

      <!-- Bottom Section: Copyright -->
      <div class="pt-6 sm:pt-8 border-t border-brew-tan/10">
        <p class="text-brew-cream/60 text-xs sm:text-sm text-center">
          © 2023 Brew Time. All Rights Reserved.
        </p>
      </div>
    </div>
  </footer>
</template>

<script setup lang="ts">
import FooterColumn from '../ui/FooterColumn.vue'
import SocialIcon from '../ui/icons/SocialIcon.vue'

interface FooterLink {
  name: string
  path: string
}

interface FooterColumnData {
  title: string
  links: FooterLink[]
}

type IconName = 'facebook' | 'google' | 'apple' | 'instagram'

const socialLinks: { name: string; icon: IconName; href: string }[] = [
  { name: 'Facebook', icon: 'facebook', href: 'https://facebook.com' },
  { name: 'Google', icon: 'google', href: 'https://google.com' },
  { name: 'Apple', icon: 'apple', href: 'https://apple.com' },
  { name: 'Instagram', icon: 'instagram', href: 'https://instagram.com' },
]

const footerColumns: FooterColumnData[] = [
  {
    title: 'PRODUCTS',
    links: [
      { name: 'Features', path: '/features' },
      { name: 'Solutions', path: '/solutions' },
      { name: 'Integrations', path: '/integrations' },
      { name: 'Enterprise', path: '/enterprise' },
      { name: 'Solutions', path: '/solutions' },
    ],
  },
  {
    title: 'RESOURCES',
    links: [
      { name: 'Partners', path: '/partners' },
      { name: 'Community', path: '/community' },
      { name: 'Developers', path: '/developers' },
      { name: 'App', path: '/app' },
      { name: 'Blog', path: '/blog' },
    ],
  },
  {
    title: 'WHY CHOOSE US?',
    links: [
      { name: 'Channels', path: '/channels' },
      { name: 'Scale', path: '/scale' },
      { name: 'Watch the Demo', path: '/demo' },
      { name: 'Our Competition', path: '/competition' },
    ],
  },
  {
    title: 'COMPANY',
    links: [
      { name: 'About Us', path: '/about' },
      { name: 'News', path: '/news' },
      { name: 'Leadership', path: '/leadership' },
    ],
  },
]
</script>
