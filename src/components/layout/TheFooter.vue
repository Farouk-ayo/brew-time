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

<template>
  <footer class="relative bg-brew-dark border-t border-brew-tan/10">
    <div class="absolute inset-0">
      <img
        src="/images/bg-footer-mobile.webp"
        alt=""
        class="block sm:hidden w-full h-full object-cover"
      />
      <img src="/images/bg-footer.webp" alt="" class="hidden sm:block w-full h-full object-cover" />
    </div>

    <div class="hidden md:block absolute inset-0 overflow-hidden opacity-10 pointer-events-none">
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
        <div class="absolute inset-0 flex items-center justify-center">
          <div class="w-32 h-32 rounded-full border-2 border-brew-cream"></div>
        </div>
      </div>
    </div>

    <div class="relative z-10 max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-12 sm:py-16 lg:py-20">
      <div
        class="flex flex-col lg:flex-row lg:justify-between lg:items-start gap-10 lg:gap-16 mb-12 sm:mb-16"
      >
        <div class="flex flex-col items-start">
          <RouterLink to="/" class="inline-block mb-6 lg:mb-8">
            <img
              src="@/assets/icons/brewtime.svg"
              alt="BrewTime Logo"
              class="h-16 sm:h-20 lg:h-24 w-auto"
            />
          </RouterLink>

          <div class="flex items-center gap-2 lg:gap-2">
            <SocialIcon
              v-for="social in socialLinks"
              :key="social.name"
              :icon="social.icon"
              :href="social.href"
              :aria-label="social.name"
            />
          </div>
        </div>

        <div class="grid grid-cols-2 lg:grid-cols-4 gap-8 sm:gap-10 lg:gap-12 flex-1">
          <FooterColumn
            v-for="column in footerColumns"
            :key="column.title"
            :title="column.title"
            :links="column.links"
          />
        </div>
      </div>

      <div class="pt-6 sm:pt-8 border-t border-brew-tan/10">
        <p class="text-brew-cream/60 text-xs sm:text-sm text-center">
          © 2023 Brew Time. All Rights Reserved.
        </p>
      </div>
    </div>
  </footer>
</template>
