<template>
  <div class="text-center sm:text-left">
    <h3 class="text-brew-tan font-bold text-sm sm:text-base lg:text-lg mb-3 sm:mb-4 tracking-wide">
      {{ title }}
    </h3>
    <ul class="space-y-2 sm:space-y-3">
      <li v-for="link in links" :key="link.path">
        <RouterLink
          :to="link.path"
          class="text-brew-cream text-sm sm:text-base hover:text-brew-tan transition-colors inline-block"
        >
          {{ link.name }}
        </RouterLink>
      </li>
    </ul>
  </div>
</template>

<script setup lang="ts">
interface FooterLink {
  name: string
  path: string
}

interface Props {
  title: string
  links: FooterLink[]
}

defineProps<Props>()
</script>
